brewpi.cpp mostly deprecated in favor of brewpiless.cpp

HTML JS folder is template for html files, then minified and converted to HEX to be stored in flash memory.

PROGMEM is not required on ESP32, only included for compatibility. any const will be stored to flash by default.

AsyncTCP is required for ESP32 and is the basis for ESPAsyncWebServer.

sntp not used for ESP32 i think...

ESP32 uses SPIFFS.h ESP8266 uses FS.h for same

TimeKeeper -> BPLSettings -> BrewLogger -> BrewPiProxy

BPLSettigs *DONE
BrewLogger * DONE *

BrewPiProxy:  DONE
    "VirtualSerial.h"  * Done.  No changes
    "Brewpi.h"
    "PiLink.h"
    "Version.h"
    "TemperatureFormats.h"
    "TempControl.h"
    "Display.h"
    "JsonKeys.h"
    "Ticks.h"
    "Brewpi.h"
    "EepromManager.h"
    "EepromFormat.h"
    "SettingsManager.h"
    "Buzzer.h"
    "Display.h"

    BrewPi:    (Note some weird define in brewpi.h on esp32 branch??)  * DONE*
        "ConfigDefault"  * Done - Add ESP322 def.
        "Actuator" * Done - No changes
            "FastDigitalPin.h" * Done - No changes
        "Brewpi.h" * Done - Add ESP32 board def.  Add Typedef for uint32
        "Ticks.h"  * DOne - No Changes
        "Display.h"
            "DisplayBase.h" *DONE
                "TemperatureFormats.h"
            "DisplayLcd.h" * DONE
                "BrewpiStrings.h"  *Spidey Sense....   *Done for now*
                "IicLCD.h" * Done. replace uint32 with uint32_t
                "IicOledLcd.h" * Done - not used currently. replace uint32 with uint32_t
                "Display.h" *  DONE
                "Menu.h" * DONE
                    "Pins.h"
                    "Display.h"
                    "TempControl.h"
                    "TemperatureFormats.h"
                    "RotaryEncoder.h"
                    "PiLink.h"
                "TempControl.h" *DONE
                    "Pins.h" * DONE
                    "PiLink.h" - DONE might need more attention to ESP8266 statements
                        "DeviceManager.h"  Done
                            "TempSensor.h" *DONE
                                "FilterCascaded.h" * DONE
                                    "FilterFixed.h" * DONE
                                "TempSensorBasic.h" * DONE
                            "OneWireDevices.h" * DONE
                                "DallasTemperature.h" * DONE
                                    "EepromManager.h" * DONE
                                        "EepromAccess.h" * DONE
                                            "EepromTyes.h" *DONE
                                            "ESPEepromAccess.h"  *DONE Maybe some magic is here...
                                                "Logger.h" * Done
                                                    "LogMessages.h" * DONE
                                                    "JsonKeys.h" * DONE
                                        "EePromFormat.h" * DONE
                                        "ActuatorAutoOff.h" * Done
                            "TempSensorDisconnected.h" * DONE
                            "TempSensorExternal.h" * DONE
                            "AutoCapControl.h" * DONE
                                "Mystrlib"  * Done ??? What is this bullshit??
                            "ParasiteTempController.h" * Done
                            "OneWireTempSensor.h"  * DONE
                            "OneWireActuator.h" * DONE 
                            "DS2413.h" * DONE
                            "ActuatorArduinoPin.h" * Done
                            "SensorArduinoPin.h" * DONE But contains error
                            "TempSensorWireless.h" * Done
                        "Version.h" * DONE
                        "SettingsManager.h" * DONE
                        "Buzzer.h" * DONE
                    "TempSensorMock.h" *DONE*
                    "RotaryEncoder.h" *DONE
                "TemperatureFormats.h" *DONE*
                    "TempControl.h"
                "Pins.h" DONE
                "NullLcdDriver.h" * Done -  replace uint32 with uint32_t
        "TempControl.h"
        "PiLink.h"
        "Menu.h"
        "Pins.h"
        "RotaryEncoder.h"
        "Buzzer.h"
        "TempSensor.h"
        "TempSensorMock.h"
        "TempSensorExternal.h"
        "Ticks.h"


DataLogger > Logformatter

ESPUpdateServer might need some love on line 43 & 292