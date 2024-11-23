# EMS-Homematic-Integration
This projec is about to connect a Boiler equiped with the EMS Bus to the Homematic Home Automation System

# Idea
The idea is to implement the following use cases:
- disable thermostats if the boiler is in the summer mode (i.e. no heating function) which helps to save the thermostat's battery
- switch the boiler into the boost mode if one of the thermostats is switched into the boost mode and vise versa
- adjust the boiler's heating temperature to the max temperature selected on the thermostats

# Implementation

## Hardware
There are ready to use hardware modules selled by https://bbqkees-electronics.nl/ but I wanted to build my own one to have a better understanding how the electronic communication works.

The basic circuit schematic is taken from the [Archived EMSESP8266 project](https://github.com/dimitri-rebrikov/EMS-ESP/blob/1.9.4/doc/schematics/Schematic_EMS-ESP.png).

I adapted the circuit to be power supplied from the VCC+ of the EMS Power Jack of my Boiler and used ESP32 instead of ESP8266 as the EMS-ESP Software does not support it anymore.
Here is the circutit with the adaptions:
![Adapted Circuit](./CircuitDiagram.svg)

I also used slightly different hardware parts, see the [BOM](https://html-preview.github.io/?url=https://github.com/dimitri-rebrikov/EMS-Homematic-Integration/blob/main/BOM.xhtml) file.

During the implementation I splitted the circuit into 3 hardware modules: 

![Modules](./CircuitModules.svg)

I implemented each module on a separate board of the same size and then stacked them together using the brass distance sleeves respective thick soldering wires:

![StackedBoards](./PictStackedBoards1.jpg)

![StackedBoards](./PictStackedBoards2.jpg)

Then I put the boars into a standard electronic distribution box:

![Box](./PictBox.jpg)


## Software

### EMS-ESP Software for the ESP32 S3 N16R8 module
First - install the software using the online install tool on https://install.emsesp.org/. The online installation will work only on the browsers supporting the serial interface (Chrome - yes, Firefox - not)

Second - integrate the module into your WiFi network using explanations from https://emsesp.org/Configuring/

### Homematic Sortware

(Under construction)

# External Sources
 
Those are the external information sources I used:
- https://github.com/emsesp/EMS-ESP/blob/541c0c2e10b30098e26656a97a1686c8d44bc3bd/README.md
- https://github.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/blob/9a028393e1c5bedbde9ec8262f618dd6cc0af2ec/Documentation/README.md
- https://web.archive.org/web/20240222073926/https://www.kabza.de/MyHome/EMSBus/EMSbus.php
- https://docs.espressif.com/projects/esp-idf/en/v5.3.1/esp32s3/hw-reference/esp32s3/user-guide-devkitc-1.html