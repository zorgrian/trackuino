# Building the tracker #

<font color='red'><b>This version is no longer supported due to the Venus GPS being phased out. The following information is kept as a reference for existing trackers.</b></font>

Both the schematic and PCB Eagle files are in the [downloads section](http://code.google.com/p/trackuino/downloads/list). You can do the exposure/development/etching process yourself, but I suggest sending it to a PCB house. I made the project public at BatchPCB, so anyone can [go and order one](http://batchpcb.com/index.php/Products/50481).

The Trackuino is designed to work with two different radios: [Radiometrix HX1](http://www.radiometrix.com/content/hx1) and [Argentdata MX146 8v](https://www.argentdata.com/catalog/product_info.php?products_id=81). I suggest you build the HX1 version, since it's cheaper and it involves less components.

Here is the bill of materials:

  * For the [HX1 version](https://spreadsheets.google.com/pub?key=0AqW-6zh51rr8dGNDVUZXV2l1Y2NOU2pZaElrcFUycXc&single=true&gid=0&output=html).
  * And for the [MX146 version](https://spreadsheets.google.com/pub?key=0AqW-6zh51rr8dGNDVUZXV2l1Y2NOU2pZaElrcFUycXc&single=true&gid=1&output=html).

# Building the firmware #

The recommended firmware version is [TrackuinoFirmware131](TrackuinoFirmware131.md). Refer to that page for downloading and building directions.

# How to program #

The easiest way is uploading the firmware to an Arduino, then moving the AVR chip to the Trackuino board.

The board has an ICSP header, so you can also use an ICSP programmer to flash the AVR on-board. Refer to [ProgrammingTheDevice](ProgrammingTheDevice.md) for more information.