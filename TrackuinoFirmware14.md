# What's new #

Changes since [TrackuinoFirmware131](TrackuinoFirmware131.md):

  * NEW: Support for PIC32 / Chipkit Uno32 platform
  * NEW: Support for active or passive buzzers (DC or PWM driven)
  * NEW: Battery voltage sensing
  * NEW: Slotted transmissions for multilaunch events
  * REMOVED: Support for the MX146 radio

# Download #

Get it from the [downloads area](http://code.google.com/p/trackuino/downloads/list).

# Building #

You need Arduino IDE version **22 or 23** to compile the firmware (23 is recommended). This is important! Versions previous to 22 have a buggy serial port implementation and version 1.0+ has introduced changes that are incompatible with the current firmware. Get it from the [Arduino web site](http://arduino.cc/).

Unzip the firmware in your sketches directory and load it up by double-clicking on trackuino.pde.

The single most important configuration file is "config.h". The file is self-documented. Here is where you set up your callsign, among other things.

# Flashing #

**Important**: When flashing the Arduino, remove the Venus GPS or the entire Trackuino shield. After flashing the firmware, you can plug it back in. The GPS and the host computer share the same serial port on the AVR, so they will conflict when used together.