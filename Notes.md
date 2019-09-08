# BrewPiLEsSP32

BrewPiLEsSP32 is an attempt to port the BrewPiLess fermentation controller from ESP8266 hardware to ESP32 hardware. ESP32 has bluetooth capability which will allow it to interface with the Tilt digital hydrometer. Integration of the Tilt Hydrometer was the main motivation for this.

The goals of this project are first to get the baseline project working on the ESP32 hardware and then to add Tilt Hydrometer integration.  Provided the port is successful, a PR will be initiated to merge it back into the BrewPiLess source. 

The purpose of this file is to collect notes and list notable issues.

## Hardware differences and compatibility.

ESP32 and ESP8266 have some notable differences:
 - ESP32 has more GPIO pins (Hooray!). This makes it relatively straightforward to use the PIO inline debugger and the ESP-Prog JTAG hardware debugger. Pins 12-15 are used for JTAG debugging, so conflicting pins in `config.h` will need to be changed if you want to do inline debugging.
 - A few libraries are different between the ESP32 and ESP8266, notably the WiFi libraries, SPIFFS libraries and ASyncTCP. Much of the code effort is ensuring the correct libraries are included before compile and managing the small differences between each.
 - EEPROM: ESP32 does not have actual EEPROM, but a deprecated library is available which *should* mean that we can use the existing code with little modification.  (ESP8266 also emulates EEPROM).
 - PROGMEM keyword is not required on ESP32, only defined for compatibility with other hardware. any const will be stored to flash by default. 

## Current Issues:
- WiFi scan is buggy and seems to work sporadically. Serial debug information indicates that a list of available access points is being generated successfully, however these are not being propogated to the browser on the config page. A browser request to the "/wifiscan" path returns an empty "{}".  Need to ivestigate browser request/response cycle. Issue may reside within the HTML code/javascript or even the Async webserver implementation.
- Device settings page is not working correctly. Need to check EEPROM related code first. If that doesn't fix, then a deeper dive will be required.

## Future ToDos:
- Get Tilt Hydrometer functioning. See TiltBridge implementation for inspiration.
- Replace deprecated EEPROM implementation with the Preferences library for ESP32.
- Code cleanup.

## Thoughts:
The BrewPiLess (and subsequently this) codebase could greatly benefit from a general cleanup as well as an overall refactor. It is a port of the BrewPi code and several of the files have either been changed/patched or deprecated entirely. Technical debt is starting to show itself. That's not a dig to the BrewPiLess author(s), but rather just the nature of these sorts of things. A non-trivial amount of mental real estate (especially for idiots like me) is required to parse how everything fits together. The main file `brewpiless.cpp` is almost 2000 LOC by itself. Some code cleanup and refactor would help onboard new developers. A big task either way.