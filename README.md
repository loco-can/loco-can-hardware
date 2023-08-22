# Loco-CAN Hardware
**Current version V2.2**

The software is managed in the [Loco-CAN-Software](https://github.com/Loco-can/Loco-can-software) repository.

The Loco-CAN project is an electronic control system for the large passenger-carrying garden railway. The communication is based on the CAN bus, which is used in the automotive industry and in automation. The serial signal transmission is very robust and supports multiple masters and multiple slaves.

The modular system consists of different components with specialized tasks. For example, there are modules for operating, for controlling motor controls, light switch modules or sensors for current and voltage measurement or speed values. Actuators that are addressed by a servo module can even be used to control diesel engines or gearboxes.

Due to the flexibility of the CAN bus, additional modules can easily be connected without having to change the existing structure.

The system is not only intended for networking within a traction vehicle, but can also be routed through the train via a four-pole cable. This means that not only can control consoles be connected at any point in the train, but also, for example, lights in wagons can be operated.

The system is still under developement. The CAN-specification is defined but can be extended. Board designs are available in different versions, due to the process of evolvement. Besides bugs in the board design details like the pinout of the program interface differ between the versions.


# Version
The current development of the system is based on version 2.x. It combines the microcontroller and the CAN bus connector with the specialized function on one board. Due to the use of SMD components, the modules are significantly smaller than in old 1.x versions.

With the universal module, a version with an expansion bus is also available.

## Wired units
| Unit            | Type            |
|:----------------|:----------------|
| Processor       | Atmega 328P     |
| CAN-Controller  | MCP 2515        |
| CAN-Transceiver | MCP 2551        |

## Wireless units
| Unit            | Type            |
|:----------------|:----------------|
| Processor       | ESP32           |
| CAN-Controller  | integrated      |
| CAN-Transceiver | MCP 2551        |

# Connectors
The following connectors for the basic IOs are universal used by all modules if needed. The information includes the technical specifications for the connectors and the electrical assignment.

## CAN bus
The CAN-bus is found on all modules, even the WIFI. It connects all modules and provides both communication and supply.

**4-pin 2x2**
Plug: MATE-N-LOK 794617-4
Jack: MATE-N-LOK 3-794618-4

| pin | usage                      |
|:---:|:---------------------------|
| 1   | GND                        |
| 2   | CAN-L                      |
| 3   | CAN-H                      |
| 4   | +6-30 Volt / max. 5 Ampere |

### Loco interconnection
**4-pin Mini-XLR**
The Mate-N-LOK connectors are used for internal wiring only. 4-pin MINI-XLR connectors are used to couple vehicles together. The plugs are robust, but at the same time small enough to allow model-like housings around the plugs. The pin assignment matches the internal connectors. On the vehicle the female connectors are used.

| pin | usage                      |
|:---:|:---------------------------|
| 1   | GND                        |
| 2   | CAN-L                      |
| 3   | CAN-H                      |
| 4   | +6-30 Volt / max. 5 Ampere |

### Cables
The four-pole CAN bus cables should have a minimum cross-section of 0.34mm² in order to withstand the maximum current of five amperes.

Recommended cable: UNITRONIC® ROBUST 4x0.34 black

## Pulse
Used for speed or rpm measurement.

**2-pin horizontal**
Plug: MATE-N-LOK 2-1445055-2
Jack: MATE-N-LOK 1445022-2

| pin | usage |
|:---:|:------|
| 1   | Pulse |
| 2   | GND   |

## Power
Supply input for the Loco-system.

**2-pin vertical**
Plug: MATE-N-LOK 794617-2
Jack: MATE-N-LOK 3-794618-2

| pin | usage  |
|:---:|:-------|
| 1   | +6-30V |
| 2   | GND    |


# ICP SDI pads
To flash the bootloader on Atmega chips latter versions provide four pads to access the SDI port of the MCU and a reset signal. A jumper in the CS line between the MCU and the CAN controller has to be open for the flash process and closed for normal operation.

The hardware versions with the SDI pads before 2.2 are marked with a letter s at the end of the version string.

ICP-Interface
| pin | usage |
|:----|:------|
| 1   | SCK   |
| 2   | SI    |
| 3   | SO    |
| 4   | RST   |

# Modules
All modules, except Loco-Single, are equipped with two 4-pin CAN connectors. The following modules are available or in developement:

## Interface definitions
The pinout of the FTDI interface for flashing new software differs in the early versions. The standard pinout will be implemented in all revisions, divergent pinouts are listed with the version descriptions.

All versions are compatible on the CAN-bus, the differences are only in the expansion ports.

Standard FTDI Interface to flash software updates
| pin | usage        | cable  |
|:----|:-------------|--------|
| 1   | **1 DTS**    | yellow |
| 2   | **2 RX**     | braun  |
| 3   | **3 TX**     | white  |
| 4   | **4 3V3/5V** | green  |
| 5   | **GND**      | GND    |


# Loco-Motor
With the Loco-Motor module all types of power drivers can be controlled via the CAN bus. The setup of the motor software can be adapted to a wide variety of motor control drivers. With the additional light and horn outputs a locomotive control can be set up with a control and a motor module.

## V2.1a/V2.2
The versions mainly differ in the pinout of the FDTI-interface.

### Motor driver
Plug: MATE-N-LOK 1-794617-0
Jack: MATE-N-LOK 4-794618-0

| pin | usage       | pin | usage       |
|:----|:------------|:----|:------------|
| 1   | +bus IN     | 2   | Light       |               
| 3   | DRIVE       | 4   | HORN        |
| 5   | BREAK       | 6   | MOTOR VOLT+ |
| 7   | FORWARD     | 8   | MOTOR VOLT- |
| 9   | REVERSE     | 10  | GND         |

Pins 6 and 8 are connected to the motor output to sense the voltage. Drive and break outputs provide a PWM signal to drive the power output stage.

### FTDI Interface
| V2.1a    | V2.1b     |
|:---------|:----------|
| 1 DTS    | **1 DTS** |
| 2 **TX** | **2 RX**  |
| 3 **RX** | **3 TX**  |
| 4 3V3    | **4 3V3** |
| 5 GND    | **5 GND** |


# Loco-Switch
With the switch module different lights and other devices can be switched. Each output can drive up to 3 Ampere, when using the external +bus input with the version greater V2.1. With the V2.0 only the maximum output current of the CAN-bus can be used.

## Setup
With the base setup the module is configurated to use the light messages to set the outputs. A setup to react on every message for each output increases the flexibility. As an example four outputs can be used for different lights, one output to drive a horn and the last to activate an pantograph.

###CAN light stati
The can protocol supports eight light stati in out byte, that can be mapped to the six output lines in the module setup. To activate a status, the corresponding bit has to be set to 1.

	bits     7      6      5      4      3      2      1      0
	       	main  train   cab   instr   back    high   low   posit
	       	------------------------------------------------------
	main:	main light switch
	train:	train lights
	cab:	cabine light
	instr:	instrument light
	back:	back light
	high:	bright spot light
	low:	low spot light
	posit:	position light

A common current sensor returns the overall consumption of all outputs.

The versions differ in the pinout of the output connector and the FDTI-interface.

## Output connector
Degson DG308-2.54-08P-14-00AH
or
JST XH

## Hardware version V2.0
| pin | usage      |
|:----|:-----------|
| 1   | Output 1   |
| 2   | Output 2   |
| 3   | Output 3   |
| 4   | Output 4   |
| 5   | Output 5   |
| 6   | Output 6   |
| 7   | GND        |

## Hardware version V2.1a/V2.2
| pin | usage      |
|:----|:-----------|
| 1   | +bus       |
| 2   | Output 1   |
| 3   | Output 2   |
| 4   | Output 3   |
| 5   | Output 4   |
| 6   | Output 5   |
| 7   | Output 6   |
| 8   | GND        |

The switching module can switch up to 3 amps per output. Both resistive and inductive loads can be switched. If the current is taken from the bus, make sure that the total consumption of the system does not exceed the limit of 5 amperes.

If all outputs are operated with 3 amps, a separate supply line must be laid from the positive pole of the battery to the loads and from the negative pole of the battery to the GND connection of the switching output. The value of the maximum current must be adjusted in the configuration of the module.

### FTDI Interface
| V2.1     | V2.1a     |
|:---------|:----------|
| 1 DTS    | **1 DTS** |
| 2 **TX** | **2 RX**  |
| 3 **RX** | **3 TX**  |
| 4 3V3    | **4 3V3** |
| 5 GND    | **5 GND** |


# Loco-Single
A tiny module with only one fix wired CAN connector and one current controlled output for a single LED light. It can be used for intelligent back lights. In this case, a backlight heartbeat status can detect the train integrity.

# Loco-Sensor
The sendor module provides four voltage inputs and a current measurement up to 30 Ampere. In addition a speed/pulse input is provided.

## Hardware version V2.1/V2.1a/V2.1a-s
The versions differ in the pinout of the FDTI-interface. Both versions V2.1a and V2.1a-s offers the SDI pads.

### Voltage
The pins can provide absolute values reffered to GND, or relative values between two pins, depending on the module setup.

| pin | usage     |
|:----|:----------|
| 1   | Voltage 1 |
| 2   | Voltage 2 |
| 3   | Voltage 3 |
| 4   | Voltage 4 |

### Current
The current measurement connectors are thwo 6mm holes outside of the casing. The direction of the current is provided as positive or negative values. The ratio of the positive direction to the connection on the pins, can be set in the setup.

### Speed/pulse
See in the Connector section below.

### FTDI Interface
| V2.1     | V2.1a     |
|:---------|:----------|
| 1 DTS    | **1 DTS** |
| 2 **TX** | **2 RX**  |
| 3 **RX** | **3 TX**  |
| 4 3V3    | **4 3V3** |
| 5 GND    | **5 GND** |

## Loco-Servo
The module provides four analog model servo outputs. The power for all servos must not exceed 900mA. If more power is needed, the 5 Volt for the servo motors must be supplied by an external voltage regulator.

The values for each servo motor position can be mapped to each analog value of CAN messages. The received values are mapped using input min and max settings and output min and max values. Reverse actions are reached by setting the output mapping values in a reversed order (forward: input 0-1024 => output 100-170, reverse: input 0-1024 => output: 180-100).

### V2.0/V2.2
The versions only differ in the pinout of the FDTI-interface.

### 12-pin Servo Output
Plug: MATE-N-LOK 1-794617-2
Jack: MATE-N-LOK 4-794618-2

| Row 1     | Row 2      |
|:----------|:-----------|
| 1 Servo-1 | 7 Servo-3  |
| 2 +5V     | 8 +5V      |
| 3 GND     | 9 GND      |
| 4 Servo-2 | 10 Servo-4 |
| 5 +5V     | 11 +5V     |
| 6 GND     | 12 GND     |

### FTDI Interface
| V2.0     | V2.2  |
|:---------|:----------|
| 1 DTS    | **1 DTS** |
| 2 **TX** | **2 RX**  |
| 3 **RX** | **3 TX**  |
| 4 3V3    | **4 3V3** |
| 5 GND    | **5 GND** |

## Loco-Universal
These modules offer an unallocated connector for universal use. 

### V1.0
The first prototype board using DIL packages and JST-PH connectors for the CAN-bus. **Although this version is compatible with the system, it is no longer supported!**

**Extension bus: 10x1 pins**
| pin         | usage        |
|:------------|:-------------|
| 1  VCC      |              |
| 2  D9 (PWM) | METER_AMP    |
| 3  D8       | METER_VOLT   |
| 4  D7       | STATUS_GREEN |
| 5  D6 (PWM) | STATUS_RED   |
| 6  A0       | ANALOG_DRIVE |
| 7  A1       | MAINS_SWITCH |
| 8  A2       | DIR_SWITCH   |
| 9  A3       | LIGHT_SWITCH |
| 10 GND      |              |

### V1.2
The second prototype board using DIL packages and an bigger extension bus. It was never produced. **Although this version is compatible with the system, it is no longer supported!**

**Extension bus: 8x2 pins**
| pin         | usage             | pin         | usage              |
|:------------|:------------------|:------------|:-------------------|
| 1  VCC      |                   | 2  D2       |                    | 
| 3  A5       |                   | 4  D3 (PWM) |                    |
| 5  A4       |                   | 6  D4       |                    |
| 7  A3       |                   | 8  D5 (PWM) |                    |
| 8  A2       |                   | 10 D6 (PWM) | STATUS_RED         |
| 11 A1       |                   | 12 D7       | STATUS_GREEN       |
| 13 A0       |                   | 14 D8       | METER_VOLT (Servo) |
| 15 D9 (PWM) | METER_AMP (Servo) | 16 GND      |                    |

**big extension bus version: 9x2 pins**
| pin         | usage             | pin         | usage              |
|:------------|:------------------|:------------|:-------------------|
| 17  +bus    |                   | 18 GND      |                    | 

### FTDI Interface
Both versions provide the default FTDI pinout.
| pin | usage     |
|:----|:----------|
| 1   | **1 DTS** |
| 2   | **2 RX**  |
| 3   | **3 TX**  |
| 4   | **4 3V3** |
| 5   | **GND**   |

### V2.x
From version 2.x the universal board is pin compatible with the WIFI universal board.

| **IO 1**           | **IO 2**             |
|:-------------------|:---------------------|
| **9x1 pins**       | **5+4x1 pins**       |
| 1 +5V              | 1 +bus               |
| 2 D2               | 2 A5                 |
| 3 D3               | 3 A4                 |
| 4 D4               | 4 A3                 |
| 5 D5               | 5 A2                 |
| 6 D6               |                      |
| 7 D7               | 1 A1                 |
| 8 D8               | 2 A0                 |
| 9 GND              | 3 D9                 |
|                    | 4 GND                |

### FTDI Interface
The version provide the default FTDI pinout. To flash a new software version, pin 3 of the 5-pin IO 2 must be connected to GND before power up.

| pin | usage     |
|:----|:----------|
| 1   | **1 DTS** |
| 2   | **2 RX**  |
| 3   | **3 TX**  |
| 4   | **4 3V3** |
| 5   | **GND**   |

The +bus connection can either be used to power the CAN bus from an outside source, like a motor driver or in reverse provide an outside device with the bus supply of 6 to 30 Volts. In the different use cases the diode D2 has to be swapped regarding the printed direction for in or out on the pcb.

## Loco-WIFI (universal)
The Loco-WIFI is a universal module with two extension busses besides the two CAN connectors. It can establish a wireless connection via WIFI and Bluetooth. 

### V2.1
The ESP32 boards are shipped with a bootloader and do not need the SPI flash pads.

| **IO 1**           | **IO 2**             |
|:-------------------|:---------------------|
| **9x1 pins**       | **5+4x1 pins**       |
| 1 +3,3V            | 1 VCC (12V)          |
| 2 IO27             | 2 IO4                |
| 3 IO26             | 3 IO0 (GND to Flash) |
| 4 IO25             | 4 IO2                |
| 5 IO33             | 5 IO15               |
| 6 IO32             |                      |
| 7 IO35             | 1 IO13               |
| 8 IO34             | 2 IO12               |
| 9 GND              | 3 IO14               |
|                    | 4 GND                |

### FTDI Interface
The version provide the default FTDI pinout. To flash a new software version, pin 3 of the 5-pin IO 2 must be connected to GND before power up.

| pin | usage     |
|:----|:----------|
| 1   | **1 DTS** |
| 2   | **2 RX**  |
| 3   | **3 TX**  |
| 4   | **4 3V3** |
| 5   | **GND**   |


# Loco-Control-Adapter
The controller module provides connectors to apply pots, switches, leds and meters in an easy way to implement an own controller design.

The analog switch inputs use a potentiometer or a switch with applied resistors to change the voltage on the analog input. The software can learn the distinct positions and map them to discrete switch positions.

The connectors for volt and ampere display provide either an analog value (PWM) or a model servo signal. The servo can be used to build a analog gauge for display.

The control module consists of an universal module providing CAN-bus connectors and an optional wireless connection (Loco-Universal, LOCO_WiFi), that is piggipacket on a adapter board. The adapter creates a +5 Volt supply for all controls from the CAN-supply lines and offers JST-PH connectors for the switches, pots and LEDs.

## Hardware version V2.x

### Power out
The 5-Volt supply output can be used to supply additional electronic inside the controler with up to 500mA.

### DRIVE / BREAK / POWER
Three pot inputs for drive, break and power regulators.
**3-pin JST-PH connectors**
| DRIVE    | BREAK    | POWER    |
|:---------|:---------|:---------|
| 1	GND	   | 1 GND    | 1 GND	 |
| 2	POT    | 2 POT    | 2 SWITCH |
| 3 VCC	   | 3 VCC    | 3 VCC    |

### DIR / MAINS
Two analog switch inputs for direction and mains.
**3-pin JST-PH connectors**
| DIR      | MAINS    |
|:---------|:---------|
| 1	GND	   | 1 GND    |
| 2	POT    | 2 POT    |
| 3 VCC	   | 3 VCC    |

### V-BATT / V-MOT / AMP
Three servo/analog outputs for analog meters. The output type is either a model servo or a pwm signal.
**3-pin JST-PH connectors**
| BATTERY  | MOTOR    | AMPERE   |
|:---------|:---------|:---------|
| 1	OUT    | 1 OUT    | 1 OUT    |
| 2 VCC	   | 2 VCC    | 1 VCC    |
| 3	GND	   | 3 GND    | 1 GND    |

### STATUS
The dual color LED (green/red with common GND) is conneted to this port.
**3-pin JST-PH connectors**
| pin | usage |
|:----|:------|
| 1   | red   |
| 2   | GND   |
| 3   | green |

### INST
The instrument light output provides a +5V/+12 Volt supply for lighting the instruments. It is powered by the CAN-bus line and therefore can only use the maximum of 5 Ampere. The FET-ouput is designet to switch this current, but it is recommended to use LEDs with much less power consumption, especially when the WiFi controller is powered by a battery.
To select the voltage a connection between the voltage and the center off instsupent light jumper has to be soldered regarding the text on the pcb.

**3-pin JST-PH connectors**
| pin | usage      |
|:----|:-----------|
| 1   | +5V/+bus   |
| 2   | Lights     |
| 3   | GND        |

### SIGNAL
The signal connector has two inputs for a high/low horn operation. Setting both inputs to low, activates the bell function.
**3-pin JST-PH connectors**
| pin | usage |
|:----|:------|
| 1   | high  |
| 2   | low   |
| 3   | GND   |


# Power Supply

The Modules are connected with 4-pin cables using MICRO MATE-N-LOK connectors. The cables have a supply line with a voltage of +6 up to +30 Volts. The supply can be provided through some modules, that have got supply connectors (vertical 2-pin MICRO MATE-N-LOK connector). The motor module supplies directly from the motor driver.

All supply connectors have a diode, so the input voltages on places in the network can be different. The supply voltage on the bus will be the highest value. The operation voltage for internal function of the modules is created onboard.

So it is possible to connect two locomotives with 12 Volt and 24 Volt batteries without any problem. All connected units have a common GND level. When using the CAN-supply for LED-lights, it is important to have the big voltage range in mind. Best is to use a current regulator for the LEDs.

**It is not recommended to use the CAN-Connector for supply of the bus.**


## Loco-Split
The splitbox is a tiny module that split up the CAN-bus line with three connectors. It also provides a power input connector for additional supply of the bus.

For details ot the connector pinouts see the connector section below.

**Power for the system has to be provided via a motor module or the splitboxes. It is not recommended to use the CAN connector for this purpose!**


## Loco-train
**not yet designed**
The train device connects an vehicle intern bus with the train interconnecting plugs. To enshure safe operation, the Loco-train has a built in current limmiter to 5 Amperes as well as a over current shutdown. An additional puwer input can be used, to enshure the full 5 Amps to the train.


## Loco-Power
**not yet designed**
A power box with an integrated battery that is charged from the CAN bus supply. It can i.e. be used to power a speedometer without any other module.


# Cases
The cases for all modules are collected in the mechanics directory of the repository. Cases only exist in the Version 2 and above. There are both a STL version and the Fusion 360 file.

Most modules use the standard baseplate and differ only in the cover design. The housing for the control adapter consists of three parts, the controller base plate, an intermediate frame and the cover for the universal module.


# Deprecated Hardware Versions

## V1.2
Version 1.2 is similar in concept to version 1.0, but has a 16 or 18 pin expansion bus with more connections for the adapters.

The version is software compatible, but uses a 5 Volt supply on the CAN bus connector and is therefore not directly electrically compatible with version 2.0. 

It will not be further developed.

## V1.0
The first version is based on a control unit with a microcontroller and a CAN bus connector and a 10-pin extension bus to which the respective adapters are plugged.

The version is software compatible, but uses a 5 Volt supply on the CAN bus connector and is therefore not directly electrically compatible with version 2.0. 

It will not be furt
