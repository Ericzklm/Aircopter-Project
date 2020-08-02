This project was done in association with the IEEE Student Branch on the UCLA campus.
This is the first iteration of the project.

The goal of the project was to: 1. Design and assemble a custom PCB for a drone,
2. Write a program to hover the drone, then fly the drone. Because of the nature
of the project, the PCB was required to be small and compact (meaning SMD soldering
was needed) and the program needed to be quick and responsive.

Hardware Design Choices:

MCU: The main chip is the model STM32F405. This was chosen for its ideal balance
between size and functionality. It is able to support all the needed sensors and
motor drivers for our drone and can be powered by a 3.3v supply which closely
matches the 3.7v of standard drone batteries (3.7v is stepped down to 3.3 using
a voltage regulator). Additionally, this chip was more ideal than other chips of
similar style because it handles floating point calculations better which allows
for simplicity and efficiency when writing the program.

Voltage Regulator: The voltage regulator used is the Richtek RT6150B-33GQW which
was choosen for its size and the use of buck-boost as well as operating within
the voltage supplied by the battery. The voltage regulator was simple to use
and had a well documented spec sheet in comparison to other choices but used
exposed pads instead of pins for soldering which proved to be the biggest
challenge in assembly.

Wireless Module: The wireless module used is the nrf24l01 which is standard, easy
to use, and familiar so we used it in this application since it fits well with the
acclerometer module.

Accelerometer/Gyroscope: The module used is the mpu6050 which is standard, easy to
use, and familiar so we used it in this application since it fits well with the
wireless module.

Oscillator: The oscillator used is the Abracon ABLS-12.000MHZ-B2-T which is a
crystal oscillator at 12 mHz which was suitable for the MCU. This specific oscillator
was choosen because the documentation was clear on how to configure the module. A
SMD mounted version was chosen.

Passive Components: For the resistors, capacitors, and inductors, we primarily
used parts with the package size 0603 which would fit the board without being
overly difficult to solder. Each piece was checked for its operating voltages as 
well as the operating temperatures to make sure no issues would arise.




