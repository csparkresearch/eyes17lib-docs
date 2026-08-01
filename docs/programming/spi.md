# SPI bus (`p.SPI`)

Available on hardware form factors with SPI (firmware version ≥ ~5.0 / SEELab3-class boards). Chip-select lines: **CS1–CS4** (also listed as selectable pins in `set_cs`).

Access via `p.SPI`.

---

## set_parameters : clock and mode

`p.SPI.set_parameters(primary_prescaler=0, secondary_prescaler=2, CKE=1, CKP=0, SMP=1)`

| parameter | description |
|-----------|-------------|
| primary_prescaler | 0–3 → divide 64 MHz by 64, 16, 4, or 1 |
| secondary_prescaler | 0–7 → further divide by 8…1 |
| CKE, CKP, SMP | SPI mode bits (clock edge / polarity / sample) |

```python
p.SPI.set_parameters(primary_prescaler=0, secondary_prescaler=2, CKE=1, CKP=0)
```

---

## Chip select

| Function | Effect |
|----------|--------|
| `p.SPI.start(channel)` | Assert CS (drive low). `channel`: `'CS1'`, `'CS2'`, `'CS3'`, `'CS4'` (also `'A1'`/`'A2'` as CS in some builds) |
| `p.SPI.stop(channel)` | Deassert CS (drive high) |
| `p.SPI.set_cs(channel, state)` | `state=0` select, `state=1` release |

---

## Transfer

| Function | Description |
|----------|-------------|
| `send8(value)` | Exchange one byte; returns byte from slave |
| `send16(value)` | Exchange 16-bit word; returns response |
| `send8_burst` / `send16_burst` | Transmit without waiting for ACK (faster, no return) |
| `xfer(chan, data)` | `start(chan)`, send each byte in `data` with `send8`, `stop(chan)`; returns list of replies |

```python
# Example pattern: write command 0x9F, read 3 bytes (device-specific)
p.SPI.set_parameters()
reply = p.SPI.xfer('CS1', [0x9F, 0x00, 0x00, 0x00])
print(reply)
```

Manual CS control:

```python
p.SPI.start('CS1')
print(p.SPI.send8(0x01))
print(p.SPI.send16(0xABCD))
p.SPI.stop('CS1')
```

---

## map_reference_clock

`p.SPI.map_reference_clock(scaler, *destinations)`

Route an internal reference clock to `SQR1`, `SQR2`, `CS3`, and/or `WAVEGEN`.

Output frequency ≈ \(128 / 2^{\mathrm{scaler}}\) MHz (`scaler` 0–15).

```python
p.SPI.map_reference_clock(2, 'SQR1')   # ≈ 32 MHz on SQ1
# Lower WAVEGEN clock for finer AD9833 resolution (SEELab boards with DDS):
p.SPI.map_reference_clock(7, 'WAVEGEN')
```
