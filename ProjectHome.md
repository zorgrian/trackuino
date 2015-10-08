# Moved to Github #

<font color='red'><b>Due to Google Code <a href='http://google-opensource.blogspot.jp/2015/03/farewell-to-google-code.html'>closing down</a>, I have moved the project to <a href='https://github.com/trackuino/trackuino'>Github</a>. See you there!</b></font>

# Overview #

This is an APRS tracker shield for the Arduino platform. It features on-board GPS and radio transmitter, so the only external components required are the GPS and VHF antennas. It was designed primarily to track high altitude balloons, so it has other handy features like reading temperature sensors and a buzzer for acoustic location.

Trackuino is intended for use by licensed radio amateurs. By operating on the standard APRS frequency, the signal can be picked up by an Internet gateway and reported on [aprs.fi](http://aprs.fi), so anyone with an Internet connection can track the flight live and even help with the chase!

The project comprises both the firmware and the schematics/PCB to build your own shield. All the code and schematic designs are open software/hardware, and licensed under GPL v2.

This is how a finished board looks like:

![http://wiki.trackuino.googlecode.com/hg/img/trackuino-2.2-640px.jpg](http://wiki.trackuino.googlecode.com/hg/img/trackuino-2.2-640px.jpg)

# Main features #

  * Arduino shield form factor (you can stack more shields on it)
  * GPS: Venus 638FLPx. Reports okay above 18 Km.
  * Radio: Radiometrix's HX1 (300 mW).
  * 1200 bauds AFSK using 8-bit PWM
  * Sends out standard APRS position messages (latitude, longitude, altitude, course, speed and time).
  * Internal/external temperature sensors (LM60) to read temperature in and outside the payload
  * Active/passive buzzer support to ease acoustic payload location.
  * 2 x SMA female plugs (1 x GPS in + 1 x radio out)
  * Open source (GPLv2 license), both software and hardware. In other words, do whatever you want with it: modify it, add it to your project, etc. as long as you opensource your modifications as well.

# Documentation #

Click on the [wiki](http://code.google.com/p/trackuino/wiki/Index) link to get started.

# Support #

Discuss firmware bugs, suggestions or ask for help at the [hab-ham.org forum](http://hab-ham.org/forum/).

# More information #

For the nitty-gritty, check out the [wiki](http://code.google.com/p/trackuino/wiki/Index?tm=6).

You can also follow us and stay up-to-date at the [project's blog](http://trackuino.blogspot.com).