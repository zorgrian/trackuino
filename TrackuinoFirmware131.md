# What's new #

Changes since 1.3:

  * FIX: Altitude 16-bit rollover

# Download #

Get it from the [downloads area](http://code.google.com/p/trackuino/downloads/list).

There are two versions of the 1.31 firmware:

  * trackuino-ide-1.31 can be compiled and uploaded from the Arduino IDE and is the recommended download.
  * trackuino-gcc-1.31 if you're comfortable with command line tools. This package contains the Makefiles needed to compile with the gcc-avr toolchain on Linux and Mac OS X.


# Building #

You need Arduino IDE version **22 or 23** to compile the firmware (23 is recommended). This is important! Versions previous to 22 have a buggy serial port implementation and version 1.0+ has introduced changes that are incompatible with the current firmware. Get it from the [Arduino web site](http://arduino.cc/).

Unzip the firmware in your sketches directory and load it up by double-clicking on trackuino.pde.

The single most important configuration file is "config.h". The file is self-documented. Here is where you set up your callsign, among other things.

**Important**: When flashing the Arduino, remove the Venus GPS or the entire Trackuino shield. After flashing the firmware, you can plug it back in. The GPS and the host computer share the same serial port on the AVR, so they will conflict when used together.