---
name: Resistor Time
creator: Ben Combee
license: mit
link: https://github.com/unwiredben/resistor-time
language: c
appstore: 55561ff444dad6e1470000df
tags:
  - watchface
  - js
  - config
  - storage
  - messaging
---
This shows the current time as a resistor with the color code matching the time of day in 24-hour time.

Configuration is done through a static HTML page hosted on github pages and some PebbleKit JS code that handles
communication with the configuration page.

This only works on the Basalt color platform, as there's no point trying to show color codes on a black and white watch.
