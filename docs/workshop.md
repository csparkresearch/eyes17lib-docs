
Academy of Physics Teachers, Kerala, in association with several colleges, is organizing a series of Two-Day Workshops on ExpEYES. The schedule is HERE. The focus will be on hands-on training, to enable the participants perform experiments independantly.

The software is currently available for PCs and Android phones. The workshop will be conducted using Android phones and all the participants are expected to bring an Android phone with the SEELab app installed from Google play store. Click here to install [Seelab 3](https://play.google.com/store/apps/details?id=com.cspark.research.eyes17)

ExpEYES is an instrument that can be interfaced to the USB port of a computer or Android phone. It provides a set of Input/Output terminals that will act as test equipment like DC power supply, Function generator, Oscilloscope, Frequency counter, Capacitance meter etc. It also Also supports I2C sensor elements for measuring physical parameters like temperature, pressure, magnetic field etc. More details are [HERE](programming/sensors.md)

Plan of the program is given below. Participants are advised to go through the material below before attending the program. Click on the links for the details of each activity. During hands-on sessions, two participants will be sharing one ExpEYES kit. Minimum 20 kits will be made available.

The time schedule given below need to be followed strictly to cover the listed topics.

## Day 1

### Session 1 (10:15 AM - 11:15 AM)

Demonstration of five experiments selected from different branches of physics.

+ Acceleration due to gravity from the Time of Flight of a falling body. This experiment is conceptually very simple. 
+ Acceleration due to gravity from the Period of Oscillation of a Rod Pendulum. 
+ Frequency Response of an active band pass filter, wired using n Op-amp. The frequency and phase responses are explored. 
+ Transistor Characteristics. Output characteristics of an NPN transistor in the CE configuration is plotted. 
+ Velocity of Sound. The velocity of sound can be obtained by measuring the wavelength directly, which is done by finding out the distance between two adjacent points having minimum and maximum pressure.  OR generating Cooling curve .

Explanation of the Input/Output terminals is given on the [main page](index.md). Introduction to the Oscilloscope GUI.

### Session 2: Hands-on (11:15 AM - 1:00 PM)

The activities in this session will make the user familiar with the usage of the Input/output terminals of ExpEYES.

+ Measuring a DC voltage : Measure the voltage between the terminals of single drycell. Also their parallel and series combinations.
+ Generating and Measuring Voltage : ExpEYES has programmable DC voltage sources that can be used instead of cells. This section explains how to control and measure DC voltages.
+ Measuring Capacitance : Measure the capacitance of different types of capacitors. Make a parallel plate capacitor using aluminium foil and measure it.
+ Lemon Cell : A lemon cell is constructed using Zinc and Copper Electrodes. The voltage is measured with and without connecting a load resistor to calculate the internal resistance of the cell.
+ DC Resistance of Human Body : A small DC voltage is applied across human body to measure it’s resistance.
+ Electromagnetic Induction. A magnet is dropped into a coil and the resulting induced voltage waveform is captured.
+ Simple AC Generator. A AC generator is made by placing a coil near a rotating magnet.
+ Direct and Alternating Currents. Explains the difference by plotting the voltage as a function of time.

### Session 3: Hands-on (2:00 PM - 3:30 PM)

Continuation of the previous session, covering several experiments to study the nature of alternating current and the behavior of LCR circuits, mostly corrresponding to the theory taught in 12th standard. For a brief description of the theory login a guest to this LMS.

+ Resistor in AC Circuits. Explores the current and voltage of AC across a resistor. Amplitude and phase relationships are observed.
+ Capacitor in AC Circuits. Explores the relation between current and voltage of AC applied to a capacitor. The phase shift between voltage and current is observed. The capacitive reactance is obtained from the ampltudes.
+ Inductor in AC Circuits Explores the relation between current and voltage of AC applied to an Inductor.
+ AC to Series LCR circuit, Resonance. Explores the series LCR circuit under AC. Resonance is demonstrated.
+ Resistivity of Water using AC. Resistivity of water is measured by comparing with a known resistance, under an AC voltage.
+ AC Resistance of Human Body. Role of capacitance in the resistance of human body is demonstrated.

### Session 4: (3:45 PM - 4.45 PM) Programming ExpEYES using Python

Even though GUI programs are available for many experiments, programming ExpEYES gives a deeper understanding amd also enables the user to design new experiments. There are library functions to control/monitor the Input/Output terminals. 

Python code for some experiments presented in Session 1 will be discussed.

## Day 2:

### Session 1: Hands-on (9:30 AM - 11:15 AM) B.Sc level Experiments

Most of the experiments in this section are part of the B.Sc syllabus. Conventional method requires DC power supply, oscilloscope, function generator and frequency counter to perform them. Experiments like studying the Transient Response of LCR circuits is difficult with conventional equipment. Due to this reason they are currently present only in the theory part. ExpEYES can be used to perform all these experiments.

+ RLC circuit transient response. Apply a voltage step to a series LCR circuit and capture the resulting voltage across the capacitor. Study the underdamped, overdamped and critically damped cases. Also explore the step response of RC and RL circuits.
+ RLC circuit steady state response. Study of Series Resonance.
+ Half wave rectifier
+ Full wave rectifier
+ Clipping circuit using Diode
+ Clamping circuit using Diode

### Session 2. (11:30 AM - 1:00 PM) B.Sc level Experiments

+ Oscillator using IC555
+ Diode VI Characteristic
+ NPN transistor output characteristic
+ Transistor amplifier
+ PNP transistor output characteristic

### Session 3 (2:00 PM - 3:30 PM)

+ Inverting amplifier using Op-Amp
+ Construction of Logic gates using PN junctions and testing using square wave inputs.
+ Frequency Response of an active band pass filter
+ Distance measurement using Echo module. Measurements on oscillating Mass and Spring system.
+ Distance measurement using VL53LOX LIDAR

### Session 4. Conclusion and Feedback (3:45 to 4:30)