---
social:
  cards_layout_options:
    background_color: blue # Change background color
    background_image: /images/gluco_conns.jpg
---

!!! tip "Experiment"
	Reverse engineer a commercial glucometer by monitoring the applied and measured signals to study its 
	amperometry process.

Glucometers are fascinating devices, and I pulled apart a glucometer to monitor the signals
it applies and receives. 

The microcontroller used is a PIC16F1786, which has a 12 bit ADC, and an 8 bit DAC, making it
perfect for such applications. It is paired with a USB to serial convertor, and subsequently a type C plug.

![](/images/gluco_conns.jpg)


An LM358 op-amp was identified, and since it is a dual Op-amp,
I monitored both of the outputs using A1, and A2

![](/images/gluco_photos.jpg)

With the monitoring probes connected, I attached the meter to my phone, inserted a strip,
and proceeded to add a tiny drop of blood to get the meter to start measuring.

Both graphs were overlapping, but with slightly different noise floors, indicating that 
the opamps may have been used in cascaded form.

side note: The meter shows the results a few seconds after the graph hits the peak.

![](/images/gluco_plot.png)

On closer inspection, the DAC1OUT pin(RA2) is connected to the non-inverting input A of
the opamp, and the output is connected to the non-inverting opamp B

Further inspection shows that the - input of this stage is connected to the `working electrode(WE)`.
the configuration is similar to Figure 1 or 2 in [this technical article](https://www.analog.com/en/resources/technical-articles/blood-glucose-meters.html)
by Analog Devices.

![](/images/gluco_schematic.gif)

The strip connector from left to right has pins

`counter electrode` `NC` `GND` `Working Electrode`

The output is simply buffered using the second half of this opamp, and connected to RA0 which is probably mapped
to the internal 12 bit ADC.


So the configuration allows measurement of current at the `working electrode`, but the
counter electrode is directly connected to RB3, which is also pulled up to Vref via a resistor.

The electrode near the `working` one is grounded, and the other is not connected.

### Points to monitor

RA2 connected to pin3(in+) of the opamp is of interest, as is pin1(out) of the opamp. RA5
monitors the -Ve input(pin 2) of the opamp, but since it is directly connected to the `working electrode`
I do not plan to touch it for now.

### readings






