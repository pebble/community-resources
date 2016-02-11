---
name: Pebble Remind
creator: Matt Langlois
license: mit
link: https://github.com/fletchto99/pebble-remind
language: js
---

Remind is a simple library to remind your users to give your app a heart. A day after the user installs your app they will receive a timeline pin reminding them to heart your app. 

##  Setup

Ensure your application is setup to use [Pebble Timeline](http://developer.getpebble.com/guides/timeline/timeline-enabling/)

Copy the contents of `lib/reminder.js` to the top of your `pebble-app-js.js` file. In your ready event call `Reminder.remind(<app name>)`

Example:
```js
//Remind code here
Pebble.addEventListener('ready', function() {
    Reminder.remind("Demo App");
}
```