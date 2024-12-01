# EMS-Homematic-Integration
This project implements the communication between the Homematic smart thermostats and the Bosch boiler.
The information provided by the project can be used to understand/implement other use cases for the interaction between the Homematic devices and a boiler equipped with the EMS Bus.

# Use Cases
Using the communication I implemented the following use cases:
- put thermostats into a passive mode if the boiler is in the summer mode (i.e. no heating function) which helps to save the thermostat's battery
- switch the boiler into the boost mode if one of the thermostats is switched into the boost mode
- adjust the boiler's heating temperature to the temperature selected on the thermostats

# Overview
![Overview of the communication](Overview.svg) 
The CCU2 communicates with the thermostats over the proprietary Homematic 866 mHz protocol. 
The CCU2 is connected to the home network over the Ethernet cable.
The EMS-ESP module is connected to the home network over the WiFi.
The EMS-ESP module communicates with the boiler and its controller using the EMS Bus.
The CCU2 communicates with the EMS-ESP over the home network using the ESM-ESP's REST API.
The use cases are implemented on the CCU2 using the Homematic scripting language. 

# EMS Bus 
The EMS Bus is a proprietary hardware protocol for the communication between Bosch/Junkers/Buderus boilers an their external devices like displays or thermostats. 
It is closed source but it was reverse engineered by the community. 

# EMS-ESP module
The EMS-ESP module implements the access to the EMS Bus from the network.
It has a web based user interface to view/change the boiler setting.
But there is also a REST API to access to the settings by any other applications connected to the same network.

## Hardware
There are ready to use hardware modules sold by https://bbqkees-electronics.nl/ but I wanted to build my own one to have a better understanding how it works.

The basic circuit schematic is taken from the [Archived EMSESP8266 project](https://github.com/dimitri-rebrikov/EMS-ESP/blob/1.9.4/doc/schematics/Schematic_EMS-ESP.png).

I adapted the circuit to be supplied by the power from the VCC+ pin of the EMS power jack of the boiler.
And I used ESP32 instead of ESP8266 as the current EMS-ESP software does not support it anymore.
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
The EMS-ESP project provides ready-to-use software for the EMS-ESP module.
To user the software for the project:
1. install the software using the online install tool on https://install.emsesp.org/. The online installation will work only on the browsers supporting the serial interface (Chrome - yes, Firefox - not)

2. integrate the module into your WiFi network using explanations from https://emsesp.org/Configuring/

3. connect the module to the boiler  over the 3.5mm service jack.

4. reach the user interface of the module over browser and test if the module "sees" the boiler

5. copy the user access token from the security settings to be used later in the scripts to change for the write operations

# Thermostats
I have 2 types of thermostats:
- Homematic HM-CC-RT-DN
- Homematic IP HMIP-eTRV/2

In order to work with the project the thermostats needs to be paired with the CCU.
After the paring the status values of the thermostat can be viewed/changed over the CCU either over the user interface or by a script.

# Use Cases implementation
The user case logic is implemented as several scripts.
All scripts have following in common: They
- run on CCU
- implemented in Homematic script language
- follow the separation of concern they don't speak both sides - thermostats and boiler but only one of them. I.e. the use case involving both sides is implemented using 2 scripts.
- use the CCU system variables to store the detected state
- use the CCU system variables to read the state detected by another part of the use case
- use CCU object model to access the thermostat values
- use cURL (provided by CUxD) to access the boiler values

## Use Case "Send selected temperature to boiler"
TODO

## Use Case "Send boost to boiler"
TODO

## Use Case "Send boilers summer mode to thermostats"
TODO

# CUxD
TODO


# External Sources
 
- https://github.com/emsesp/EMS-ESP/blob/541c0c2e10b30098e26656a97a1686c8d44bc3bd/README.md
- https://github.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/blob/9a028393e1c5bedbde9ec8262f618dd6cc0af2ec/Documentation/README.md
- https://web.archive.org/web/20240222073926/https://www.kabza.de/MyHome/EMSBus/EMSbus.php
- https://docs.espressif.com/projects/esp-idf/en/v5.3.1/esp32s3/hw-reference/esp32s3/user-guide-devkitc-1.html
- https://www.debacher.de/wiki/Programmierung_bei_Homematic