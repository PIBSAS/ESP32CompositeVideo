# ESP32CompositeVideo

This is a simple project showing how to generate a composite video signal using the ESP32

Image2Header converts image files to c++ headers
StlConverter2 converts image files to c++ headers

CompositeVideo shows how to render a 3D mesh and display it on composite.
CompositeVideoSimple shows the simple graphics functions except for 3D currently avaialable.

You need an ESP32 module connect the pin 25 to the inner pin of the yellow AV connector and ground to the outer.

Watch the project video on YouTube:
https://youtu.be/5t1_XNc3vNw

and check the project page for updates:
http://bitluni.net/esp32-composite-video

# License

CC0. Do whatever you like with the code but I will be thankfull 
if you attribute me. Keep the spirit alive :-)

- bitluni

---

# Upgrade to ESP-IDF v5.4:

## Arduino Platform:
- Upgrade to Arduino 3.2.0 based on ESP-IDF v5.4
- Board Manager -> esp32 by Espressif Systems version 3.2.0
- GitHub: https://github.com/espressif/arduino-esp32/releases

## Platformio:
- VSCode with Platformio for Espressif 32 Dev Module Version 6.10.0 based on ESP-IDF v5.4.
- Board -> Espressif 32 Dev Module
- Platform -> Espressif 32 Version 6.10.0
- GitHub: https://github.com/platformio/platform-espressif32/releases

## Example CompositeVideoSimple
### Changes on files:
 - ``CompositeGraphics.h``:
   - After line 3 add:
     ``#include <algorithm>``

   - 68 ``void print(char *str)`` -> ``void print(const char *str)`` [char -> const char].

   - 129 ``backbuffer[y][x] = min(54, color + backbuffer[y][x]);`` -> ``backbuffer[y][x] = std::min(54, color + backbuffer[y][x]);`` [min() -> std:min()].

  - ``CompositeOutput.h``:
    - After Line 2 add:
      ``#include "soc/i2s_reg.h"``

    - 166 ``.communication_format = I2S_COMM_FORMAT_I2S_MSB`` -> ``.communication_format = I2S_COMM_FORMAT_STAND_I2S`` [I2S_COMM_FORMAT_I2S_MSB -> I2S_COMM_FORMAT_STAND_I2S]

## Example CompositeVideo.
### Changes on files:
 - ``CompositeVideo.ino`` This is for PlatformIO compability.
   - After line 1 add:

     ```
     #ifdef ARDUINO
      #include <Arduino.h>
      #endif
     ````

 - ``Mesh.h``
  - After line 2 add:
    ``#include <algorithm>``

  - 68 ``const float NdotL = max(0.0f, nx * L[0] + ny * L[1] + nz * L[2]);`` -> ``const float NdotL = std::max(0.0f, nx * L[0] + ny * L[1] + nz * L[2]);`` [max() -> std::max()]

  - ``CompositeGraphics.h``:
   - After line 3 add:
     ``#include <algorithm>``

   - 68 ``void print(char *str)`` -> ``void print(const char *str)`` [char -> const char].

   - 129 ``backbuffer[y][x] = min(54, color + backbuffer[y][x]);`` -> ``backbuffer[y][x] = std::min(54, color + backbuffer[y][x]);`` [min() -> std:min()].

  - ``CompositeOutput.h``:
    - After Line 2 add:
      ``#include "soc/i2s_reg.h"``

    - 166 ``.communication_format = I2S_COMM_FORMAT_I2S_MSB`` -> ``.communication_format = I2S_COMM_FORMAT_STAND_I2S`` [I2S_COMM_FORMAT_I2S_MSB -> I2S_COMM_FORMAT_STAND_I2S]
