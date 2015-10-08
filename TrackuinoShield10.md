# What's new #

Changes since [TrackuinoStandAlone10](TrackuinoStandAlone10.md):

  * This is a reduced version of the previous board, contributed by Kyle Crockett. As opposed to the stand-alone version, this a daughter board (shield) that plugs on Arduinos.
  * MX146 support has been removed

# Building the tracker #

<font color='red'><b>This version is no longer supported due to the Venus GPS being phased out. The following information is kept as a reference for existing trackers.</b></font>

Download trackuino-shield-1.0.zip from the [downloads area](http://code.google.com/p/trackuino/downloads/list).

The bill of materials needs to be figured out from the eagle files, sorry about that.

# Building the firmware #

The recommended firmware version is trackuino-fiwmare-1.31.zip. Download it from the [downloads area](http://code.google.com/p/trackuino/downloads/list).

You need Arduino IDE version **22 or 23** to compile the firmware (23 is recommended). This is important! Versions previous to 22 have a buggy serial port implementation and version 1.0+ has introduced changes that are incompatible with the current firmware. Get it from the [Arduino web site](http://arduino.cc/).

The single most important configuration file is "config.h". The file is self-documented. Here is where you set up your callsign, among other things.

**Important**: When flashing the Arduino, remove the Venus GPS or the entire Trackuino shield. After flashing the firmware, you can plug it back in. The GPS and the host computer share the same serial port on the AVR, so they will conflict when used together.

# Testing #

Refer to [Troubleshooting](Troubleshooting.md) if something doesn't work the way it should.