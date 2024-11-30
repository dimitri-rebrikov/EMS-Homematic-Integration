# EMS-Homematic-Integration
This project implements the communication between the Homematic Smart Thermostats and the Bosch Boiler.
The information provided by the project can be used to understand/implement general communication between the Homematic devices and a Boiler equipped with the EMS Bus.

# Use Cases
Using the communication I implemented following use cases:
- put thermostats into a passive mode if the boiler is in the summer mode (i.e. no heating function) which helps to save the thermostat's battery
- switch the boiler into the boost mode if one of the thermostats is switched into the boost mode
- adjust the boiler's heating temperature to the temperature selected on the thermostats

# Overview
![Overview of the communication](Overview.svg) 
The CCU2 communicates with Thermostats over the proprietary Homematic 866 mHz protocol. 
The CCU2 is connected to the home network over the Ethernet cable.
The EMS-ESP is connected to the home network over the WiFi.
The EMS-ESP communicates with the Boiler and its Controller using the EMS Bus.
The CCU2 communicates with the EMS-ESP over the home network using the ESM-ESP's REST API. 

# EMS Bus 
The EMS Bus is a proprietary hardware protocol for the communication between Bosch/Junkers/Buderus Boilers an their external devices like displays or thermostats. 
It is closed source but it was reverse engineered by the community and implemented by several project. 

# EMS-ESP
The EMS-ESP implements the access to the EMS Bus from the network.
It has a web based user interface to view/change the boiler setting.
But there is also a REST API to view/change the settings by any other applications connected to the same network.

## Hardware
There are ready to use hardware modules sold by https://bbqkees-electronics.nl/ but I wanted to build my own one to have a better understanding how the it works.

The basic circuit schematic is taken from the [Archived EMSESP8266 project](https://github.com/dimitri-rebrikov/EMS-ESP/blob/1.9.4/doc/schematics/Schematic_EMS-ESP.png).

I adapted the circuit to be supplied by the power from the VCC+ pin of the EMS Power Jack of the Boiler.
And I used ESP32 instead of ESP8266 as the current EMS-ESP Software does not support it anymore.
Here is the circuit diagram with the adaptions:
![Adapted Circuit](./CircuitDiagram.svg)

I also used slightly different hardware parts, see the [BOM](https://html-preview.github.io/?url=https://github.com/dimitri-rebrikov/EMS-Homematic-Integration/blob/main/BOM.xhtml) file.

During the implementation I split the circuit into 3 hardware modules: 

![Modules](./CircuitModules.svg)

I implemented each module on a separate board of the same size and then stacked them together using the brass distance sleeves respective thick soldering wires. 
Then I put the assembly into a standard electronic distribution box:

<p float="left">
  <img src="./PictStackedBoards1.jpg" width="32%" />
  <img src="./PictStackedBoards2.jpg" width="32%" /> 
  <img src="./PictBox.jpg" width="32%" />
</p>

## Software
The EMSESP project provides ready-to-use software for the module.

First - install the software using the online install tool on https://install.emsesp.org/. The online installation will work only on the browsers supporting the serial interface (Chrome - yes, Firefox - not)

Second - integrate the module into your WiFi network using explanations from https://emsesp.org/Configuring/

# Homematic

(Under construction)

# External Sources
 
- https://github.com/emsesp/EMS-ESP/blob/541c0c2e10b30098e26656a97a1686c8d44bc3bd/README.md
- https://github.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/blob/9a028393e1c5bedbde9ec8262f618dd6cc0af2ec/Documentation/README.md
- https://web.archive.org/web/20240222073926/https://www.kabza.de/MyHome/EMSBus/EMSbus.php
- https://docs.espressif.com/projects/esp-idf/en/v5.3.1/esp32s3/hw-reference/esp32s3/user-guide-devkitc-1.html