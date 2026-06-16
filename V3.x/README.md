For# Version 3.x
*in early development state*

The new version 3.x marks the switch from the Atmega MCUs to the ESP32 series from the Chinese manufacturer Espressif. In addition to integrated Bluetooth and WiFi functionality, the CAN controller is also already built in, making the modules even smaller.

The first module is a complete 4-quadrant motor driver for 80 amps motor current, which can be operated directly on the CAN bus.

Version 3.x is fully compatible with all other versions.

## ESP32-PICO-V3-02

For all small modules the PICO-V3-02 will be used. It is based on the ESP32 core with internal flash, ram and the CAN controller in a package with only 7x7mm of size. Only the CAN transceiver is needed in addition. 

For wireless communication an antenna has to be developed. In this case it may be simpler to use a full ESP32 WROOM like on the motor driver project.