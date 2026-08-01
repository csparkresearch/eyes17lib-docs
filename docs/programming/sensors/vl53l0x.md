# VL53L0X / VL53L01X — Time-of-flight distance

I2C address **0x29**. Driver module: `eyes17.SENSORS.VL53L01X`.

```python
from eyes17 import eyes
from eyes17.SENSORS import VL53L01X

p = eyes.open()
tof = VL53L01X.connect(p.I2C)
print(tof.getRaw())   # distance reading (mm-scale per driver)
```

Init prints revision / model IDs over I2C. Keep the target within the sensor’s rated range and avoid highly absorptive surfaces for best results.
