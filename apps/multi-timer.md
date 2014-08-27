---
name: Multi Timer
creator: Matthew Tole
link: https://github.com/smallstoneapps/multi-timer
appstore: 52d30a1d19412b4d84000025
tags:
  - watchapp
  - js
  - storage
  - config
---

Multi Timer is a Pebble watchapp that allows you to run several timers and
stopwatches simultaneously.

It uses ``Persistent Storage`` on the watch to remember your timers, and even
fakes the timers running in the background by calculating how much time has
elapsed since the app was last run and adding / removing this amount of time
from any running timers.

Some parts of the C and JS code are tested, and are run automatically using
[Travis CI][1].

The current build status of the app is: [![Build Status](https://travis-ci.org/smallstoneapps/multi-timer.png?branch=master)][2]

Here is what the app looks like:

![Multi Timer Screenshot #1](http://pblweb.com/screenshots/wrap/?colour=steel_stainless&url=https://raw.githubusercontent.com/smallstoneapps/multi-timer/master/marketing/screenshots/2.7/multi-timer_2-7_01.png)

[1]: https://travis-ci.org/
[2]: https://travis-ci.org/smallstoneapps/multi-timer/