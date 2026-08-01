!!! tip "Experiment"
	results from a Malus Law experiment carried out using a TSL2561 Luminosity sensor, a laser diode, two pieces of polarizers
	ripped out of an LCD screen, and a hollow shaft stepper motor.

	![Screenshot](/images/malus.png)

	The analyzer was rotated step by step, and light intensity was recorded using the light sensor. It confirms maximum transmission
	when both polarizer and analyzer are parallel, and minimum when orthogonal.
	
	Ambient light should be fully blocked by leveraging a dark room

	Curve fitting showed that the shape was sinusoidal (cos^(theta))


```python
import time
from matplotlib import pyplot as plt
from eyes17 import eyes
from eyes17.SENSORS import TSL2561

p = eyes.open()
sens = TSL2561.connect(p.I2C)
p.set_state(SQR1=False) # connect SQ1 output to the STP input ofthe motor driver module(A4988)
plt.ion()
for a in range(200):# step size is 360/200. 200 steps per revolution motor
	val = sens.getRaw() #Get RAW readings from the sensor [Total,Infrared, Visible]
	plt.scatter(a*360/200.,val[0]) #Plot angle vs intensity. If using microstepping, divide angle by 16 or 32 or 64 as per the setting.
	p.set_state(SQR1=True)  #Pulse SQ1 to make the motor take one step
	time.sleep(0.001)
	p.set_state(SQR1=False)
	time.sleep(0.001)
	plt.pause(0.05)#50mS delay
```