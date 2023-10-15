# I2C Communication interface

The I2C interface consists of 2 pins:

+ SCL, also known as the clock pin.
+ SDA, also known as the data pin.

With these two connections, and a power supply, it is possible to get data from a variety of sensors measuring
physical parameters.

## I2C function calls


=== "p.I2C.Scan()"
	```python
	def I2CScan()
	scan the I2C bus, and return a list of addresses that responded
	
	  return: list of numbers between 0-127.
	
	```

=== "p.I2C.writeBulk()"
	```python
	def I2CWriteBulk(address,bytestream)
	write a set of bytes to an I2C address
	
	  address: Address of I2C slave device. 0-127
	  bytestream: list of bytes to write
	  return: True if success.
	
	```

=== "p.I2C.readBulk()"
	```python
	def I2CReadBulk(address,register,total_bytes)
	write a set of bytes to an I2C address
	
	  address: Address of I2C slave device. 0-127
	  register: The starting address in the I2C slave device from where bytes are to be read
	  total_bytes: Total number of bytes to read
	  return: bytes, timeout
	  "ignore contents if timeout==True"
	
	```


## Monitor I2C Sensors

!!! info "List of I2C sensors supported thus far (Minimal data logging. Configuration options available for some)"
	- MS5611 : 24 bit pressure and temperature sensor. Can resolve 15cm height variations
	- BMP280 : Pressure and temperature Sensor
	- BME280: Humidity measurement
	- TSL2561/BH1750: Light intensity sensor
	- MPU6050: 3 Axis Accelerometer, 3 axis Angular velocity (Gyro)
	- MPU9250 : 9-DOF sensor Accel/Gyro/Magnetic Fields
	- VL53L0X : Distance measurement (LIDAR)
	- MLX90614: Passive IR temperature sensor
	- AD8232 : ECG instrumentation ampliﬁer
	- with 3 electrodes
	- AD9833: Precision Sine Wave generator
	- Dual AD9833 with 3V output
	- AD9833: Precision Sine Wave generator
	- Single output. 0.6V P2P
	- Servo Motors via SQ1, SQ2, or PCA9685
	- AHT10: Humidity Sensor
	- MAX44009; Visible Spectrum Luminosity sensor
	- QMC5883L/HMC5883L : 3 Axis Magnetometer
	- ML8511 : UV sensor
	- MAX30100: Heart rate and pulse oximetry
	- INA219 : High Side Current Sensing
	- ADS1115 : 16 bit , 4 channel voltmeter
	- TCS34725 : RGB Color sensor
	- ADXL345: 3 axis accelerometer
	- SR04 : Distance sensor (Sound based)

## Luminosity sensor(TSL2561) Example

A light sensor is being monitored with the flash of the camera enabled. As the camera approaches the sensor, the readings go up. Not a very clever example. TODO.

[Project Example with TSL2561 light sensor: Malus Law](../malus.md)
