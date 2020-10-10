# Aircopter Project

#### To see a more updated version of this project, see Aircopter-Project-v2

This project was done in association with the IEEE Student Branch on the UCLA campus.
This is the first iteration of the project.

The goal of the project was to: 1. Design and assemble a custom PCB for a drone,
2. Write a program to hover the drone, then fly the drone. Because of the nature
of the project, the PCB was required to be small and compact (meaning SMD soldering
was needed) and the program needed to be quick and responsive.

### Hardware Selection Choices:

**MCU**: The main chip is the model STM32F405. This was chosen for its ideal balance
between size and functionality. It is able to support all the needed sensors and
motor drivers for our drone and can be powered by a 3.3v supply which closely
matches the 3.7v of standard drone batteries (3.7v is stepped down to 3.3 using
a voltage regulator). Additionally, this chip was more ideal than other chips of
similar style because it handles floating point calculations better which allows
for simplicity and efficiency when writing the program.

**Voltage Regulator**: The voltage regulator used is the Richtek RT6150B-33GQW which
was choosen for its size and the use of buck-boost as well as operating within
the voltage supplied by the battery. The voltage regulator was simple to use
and had a well documented spec sheet in comparison to other choices but used
exposed pads instead of pins for soldering which proved to be the biggest
challenge in assembly.

**Wireless Module**: The wireless module used is the nrf24l01 which is standard, easy
to use, and familiar so we used it in this application since it fits well with the
acclerometer module.

**Accelerometer/Gyroscope**: The module used is the mpu6050 which is standard, easy to
use, and familiar so we used it in this application since it fits well with the
wireless module.

**Oscillator**: The oscillator used is the Abracon ABLS-12.000MHZ-B2-T which is a
crystal oscillator at 12 mHz which was suitable for the MCU. This specific oscillator
was choosen because the documentation was clear on how to configure the module. A
SMD mounted version was chosen.

**Passive Components**: For the resistors, capacitors, and inductors, we primarily
used parts with the package size 0603 which would fit the board without being
overly difficult to solder. Each piece was checked for its operating voltages as 
well as the operating temperatures to make sure no issues would arise.

### Hardware Design Choices:

**General**: The board is composed of two sides where each side has routes and vias to
connect the different components. The negative spaces are occupied by polygons. On
the front side, there is a seperate polygon for 3.7v and 3.3v that are connected
by the voltage regulator that steps the voltage down. On the back, there are seperate
polygons for ground and motor ground. Motor ground is seperated because the motor
ground will have more noise and we dont want to include the added noise in other
components.

**Battery**: The battery is a generic 3.7v drone battery that connects via a JST connector.
A couple of decoupling capacitors are placed directly alongside the female header on the 
board. It is placed as close as possible to the JST headers that connect to the motors
as we need to decrease the resistance by having a large polygon that gives a direct
connection.

**Voltage Regualtor**: The voltage regulator is placed between the 3.7v and 3.3v planes
such that the two are completely isolated. There is an inductor included directly
alongside the voltage regulator as recommended by the spec sheet. A few decoupling
capcitors are also included.

**Voltage Divider**: A couple resistors are used to form a voltage divider that gives
an analog input to the MCU which can be used to read battery status. These resistors
are placed such that they do not have signficant effect on the routing or the polygons.

**Programmer**: The programmer is a set of 4 male header pins that allow us to upload 
programs to the drone through a seperate board. It is placed in the top left corner
for easy access and to make sure the sensors do not cover the pins.

**Reset Button**: The switch is placed such that there is easy access to it while not having
the placement disrupt any polygons. A capacitor is included to stabalize the signal sent
to the MCU.

**Oscillator**: The oscillator is placed as close to the MCU as possible to reduce unwanted
affects on the traces. As indicated by the spec sheet, there are two resistors that
ground both the input and output of the oscillator.

**Motors**: The motors connectorsare placed along the top of the board for easy access when 
plugging in the JST connectors. Each motor is paired with a motor driver circuit including
a diode and a mosfet. These components are located as close as possible to each other and 
have the thickest possible traces to decrease resistance. Each motor driver is connected
to a PWM capable pin located on the MCU.

**MCU**: The MCU is placed in a central position on the board as it needs to connect to most
components on the board. It is turned such that the length of traces is optimized and
components that are more essential to have short traces are accounted for. The decoupling
capacitors for the MCU are located on the opposite side of it and are connected by vias.

**Sensor Modules**: Both modules are lifted above the board using headers and because they
sit at similar heights above the board, their placement does not overlap. The decoupling
capacitors are placed near the respective pins on the MCU.

### Hardware Flaws:

**Not Space Efficient**: A few choices made the board more cluttered and more difficult to
make routes and polygons. The motor driver circuits could have made better use of the
two sided board as in the current configuration, they occupied a quarter of the board.
The oscillator would have benefitted from being a through-hole component as the soldering
pads and capacitors occupied a lot of space. In a different part of the board. There is
a lot of open space meaning there are parts of the board where there are unnecessary
bottlenecks.

**Accelerometer Placement**: The idea behind the accelerometer and wireless module not
overlapping is that since they were both lifted off the main board at a similar height,
they could not occupy the same space. However, the accelerometer lies slightly lower
than the wireless module so it can be moved closer the the MCU, allowing for shorter
traces.

**Bottlenecks**: There are some moderate bottlenecks in this design and also places where
the polygons have rather indirect routes. For example, some components rely on power
that comes gaps in the MCU which signficantly bottlenecks the polygons. The 3.3v 
needed by the wireless module comes from a couple vias and a route used as a bridge
rather than having a direct connection as it is cut off from the 3.3v polygon.

**Voltage Regulator**: The voltage regulator was small and simple but due to the exposed
pad design and its small size, was a pain to solder. This ended up being by far the
biggest hiccup in the assembly of the board and required backup components.

**Decoupling Capacitors**: The decoupling capacitors are not optimally placed in every
case but rather are placed to prevent bottlenecks. Capacitors for certain components
are placed near the MCU rather than the component itself.



