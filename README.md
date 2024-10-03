# EMS-Homematic-Integration
Connect a Boiler with the EMS Bus to the Homematic Home Automation System



# Idea
The idea is to connect the Homematic Thermostats to the Boiler for the following functions:
- disable thermostats if the boiler is in the summer mode (i.e. no heating function)
- switch the boiler into the boost mode if one of the thermostats is switched into the boost mode

# Implementation (Under Construction)

## Hardware
The basic circuit schematic is taken from the [Archived EMSESP8266 project](https://github.com/dimitri-rebrikov/EMS-ESP/blob/1.9.4/doc/schematics/Schematic_EMS-ESP.png).

The parts I used for the circuit are in the [BOM](https://html-preview.github.io/?url=https://github.com/dimitri-rebrikov/EMS-Homematic-Integration/blob/main/BOM.xhtml) file.

The overview of the circuit assembly: 


![Assembly](./AssemblyCircuit.svg)

# External Sources
 
Those are the external information sources I used:
- https://github.com/emsesp/EMS-ESP/blob/541c0c2e10b30098e26656a97a1686c8d44bc3bd/README.md
- https://github.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/blob/9a028393e1c5bedbde9ec8262f618dd6cc0af2ec/Documentation/README.md
- https://web.archive.org/web/20240222073926/https://www.kabza.de/MyHome/EMSBus/EMSbus.php