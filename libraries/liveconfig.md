---
name: Liveconfig
creator: Matt Langlois
license: mit
link: https://liveconfig.fletchto99.com
language: JS & HTML
---

Liveconfig is an easy to use library to have your configuration page settings be reflected realtime on the user's watch.

##  Setup

There are 2 parts to the setup of this library. First download the latest release from: https://liveconfig.fletchto99.com/releases. 

### Updating your configuration page

Include the script `/web/liveconfig.js` in your configuration page, and then add the class `liveconfig` to any inputs that you wish to be updated in realtime.

### Updating your app

Require the script `/watchapp/liveconfig.js` in your watchapp/watchface using `var liveconfig = require('liveconfig.js');`. In your In your `showConfiguration` event listener before you make the call `Pebble.openURL` call `liveconfig.connect(<uuid>, onChange(<id>, <value>)`. This will connect to the liveconfig server and call your onchange callback any time a value is updated. Lastly, you must prepare your URL for liveconfig on the web. To do this call `var prepared_url = liveconfig.prepareURL(<uuid>, <config_page_url>)` followed by `Pebble.openURL(prepared_url)`. That's all you have to do, now all configuration inputs will be sent in near realtime to your onChange callback!

## Code Example

For a more complete code example please see https://liveconfig.fletchto99.com/example

## Demo

[Example app in Appstore](https://apps.getpebble.com/applications/56bed5490ed2a75acd000040)

[![Video](http://img.youtube.com/vi/6cuWw52ojV4/0.jpg)](http://www.youtube.com/watch?v=6cuWw52ojV4)