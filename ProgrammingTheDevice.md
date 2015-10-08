# Overview #

After you have the firmware configured to your needs, it's time to upload it to the Atmega chip. The Trackuino board has an ICSP header, so it can be programmed with standard ICSP programmers. This is a compilation of links to pages I've found useful explaining how to program an in-system chip.

## Using an Arduino ##

The simplest option is to upload your firmware into an Arduino board from the IDE. Then, remove the chip and plug it into Trackuino. That will only work if you have the Arduino bootloader pre-loaded on the Atmega328p chip.

If you bought a blank AVR, you can burn the bootloader first, and then flash any firmware into it as you would normally do from the IDE. But you don't really have to, since you can flash the Trackuino firmware directly into it. In either case, you need an ICSP programmer:

## ICSP programmers ##

The Trackuino board has a 6-pin header interface that you can use to burn the firmware into the microcontroller chip with an ICSP programmer and the "avr-dude" tool.

| **Warning:** when programming, the trackuino needs to be powered externally. Powering Trackuino from the ICSP's Vcc pin is not a good idea, because, 1st) it may draw more current than the programmer is able to source, and 2nd) reverse powering the regulators may damage them. Commercial programmers will take care of this, but pay special attention if you're making your own DIY ICSP, and make sure you don't wire the Vcc pin between a programmer and the target board! |
|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

There are a few alternatives:

### USBasp programmer ###

There are [USBasp](http://www.fischl.de/usbasp/) programmers on [dealextreme](http://dx.com/s/isp+programmer) for as little as $5.

### The AVRISP mkII programmer ###

[![](http://store.atmel.com/di.ashx/10520172/150/150?avr.jpg)](http://www.atmel.com/dyn/products/tools_card.asp?tool_id=3808)

This is [Atmel's standard ICSP programmer](http://www.atmel.com/dyn/products/tools_card.asp?tool_id=3808). [Digikey also carries it](http://search.digikey.com/scripts/DkSearch/dksus.dll?Detail&name=ATAVRISP2-ND). It might be kind of expensive if you're only going to use it once or twice, but this device is otherwise good to have. You can erase/flash/verify chips directly from AVR Studio or through the "avr-dude" command-line tool. The Arduino IDE, however, does not support it as far as I know.


### Using and Arduino to emulate an AVRISP programmer ###

[![](http://farm3.static.flickr.com/2630/3718355976_c162f494af_t.jpg)](http://hackaday.com/2009/07/15/avr-isp-programming-via-arduino/)

If you have an Arduino lying around, you can turn it into an AVRISP compatible programmer without cashing out the extra $30 for the actual device.

You need to flash the [mega-isp firmware](http://code.google.com/p/mega-isp/) into the Arduino. Then, wire the Arduino pins yourself according to the docs, or use [this shield](http://drug123.org.ua/mega-isp-shield/), which provides a nice break-out of the needed ICSP pins.

### Sparkfun's AVR Pocket Programmer ###

[![](http://dlnmh9ip6v2uc.cloudfront.net/images/products/09825-01b_i_ma.jpg)](http://www.sparkfun.com/products/9825)

It's slightly cheaper than Atmel's AVRISP mkII, but read the comments as some people reported problems on OSes other than Windows: http://www.sparkfun.com/products/9825

### Using the FT232 chip on Diecimilas and Duemilanoves ###

[![](http://farm4.static.flickr.com/3286/2754610329_6f61016593_m.jpg)](http://www.geocities.co.jp/arduino_diecimila/bootloader/index_en.html)

On the Diecimila and Duemilanove versions of the Arduino there is an empty header near the FT232 chip that you can use to bitbang an ICSP interface using an especially modified version of avr-dude. It's very easy and it can be done with just a few jumper wires. We need to remove the AVR chip from the Arduino, then connect MISO, MOSI, SCK, /RESET and GND from the AVR-less Arduino to Trackuino:

![http://trackuino.googlecode.com/svn/wiki/img/trackuino-icsp.png](http://trackuino.googlecode.com/svn/wiki/img/trackuino-icsp.png)

Remember we have to power the board externally and not from the ICSP, since the GPS and the radio transmitter will definitely draw more power than the USB port can handle. So, we left Vcc purposedly out of the diagram.

Then, follow the instructions here:

http://www.geocities.co.jp/arduino_diecimila/bootloader/index_en.html

### The AVR Dragon ###

This is the [mother of all Atmel programers](http://www.atmel.com/dyn/products/tools_card.asp?tool_id=3891). It not only works as an ICSP programmer, but also as a [debugger](http://support.atmel.no/knowledgebase/avrstudiohelp/mergedProjects/AVRDragon/AVRDragon.htm#AVRDragon_connecting_to_target_through_the_debugwire_interface.htm) via Atmel's proprietary DebugWire interface. It's the ultimate, yet priciest programmer of all.