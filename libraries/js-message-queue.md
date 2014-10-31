---
name: JS Message Queue
creator: Matthew Tole
license: mit
link: https://github.com/smallstoneapps/js-message-queue/
language: js
---

PebbleKitJS library for sending messages to your Pebble app.

##  Advantages

Automatically retries sending messages when they fail, and ensures that messages
are sent in order (i.e. wait for first message to be acknowledged before
sending the second message.

## Usage

1. Include js-message-queue.min.js in your application's JS file, either by copying
and pasting it into the top of `pebble-js-app.js`, or by adding it to your
JS build script.
2. Replace all instances of `Pebble.sendAppMessage()` with
`MessageQueue.sendAppMessage()`.
3. Profit!