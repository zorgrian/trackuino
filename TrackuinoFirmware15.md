# What's new #

Changes since [TrackuinoFirmware14](TrackuinoFirmware14.md):

  * FIX: Allow compilation on Arduino 1.0+
  * FIX: Added pre-emphasis flag, makes the signal more intelligible
  * FIX: Revamped modem code to avoid ISR overruns
  * FIX: improve baudrate accuracy

# Download #

Get it from the [downloads area](https://code.google.com/p/trackuino/wiki/Downloads?tm=2).

# Building #

If you are building for the Arduino platform you need Arduino IDE version 0023 or higher (tested with versions 0023 and 1.0.5). Get it from the [Arduino web site](http://arduino.cc/).

If you are building for the Chipkit Uno32 you need the Mpide IDE. Tested with 0023-20130715. Get it from the [Chipkit site](http://chipkit.net/).

Unzip the firmware in your sketches directory and load it up by double-clicking on trackuino.pde.

The single most important configuration file is "config.h". The file is self-documented. Here is where you set up your callsign, among other things.

# Flashing #

**Important**: When flashing the Arduino/Uno32, remove the Venus GPS or the entire Trackuino shield. After flashing the firmware, you can plug it back in. The GPS and the host computer share the same serial port on the AVR, so they will conflict when used together.