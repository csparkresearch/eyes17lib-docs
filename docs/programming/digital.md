# Digital I/O and Timing

## Set and Sense Logic Levels

Set/sense logic levels on digital pins **SQ1**, **SQ2**, **OD1**, **SEN**, **IN2**, and **CCS**.

Digital input names accepted by timing / frequency calls:

`IN2`, `SEN`, `SQR1`, `OD1`, `SQR1_READ`, `OD1_READ`, `SQ2`, `SQ3`

Digital outputs controlled by `set_state`:

`OD1`, `CCS`, `SQR1` (alias `SQ1`), `SQR2` (alias `SQ2`)

---

### set_state : set a digital pin HIGH (5 V) / LOW (0 V)

`p.set_state(**kwargs)`

| parameter  | description |
|------------|-------------|
| \*\*kwargs | `SQR1` / `SQ1`, `SQR2` / `SQ2`, `OD1`, `CCS` = `True` (HIGH / on) or `False` (LOW / off) |

Only pins passed as keyword arguments are changed; others are left untouched.

!!! tip "Set SQ1 to 5 V, OD1 to 0 V"
	```python
	import eyes17.eyes
	p = eyes17.eyes.open()
	p.set_state(SQR1=True, OD1=False)
	```

!!! tip "Enable CCS (ExpEYES-17 constant current source)"
	```python
	# ExpEYES-17 only: fixed ~1.1 mA (see p.currentSourceValue)
	# SEELab3 uses programmable PCS via p.set_pcs() instead — see Voltage Outputs
	p.set_state(CCS=True)
	print('CCS current ≈', p.currentSourceValue, 'A')
	p.set_state(CCS=False)  # turn off
	```

---

### get_states : get logic levels on digital pins

`p.get_states()`

| Returns | description |
|---------|-------------|
| dict    | `{'IN2', 'SQR1', 'OD1', 'SEN', 'SQR1_OUT', 'OD1_OUT', 'CCS'}` → `True`/`False` |

!!! tip "Measure state of IN2"
	```python
	import eyes17.eyes
	p = eyes17.eyes.open()
	states = p.get_states()
	print(f"IN2 is {'HIGH' if states['IN2'] else 'LOW'}")
	```

??? info "Example output"
	```python
	{
	 'IN2': True,
	 'SQR1': False,
	 'OD1': False,
	 'SEN': True,
	 'SQR1_OUT': False,
	 'OD1_OUT': False,
	 'CCS': False
	}
	```

### get_state : get logic level on one pin

`p.get_state(channel)`

| Parameter | description |
|-----------|-------------|
| channel   | key from `get_states()`, e.g. `'IN2'`, `'OD1'`, `'SEN'`, `'CCS'` |
| _Returns_ | `bool` — `True` / `False` |

```python
p.get_state('SEN')
```

---

## Measure Frequencies and Duty Cycle

### get_freq : frequency on IN2 / SEN

`p.get_freq(channel='IN2', timeout=1.0)`

Measures time for 4 rising edges of the input signal.

| parameter | description |
|-----------|-------------|
| channel   | `'IN2'` or `'SEN'` (see digital input list above) |
| timeout   | seconds; returns `0` if timed out |
| _return_  | frequency in Hz |

```python
p.set_sq1(1000)
# Connect SQ1 → IN2
print(p.get_freq('IN2'))
```

### get_high_freq : high frequency via counter

`p.get_high_freq(pin)`

Counts edges for 100 ms using a hardware counter. Useful for frequencies above ~100 kHz. Avoid using the oscilloscope at the same time (shared hardware).

```python
print(p.get_high_freq('IN2'))
```

### duty_cycle : duty cycle on a pin

`p.duty_cycle(pin, timeout=2.0)`

| parameter | description |
|-----------|-------------|
| pin       | digital input, e.g. `'IN2'` |
| _return_  | duty cycle in % , or `-1` on timeout |

```python
print(p.duty_cycle('IN2'))
```

---

## Timing Measurements

Times are returned in **seconds** (unless noted). Returns `-1` or `None` on timeout.

### Interval between edges

| Function | Meaning |
|----------|---------|
| `r2rtime(pin1, pin2)` | Rising edge on `pin1` → rising edge on `pin2` |
| `f2ftime(pin1, pin2)` | Falling → falling |
| `r2ftime(pin1, pin2)` | Rising → falling |
| `f2rtime(pin1, pin2)` | Falling → rising |

Pins may be the same or different (`'IN2'`, `'SEN'`, …). For multiple cycles on one pin, prefer `multi_r2rtime`.

```python
# Connect SQ1 → IN2
p.set_sq1(1000)
T = p.r2rtime('IN2', 'IN2')   # period ≈ 0.001 s
print('Period (s) =', T, '  Freq (Hz) =', 1 / T)
```

### multi_r2rtime : several rising edges on one pin

`p.multi_r2rtime(pin, edges=1, timeout=1.0)`

Time spanning `edges` cycles. Valid `edges`: `1, 2, 3, 4, 8, 12, 16, 32, 48`.

```python
# Time for 8 cycles → better resolution at high frequency
T = p.multi_r2rtime('IN2', 8)
print('Freq =', 8 / T)
```

### Output-then-measure (set / clear → edge)

Useful for RC timing, light-barrier TOF, etc.

| Function | Action |
|----------|--------|
| `set2rtime(out, inp)` | Drive `out` HIGH, time until rising edge on `inp` |
| `set2ftime(out, inp)` | Drive `out` HIGH, time until falling edge on `inp` |
| `clr2rtime(out, inp)` | Drive `out` LOW, time until rising edge on `inp` |
| `clr2ftime(out, inp)` | Drive `out` LOW, time until falling edge on `inp` |

`out` must be a digital output: `'OD1'`, `'CCS'`, `'SQR1'`, `'SQR2'`.

```python
# Example: charge via OD1, wait for threshold on SEN
t = p.set2rtime('OD1', 'SEN')
print('Charge time (s) =', t)
```

---

### MeasureInterval : general two-edge interval

`p.MeasureInterval(channel1, channel2, edge1, edge2, timeout=0.1)`

| parameter | description |
|-----------|-------------|
| channel1, channel2 | digital inputs |
| edge1, edge2 | `'rising'`, `'falling'`, or `'four rising edges'` |
| _return_ | signed time in seconds (`NaN` on timeout). Negative if event 2 occurred first |

```python
dt = p.MeasureInterval('IN2', 'SEN', 'rising', 'falling')
```

### SinglePinEdges / DoublePinEdges : timestamped edges

Lower-level calls that return arrays of edge timestamps (seconds).

```python
# Up to 4 rising edges on IN2; optionally set OD1 when starting
T = p.SinglePinEdges('IN2', 'rising', 4, timeout=1.0, OD1=True)

# Edges on two pins
T1, T2 = p.DoublePinEdges('IN2', 'SEN', 'rising', 'falling', 2, 2)
```

`edgeType` options: `'rising'`, `'falling'`, `'4xrising'`, `'16xrising'`.

`MeasureMultipleDigitalEdges` is an older two-channel API; prefer `DoublePinEdges` / `SinglePinEdges`.

---

## Hardware edge counter

For continuous high-rate counting on a digital input (shared hardware with `get_high_freq` — avoid using the oscilloscope at the same time).

| Function | Description |
|----------|-------------|
| `startCounter(chan)` | Reset and arm the 32-bit counter on `chan` (e.g. `'IN2'`) |
| `pauseCounter()` | Freeze counting |
| `resumeCounter()` | Continue counting |
| `getCounts()` | Read the current count |

```python
import time
import eyes17.eyes
p = eyes17.eyes.open()

p.set_sq1(10000)          # 10 kHz test signal → connect SQ1 to IN2
p.startCounter('IN2')
time.sleep(1.0)
print(p.getCounts())      # ≈ 10000
p.pauseCounter()
c1 = p.getCounts()
time.sleep(0.5)
print(p.getCounts() == c1)  # True while paused
p.resumeCounter()
time.sleep(0.5)
print(p.getCounts())
```

---

## Ultrasonic distance (HC-SR04)

Wiring: **SQ2 → TRIG**, **IN2 ← ECHO**, plus 5 V and GND.

| Function | Returns |
|----------|---------|
| `sr04_distance(speed_of_sound=340.)` | distance in **cm** (`0` on timeout) |
| `sr04_distance_time(...)` | `(timestamp, distance_cm)` |
| `sr04_time()` | raw echo time in **seconds** |

```python
print(p.sr04_distance(), 'cm')
```

---

## Servo motor

`p.servo(angle, chan='SQR1')`

Outputs ~100 Hz PWM on SQ1 for hobby servos (e.g. SG-90). `angle` is 0–180°.

```python
p.servo(90)   # center
```

---

## Multiplexer / stepper (SEELab3 CS1–CS4)

`set_multiplexer(value)` sets CS1–CS4 to the binary of `value` (0–15), for chips such as CD74HC4067.

`stepper_move(steps, direction, step_delay=0.01)`, `stepper_forward()`, `stepper_reverse()` step a motor wired to CS1–CS4 using a full-step sequence.
