||
|:|

# Using _Windows Balloon Track_ #

Windows Balloon Track or [WBALTRAK](http://www.eoss.org/wbaltrak/index.html) is a program developed by Rick von Glahn (NØKKZ), a member of the EOSS team.

This piece of software is incredibly useful in assisting the recovery of payloads. It basically has two modes of operation: it can run landing predictions based on recent winds data obtained from a nearby weather station, but most importantly, it can use the **actual** winds data gathered during the ascent of the balloon to predict the descent leg.

The program crashes often and it's a bit hard to get the hang of it, but its usefulness outweighs the stability issues. I recommend reading their on-line documentation and perusing the PDF manual, but here is a brief tutorial describing the basic workflow:

## Obtaining wind data ##

You want to start getting the latest winds data from a nearby station. There are [different sources](http://www.eoss.org/wbaltrak/import_overview.htm), and you can get both [past data](http://weather.uwyo.edu/upperair/sounding.html) or up to [240 hours forecasts](http://www.stormchaser.niu.edu/machine/textfcstsound.html). For the purposes of this tutorial, I'm using the most recent data from station 08430 (Murcia, Spain):

![http://trackuino.googlecode.com/svn/wiki/img/uwyo4.png](http://trackuino.googlecode.com/svn/wiki/img/uwyo4.png)

These stations launch 2 sounding ballons per day (at 0000Z and 1200Z) and sample the wind speeds along with other useful information from the upper layers of the atmosphere. The results are made available through that page, and this is what we'll use to run our predictions. Just copy all the tabulated data into a notepad and save it as a text file.

![http://trackuino.googlecode.com/svn/wiki/img/uwyo5.png](http://trackuino.googlecode.com/svn/wiki/img/uwyo5.png)

## Setting up WBALTRAK ##

First, [download](http://www.eoss.org/wbaltrak/download.htm) the latest version of WBALTRAK and install it.

**Important**: download the beta executable, too. Go to your program files folder, and overwrite the executable with the one from the beta archive. The beta contains numerous bug fixes, so this is really important.

Fire up WBALTRAK, we need to give it some information about our flight before we can start running predictions. On the "Setup" menu, go to the "Flight Info" tab and enter the following data:

  * Metric/Imperial: I switched this to metric, since I'm more familiar with it. This affects almost every magnitude shown by or given to the program, so it's important to set it right in the first place.
  * Flight Name: this will appear in various printouts and log files.
  * Flight Radio Callsign: the callsign of your balloon. I put N0KKZ-3 (one of EOSS's balloons), since they have a [log of their flight on-line](http://www.eoss.org/wbaltrak/aprs_demo.txt), and I'll be simulating it later.
  * Vertical rates: the expected ascent/descent rates in meters per minute (metric) or feet per minute (imperial). The descent level given is at sea level.
  * Burst altitude: the altitude at which the balloon is expected to pop. This is useful in prredicting the ascent/descent trajectories.

All in all, the screen should look like this:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrak1.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrak1.png)

Next, go to the "Location" tab. Fill out the "Launch Site Data". Coordinates are given in decimal degrees (ie. 40.47367). North and East are positive, south and west are negative.

Also, fill out the expected altitude of the landing site. Predictions will assume the payload will land at this altitude. Again, I used the values from the demo N0KKZ-3 launch:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrak2.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrak2.png)

Lastly, go to the "Mapping" tab, click on "Mapping options", then "Internet Map Site URLs", and fill this out under "First mapping service":

  * Google
  * http://maps.google.com/maps?q=BTLAT,BTLON&spn=1,1&hl=en

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrak6.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrak6.png)

Later on, we can have the program automatically launch a google map and pinpoint the predicted landing coordinates on it.

That is really it. On the "Folders/Files" tab you can set various directories to help keep things organized. By default, everything is stored in the "Balloon Track" directory under "Program Files".

## Feeding the winds data to WBALTRAK ##

Once we have everything set-up, it's time to run a prediction based on the winds data file. From WBALTRAK, click on the "File" menu, then "Open". Locate the text file you saved earlier and load it up.

The program will show a simulation of the trajectory of the balloon based on the launch site coordinates, burst altitude, landing altitude, vertical rates and the winds data we just loaded:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrak3.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrak3.png)

Now, my background looks red indicating there is not enough wind data to simulate the ascent up to the requested burst point. When that happens, the program simply makes the missing data up, so do not expect the simulation to be too accurate. If you see a red background, try to get winds data from another station and see if it covers the higher altitudes. If you have enough data up to the burst altitude, the background should be GREEN.

If you scroll down, the last line shows the landing data, this is the most important piece of information here. You can now map the coordinates, check that the landing spot is not in the middle of the sea, a swamp or something really inaccesible and call it a go / no go:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrak4.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrak4.png)

If you click on "Inet mapping", then "Google", a google map like this will show up:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrak5.jpg](http://trackuino.googlecode.com/svn/wiki/img/wbaltrak5.jpg)

## Running predictions with real-time data ##

Predictions based on past or forecast data are useful in choosing the best day for a launch and provide a more or less approximate area of landing. But one of the biggest strengths of WBALTRAK is being able to use **real-time** wind data gathered during the flight.

As the balloon climbs, the flight data takes precedence over the winds file data, and predictions will be run up to highest altitude so far. Since the balloon hasn't popped yet, this is not very useful.

However, after the balloon pops, the payload starts its descent. The program will use the real burst altitude now, and the flight data will completely override the winds file data. When we run a prediction during the descent, the program will use the last known coordinates and start the simulation from there on. As the payload approaches ground, predictions will become more and more accurate, to the point that the rescue team shouldn't expect much of a variation between the predicted and the actual landing spots.

To start real-time analysis, click on "Packet Data", then "Packet Terminal". The "Target Callsign" is already filled out for us, but we can change it by entering a different one in the "Manual Target Entry" box:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrak7.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrak7.png)

At this point, you can choose to either capture real-time data from a TNC, or run a simulation from a log file. The behavior in simulation mode is every bit as identical to the real-time mode. That means you can bring logs from another packet terminal, aprs.fi or an APRS-IS server and run predictions as if the data were captured by WBALTRAK itself.

## Starting the analysis ##

**IMPORTANT**: when starting a new simulation or real-time capture, we need to delete all the previous analysis data. Go to the "View Files" menu, then "Flight Data". At the new window, click "Delete Data". The screen should look like this:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrak8.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrak8.png)

Now, press the "Flight Analysis" button. It will ask you to "Clear the Data File", click yes. Then, a new window will pop up. This is the flight analysis window and it provides a host of useful in-flight data: altitude, bearing, range and multiple plots of the vertical rates, speed, track, course and altitude are shown here. It is the single most important window in the program and at least one person in the recovery team should never look away from it:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrak9.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrak9.png)

Ok, time to run our simulation. I'm going to use [this log from the EOSS team](http://www.eoss.org/wbaltrak/aprs_demo.txt). Click on "File", then "Open simulation", then open up your log file. [The formats accepted by WBALTRAK are described here](http://www.eoss.org/wbaltrak/importgpsaprs.htm).

A new window will appear with controls to pause, resume, speed up or slow down the simulation:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltraka.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltraka.png)

As the program parses the log file, you can see new lines coming up in the packet terminal window:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrakb.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrakb.png)

Check the flight analysis window, the new data is being plotted real-time:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrakc.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrakc.png)

After the balloon pops, it's time to run predictions. From the Packet Terminal, click on "Realtime Predict", and check out the main window:

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrakd.png](http://trackuino.googlecode.com/svn/wiki/img/wbaltrakd.png)

A few things happened here: the wind data file has been replaced by the flight winds' data recorded so far. The highest recorded altitude (92748 feet) is assumed to be the burst point. The program notes the last reported coordinates and takes up predicting from there. The last line, again, gives the landing information. In this example, the payload is expected to end up 67.3 Km, 85º from the launch site, at 40.5238N, 104.1685W. If you click on "Inet Mapping", then "Google", a Google map will point at the coordinates.

You're probably wondering how accurate that prediction is. Well, I did a [quick check](http://www.movable-type.co.uk/scripts/latlong.html), since this is a simulation of a past flight I already know that the balloon landed at 40.5205N, 104.1348W. That's about 2.9 Km or 1.8 miles off! As the total expected range is 67.3 Km, I wouldn't say the error is bad at all!

![http://trackuino.googlecode.com/svn/wiki/img/wbaltrake.jpg](http://trackuino.googlecode.com/svn/wiki/img/wbaltrake.jpg)

As the payload falls from the sky, you can keep running predictions constantly. At the packet terminal, click on "Restore Config". That will restore the winds file back to the main window. Then click on "Realtime Predict" again to run another prediction based on the latest data.

For example, another prediction at 24629 feet, gives an estimation of 40.5275N, 104.1604W, or 2.3 Km (1.4 miles) off.

## Some additional notes ##

### Using Microsoft MapPoint to plot landing predictions ###

With the advent of 3G and mobile tethering, it's possible to get on-line in the middle of nowhere. That will give you the ability to plot Google maps while on the field.

However, if your connection fails, you need to resort to some off-line mapping system. WBALTRAK has the ability use MapPoint to plot landing predictions. However, I haven't had much success with it (I'm using version 2010). This issue can be minimized by carrying a GPS that allows setting a pair of latitude/longitude coordinates as the destination point and letting it drive you there.