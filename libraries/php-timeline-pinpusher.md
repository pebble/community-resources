---
name: PinPusher
creator: Stephen Rees-Carter
license: mit
link: https://github.com/valorin/pinpusher
language: PHP
---

PinPusher is a simple Pebble Timeline Pin API wrapper for PHP, with full support for all of the Pebble Timeline API options. It is designed to be easy to use, and allow you to completely construct Timeline pins using PHP classes. This is beneficial to those with bad memories and/or IDEs that autocomplete. It also covers each individual layout case with the different requirements, so you don't need to guess what works where.

PinPusher is easily installable via Composer (or manually) and is framework independent. It also supports a PSR-3 compatible logger, if you need logging support. (Which is very helpful for debugging responses from the timeline API.)

## Installation

PinPusher can be installed with [composer](https://getcomposer.org/):

```bash
composer require valorin/pinpusher
```

## Examples

Here are a couple of usage examples, based on the examples in the [Pebble Timeline documentation](http://developer.getpebble.com/guides/timeline/pin-structure/).
More usage examples can be found at: <https://github.com/valorin/pinpusher>.

**Minimal Pin Example**

```json
{
  "id": "example-pin-generic-1",
  "time": "2015-03-19T18:00:00Z",
  "layout": {
    "type": "genericPin",
    "title": "News at 6 o'clock",
    "tinyIcon": "system://images/NOTIFICATION_FLAG"
  }
}
```

With PinPusher:

```php
use Valorin\PinPusher\Pusher;
use Valorin\PinPusher\Pin;

$pin = new Pin(
    'example-pin-generic-1',
    new DateTime('2015-03-19T18:00:00Z'),
    new Pin\Layout\Generic(
        "News at 6 o'clock",
        Pin\Icon::NOTIFICATION_FLAG
    )
);

$pusher = new Pusher()
$pusher->pushToUser($userToken, $pin);
```

**Complete Pin Example**

```json
{
  "id": "meeting-453923",
  "time": "2015-03-19T15:00:00Z",
  "duration": 60,
  "createNotification": {
    "layout": {
      "type": "genericNotification",
      "title": "New Item",
      "tinyIcon": "system://images/NOTIFICATION_FLAG",
      "body": "A new appointment has been added to your calendar at 4pm."
    }
  },
  "updateNotification": {
    "time": "2015-03-19T16:00:00Z",
    "layout": {
      "type": "genericNotification",
      "tinyIcon": "system://images/NOTIFICATION_FLAG",
      "title": "Reminder",
      "body": "The meeting has been rescheduled to 4pm."
    }
  },
  "layout": {
    "title": "Client Meeting",
    "type": "genericPin",
    "tinyIcon": "system://images/TIMELINE_CALENDAR",
    "body": "Meeting in Kepler at 4:00pm. Topic: discuss pizza toppings for party."
  },
  "reminders": [
    {
      "time": "2015-03-19T14:45:00Z",
      "layout": {
        "type": "genericReminder",
        "tinyIcon": "system://images/TIMELINE_CALENDAR",
        "title": "Meeting in 15 minutes"
      }
    },
    {
      "time": "2015-03-19T14:55:00Z",
      "layout": {
        "type": "genericReminder",
        "tinyIcon": "system://images/TIMELINE_CALENDAR",
        "title": "Meeting in 5 minutes"
      }
    }
  ],
  "actions": [
    {
      "title": "View Schedule",
      "type": "openWatchApp",
      "launchCode": 15
    },
    {
      "title": "Show Directions",
      "type": "openWatchApp",
      "launchCode": 22
    }
  ]
}
```

With PinPusher:

```php
use Valorin\PinPusher\Pusher;
use Valorin\PinPusher\Pin;

// Generic Layout
$layout = new Pin\Layout\Generic('Client Meeting', Pin\Icon::TIMELINE_CALENDAR);
$layout->setBody('Meeting in Kepler at 4:00pm. Topic: discuss pizza toppings for party.');

// Create Notification
$createNotification = new Pin\Notification\Generic('New Item', Pin\Icon::NOTIFICATION_FLAG);
$createNotification->setBody('A new appointment has been added to your calendar at 4pm.');

// Update Notification
$updateNotification = new Pin\Notification\Generic('Reminder', Pin\Icon::NOTIFICATION_FLAG);
$updateNotification->setTime(new DateTime('2015-03-19T16:00:00Z'))
                   ->setBody('The meeting has been rescheduled to 4pm.');

// Reminders
$reminders = [
    new Pin\Reminder\Generic(new DateTime('2015-03-19T14:45:00Z'), 'Meeting in 15 minutes', Pin\Icon::TIMELINE_CALENDAR),
    new Pin\Reminder\Generic(new DateTime('2015-03-19T14:55:00Z'), 'Meeting in 5 minutes', Pin\Icon::TIMELINE_CALENDAR),
];

// Actions
$actions = [
    new Pin\Action\OpenWatchApp('View Schedule', 15),
    new Pin\Action\OpenWatchApp('Show Directions', 22),
];

// Put it all together
$pin = new Pin('meeting-453923', new DateTime('2015-03-19T15:00:00Z'), $layout);
$pin->setDuration(60)
    ->setCreateNotification($createNotification)
    ->setUpdateNotification($updateNotification)
    ->setReminders($reminders)
    ->setActions($actions);

$pusher = new Pusher()
$pusher->pushToUser($userToken, $pin);
```
