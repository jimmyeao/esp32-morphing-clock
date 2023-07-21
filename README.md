# esp32-morphing-clock
ESP32 HUB75 Matrix Morphing Clock

A clock based on a HUB75 RGB LED matrix, controlled by an ESP32.
Modified to run on a 63x32 Matrix!
![IMG_5742](https://github.com/jimmyeao/esp32-morphing-clock/assets/5197831/b3ed19ec-da13-48d7-839f-38b37a54365d)


So far, it does the following:
* Displays the current date, time, and day of the week
* Updates the time on startup and periodically, via NTP
* TODO Displays the current outdoor temperature and humidity (received via MQTT - if you want to use this, you will need an MQTT server and a separate temperature sensor publishing to it!)
* TODO Displays the current light levels, read via a TSL2591 I2C light sensor
* Displays the weather forecast for current day (including min/max temperatures)
* Can receive OTA updates, triggered via an MQTT message (of course, this also requires an MQTT server :) )

This is very much a work in progress, and it is far from being finished. Things that are planned for the future include:
Forked from https://github.com/bogd/esp32-morphing-clock 

You can find the "components" for the project here:
* The full source code is [here](code/)  - requires PlatformIO!
* The schematics for the PCB used is [here](pcb/)
* The drawings for the lasercut plexiglass enclosure are [here](case/)

## Changelog

### Version 0.2
* Added MQTT SSL support (thanks to [Andreas](https://github.com/lefty01)). Disabled by default, since I do not use it when testing
* Implemented weather forecast - clock now displays min/max temperature for today
* Decreased light sensor read interval (interval is now configurable from config.h)
* Added a watchdog timer to automatically reset the unit (sometimes the main thread seems to hang, possibly due to the light sensor read?)

## Thanks

This project would not have been possible without the work of many others, who have been gracious enough to open source their work. Some of the things that I have used when building this:
* The MQTT SSL code contributed by [Andreas](https://github.com/lefty01)
* The PxMatrix library from [2dom](https://github.com/2dom/PxMatrix). Even though this is NOT used in this project (I switched to the DMA library below, for performance reasons), it is the library that got me started on working with HUB75 matrices.
* The ESP32 DMA library for controlling the matrix, from [mrfaptastic](https://github.com/mrfaptastic/ESP32-HUB75-MatrixPanel-I2S-DMA)
* The morphing clock code from [HariFun](https://www.instructables.com/Morphing-Digital-Clock/) (modified to work with mrfaptastic's library instead of pxmatrix)
* The shield schematics from [hallard](https://github.com/hallard/WeMos-Matrix-Shield-DMA), which gave me the confidence to try building my own version of a shield PCB :)

And, of course, all the authors of the various open source libraries (there are already too many to mention :) ).

I also have to mention here [Brian Lough's work](https://www.tindie.com/products/brianlough/esp32-i2s-matrix-shield/) on a shield for the matrix. Even though he decided not to open source the board (he only sells the finished board on tindie), he has been extremely helpful during my initial work on the project. So if you are looking for a simple option for getting the full kit (shield and components, all in one package), take a look at [his tindie page](https://www.tindie.com/products/brianlough/esp32-matrix-shield-mini-32/) .

## License

The ESP32 HUB75 Matrix Morphing Clock is (c) [Bogdan Sass](https://github.com/bogd), licensed with GNU General Public License Version 3.0 (which means, if you use it in a product somewhere, you need to make the source and all your modifications available to the receiver of such product so that they have the freedom to adapt and improve).
