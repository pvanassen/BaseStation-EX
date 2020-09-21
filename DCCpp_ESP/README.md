What is DCC++ ESP
-----------------

DCC++ ESP is an addon to the DCC++ BaseStation that provides a WiFi <-> Serial bridge with extras.
The extra features that DCC++ ESP provides are:
* Port 2560 listener for JMRI connections
* http server providing a web based two cab throttle
* web socket listener (used by web based throttle)

Configuring DCC++ ESP
---------------------

This version of DCC++ ESP does not create it's on WiFi. Instead it connects to your existing infrastructure. To configure this, 
create a file named 'WifiSettings.h' in the src directory containing: 
```c
#ifndef STASSID
#define STASSID "network-name"
#define STAPSK  "passphrase"
#endif
```

config.h provides default values that match what is provided in DCC++ EX.

Building DCC++ ESP
------------------

The easiest way to build DCC++ ESP is to use Platform IO IDE, this will ensure the
necessary libraries are installed and everything is automated.

Building DCC++ ESP requires the following libraries:
* ArduinoOTA (https://github.com/esp8266/Arduino)
* ESP8266mDNS (https://github.com/esp8266/Arduino)
* ESP8266WiFi (https://github.com/esp8266/Arduino)
* ESPAsyncTCP (https://github.com/me-no-dev/ESPAsyncTCP)
* ESPAsyncWebServer (https://github.com/me-no-dev/ESPAsyncWebServer)
* ArduinoJson (https://github.com/bblanchon/ArduinoJson)
* TaskScheduler (https://github.com/arkhipenko/TaskScheduler)

Additionally the Arduino IDE will require ESP8266 support, see https://github.com/esp8266/Arduino
for details in setting up the additional packages for this.

Uploading DCC++ ESP to your device
----------------------------------

The Arduino IDE provides the basic support for compiling and uploading the binary, but does not
provide the support for SPIFFS upload without adding additional plugins.

The easiest way to upload this to your ESP device is to use Platform IO IDE and execute the
following commands from a terminal window in the project directory:
```shell script
platformio init
platformio run --target upload
platformio run --target uploadfs
```

This should compile and upload both the binary and SPIFFS data to the ESP device.

Wiring Arduino and your ESP device
----------------------------------

DCC++ ESP communicates with your Arduino through RS 232, via the RX/TX pins on both devices. In order to make this work, 
connect the Ardiono TX to the ESP RX and vice-versa. Also make sure both devices are connected on the ground pins

Arduino       ESP
RX      <---> TX
TX      <---> RX
GND     <---> GND

You can also connect the 5v supply of the Arduino to the 5v VIN on your ESP device, powering them both of the same 
supply. 

Lastly, if your device has an EN pin, connect this to the 3.3v line.  