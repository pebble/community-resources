---
name: Caltrain
creator: Katharine Berry
link: https://github.com/Katharine/pebble-caltrain/
appstore: 53eb5caf6743f7a863000201
tags:
  - watchapp
  - js
  - storage
---

Caltrain is a Pebble app that displays upcoming trains at a station, and where
those trains will stop along the remainder of each of their routes.

It stores the schedule locally in ``resources``, and makes heavy use of
``resource_load_byte_range`` to read in the required data without running out
of RAM. This is wrapped in a block reading API for performance reasons; without
that it takes several seconds to load each window.

It also uses ``Persistent Storage`` to store the state of the UI, so it can be
restored to the state in which you left it when you return to the app.

Finally, it uses PebbleKit JS to retrieve your location on launch. If it gets a
response before you manually choose a station, it will automatically show the
station closest to you.

The windows were built using [CloudPebble's UI Editor][ui-editor].

A python script is included to convert from the Caltrain GTFS data to the
compressed format it uses.

Screenshots:

![](http://i.imgur.com/iGGxV9q.png)
![](http://i.imgur.com/RNeaSQ1.png)
![](http://i.imgur.com/23kD7ie.png)
![](http://i.imgur.com/mHFaUMy.png)

[ui-editor]: https://developer.getpebble.com/blog/2014/08/08/CloudPebble-Graphical-UI-Editor/
