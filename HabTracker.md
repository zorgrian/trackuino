# Introduction #

HAB Tracker is an application for Android mobile devices to aid in tracking and predicting the trajectory of high altitude balloons. The basic features are:

  * Flight path plotting on a map (similarly to http://aprs.fi).
  * Flight simulation based on current/forecast sounding data from NOAA (helps in making go/no-go calls prior to the launch date)
  * Real-time update of the trajectory and touchdown predictions based on real-time atmosphere conditions learned during the flight.
  * One-click directions to the landing site
  * APRS packet monitor

# Operation #

## Download and installation ##

HAB Tracker should work on Android 2.1+ and requires Google's Maps app.

Download the app from the [downloads area](http://code.google.com/p/trackuino/downloads/list). You will have to allow unsigned applications when prompted so.

## Set up ##

After launching the app, a map will show up. You can pan around or use the +/- buttons to zoom in and out:

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker01.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker01.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|

Before anything else, we need to configure a few things such as the callsign of the balloon and the estimated flight parameters (vertical rates, launch altitude and burst altitude). Press MENU, then Settings:

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker02.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker02.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|

The options under the "APRS" section are:

  * **Callsign**: your balloon's callsign and SSID (usually -11).
  * **APRS-Log server**: this is the server where APRS-IS data will be collected from.
  * **APRS poll interval**: this is how often the app will query the APRS server to check for new packets. Set it to a value just below your tracker's beacon interval. Higher values will be easier on your 3G data plan.
  * **Launch date/time**: set this to a time just before the launch. Packets before this time will be ignored. This is useful if your tracker has been reporting test data on the hours previous to the launch and you don't want the prediction engine to get confused with test position data.
  * **Connect**: turn this on when you are ready to track the balloon. Note: you will need a wifi/3G connection for the app to be able to connect to the APRS-Log server.
  * **Unit system**: In a future, you will be able to choose between international metric or british imperial. For now, only metric units are supported.
  * **Ascent rate**: The estimated ascent rate in meters/minute. It is important to set this right to get valid predictions. You can reset this value during the flight to better reflect the actual ascent speed and predictions will be recalculated accordingly.
  * **Descent rate**: The estimated descent speed at **sea level**. This depends on the parachute and the payload weight.
  * **Burst altitude**: The estimated burst altitude. This is useful when running predictions based on sounding data from NOAA. Note that NOAA provides sounding data only up to ~26 Km, so any value above this will be capped to ~26 Km. Under this scenario, simulations based on NOAA data will be run only up to the highest sounded altitude and the prediction engine will undershoot the touchdown point.
  * **Launch altitude**: The launch point altitude.

Here is a sample config to track a balloon with callsign KJ6KUV-11. It will poll the APRS server for new packets every 30 seconds. The estimated ascent rate is 350 meters/min, descent rate will be 250 m/min. We are targeting at 30 Km burst altitude (even though predictions will probably be capped to the highest NOAA sounding, around ~26 Km), and the launch site is 200 meters high:

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker03.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker03.png)|![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker04.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker04.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|

## Running flight simulations ##

In order to run a flight simulation we need to get sounding data from NOAA first. Sounding data varies with location, so find your launch site on the map, and long-press on it. Then, touch "Get sounding winds":

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker05.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker05.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|

Choose the prediction model. Currently only GFS models are supported. Other models (RUC, etc.) will probably not work, so stick to GFS. There are two different GFS models, one will give you 3-hourly forecasts within the next 192 hours, and the other will give you 12-hourly forecasts within the next 192-384 hours:

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker06.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker06.png)|![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker07.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker07.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|

Now, choose the forecast cycle. This is the time at which sounding data was gathered. Forecasts are based on this particular set of data:

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker08.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker08.png)|![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker09.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker09.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|

Next, choose the launch time. The first item (+00 Hrs) will use the actual sounding data, so it will produce a simulation of how your ballon would have behaved if launched at that time. The remaining items will give you more or less accurate forecasts according to the chosen model:

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker10.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker10.png)|![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker11.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker11.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|

Now, it seems the NOAA service has been abused in the past, so they will force you to answer a CAPTCHA in order to get the sounding data. Just enter the letters (case is indifferent) on the box below:

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker12.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker12.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|

If everything works right, you'll see the estimated trajectory displayed on the map: if the NOAA "window" doesn't close automatically, something went wrong and you will have to start over. The green "target" shows the launch point, and the red target shows the predicted touchdown point.

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker13.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker13.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|

## Real-time tracking and predictions ##

When you are ready to launch the balloon, go again to the settings and set the launch time. Any position data reported before the launch date (such as test packets or bogus positions) will be ignored so that the prediction engine doesn't get confused. Touch "Connect" to connect to the APRS network.

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker14.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker14.png)|![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker15.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker15.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|

As soon as the ballon starts flying, position data will be displayed on the map. The blue dots mean the actual trajectory, with yellow points representing the estimated trajectory until landing. Between the dots, you will see either a green line or a red line. Green means ascent, red means descent. The estimated touchdown point will be displayed as a red "target":

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker16.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker16.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|

At any given point, you can view the raw APRS packets by touching on MENU, then "Packet monitor":

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker17.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker17.png)|![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker18.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker18.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|

The prediction engine uses a combination of NOAA sounding winds as well as in-flight data reported by the balloon itself. When available, the latter will override the former. Predictions are run constantly as new packets arrive, so, the estimated and actual touchdown points will end up converging. Theoretically, as the flight progresses, the estimations will get more and more reliable.

At any given time, you can go back to the settings and adjust the vertical rates to better reflect the actual behavior of the balloon. It is important to set these values right for the predictions to be minimally useful.

# Accuracy of predictions #

There is no such thing as an accurate prediction of a balloon trajectory.

That said, the following two screenshots are from a real flight. The one on the left was taken shortly after burst (burst occurs when the green line turns red, near the "w" of Twin Lakes). The remaining of the flight (or an estimate of it) is shown in yellow. On the right, you can see the **actual** path followed by the balloon and was taken moments before landing. It turns out that the prediction was about right!

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker19.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker19.png)|![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker20.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker20.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|

## Getting directions to the touchdown site ##

At any time, you can get directions to the landing site by clicking MENU, then "Navigate to landing". That will fire up Google Navigation with the destination preset at the landing coordinates.

> |![http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker22.png](http://trackuino.googlecode.com/svn/wiki/img/habtracker/habtracker22.png)|
|:----------------------------------------------------------------------------------------------------------------------------------------------------|

## Disclaimer and feedback ##

This app is in a very early beta stage. It may crash, lead you in the opposite direction or drive you down a cliff. It hasn't even been used on a real launch yet (the pictures above are actually a reenactment of a past flight). It is more or less a proof of concept and is yet to be determined if the predictions produced by the program are useful at all.

Feedback is **seriously** welcome. Discussion about this app will happen at: http://hab-ham.org/forum/index.php