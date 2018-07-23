# AnarduinoMiniWireless-TTN-Getting-Started
A guide to connecting the Anarduino MiniWireless (US915) to The Things Network using OTAA

## Intro
The Anarduino MiniWireless LoRa board consists of an ATMEGA328p microcontroller connected to a HopeRF RFM95 LoRa radio module. This tutorial is for the **US915** band. Other bands will not work using these instructions, the differences are significant.
The IBM LMIC framework is an Arduino port of the LoRaWAN-in-C framework provided by IBM.

### Software
* Install the IBM LMIC framework for Arduino.
* Modify the library directly so that it will work in the US915 band and with our specific radio.
* To the config of the example sketch, modify the Device EUI, Application EUI and Application Key parameters taken from The Things Network registration.
* To the config of the example sketch, modify the pin mapping specifically for the Anarduino.
### Hardware
* Solder 3 jumpers to enable the MiniWireless to function as a LoRaWAN node using LMIC.
---
### Install the IBM LMIC framework for Arduino
In the Arduino IDE Library Manager select and install **IBM LMIC framework by IBM Version 1.5.0+arduino-2**
![Library Screenshot](https://github.com/bborncr/AnarduinoMiniWireless-TTN-Getting-Started/blob/master/images/lmic-library.PNG)
### Library Modifications
These modifications must be done directly in the installed library.
The following files to modifiy will be relative to **Arduino-->libraries-->IBM_LMIC_framework**.
#### Change the SPI Clock Frequency
* Navigate and edit `src-->hal-->hal.cpp`
* Locate the line SPISettings and set to the following `static const SPISettings settings(8E6, MSBFIRST, SPI_MODE0);`
The only change is the constant from `10E6` to `8E6`
#### Set the frequency band and radio type
* Navigate and edit `src-->lmic-->config.h`.
* Ensure that the US915 band is selected and the EU868 band is commented out:
```
//#define CFG_eu868 1
#define CFG_us915 1
```


