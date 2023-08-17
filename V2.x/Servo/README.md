# Loco-Servo

## V2.0/V2.1a-s
The versions only differ in the pinout of the FDTI-interface.

## FTDI Interface
| V2.0     | V2.1x-s   |
|:---------|:----------|
| 1 DTS    | **1 DTS** |
| 2 **TX** | **2 RX**  |
| 3 **RX** | **3 TX**  |
| 4 3V3    | **4 3V3** |
| 5 GND    | **5 GND** |


## Servo connetor
The overall current of the servos must not exceede 4 Amps. If more power is needed, the serve +5 Volt line has to be connected to an external power line.

| #  |         | #  | 
|----|---------|----|---------|
| 1  | Servo 1 | 2  | Servo 2 |
| 3  | +5 Volt | 4  | +5 Volt |
| 5  | GNC     | 6  | GND     |
| 7  | Servo 3 | 8  | Servo 4 |
| 9  | +5 Volt | 10 | +5 Volt |
| 11 | GNC     | 12 | GND     |


## Voltage

The pins can provide absolute values reffered to GND, or relative values between two pins, depending on the module setup.

| pin | usage     |
|:----|:----------|
| 1   | Voltage 1 |
| 2   | Voltage 2 |
| 3   | Voltage 3 |
| 4   | Voltage 4 |