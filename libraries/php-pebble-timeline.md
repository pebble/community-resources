---
name: PHPebbleTimeline
creator: Matt Langlois
license: mit
link: https://github.com/fletchto99/PHPebbleTimeline
language: PHP
---

PHPebbleTimeline is a library for making use the Timeline API through PHP.

##  Setup

Copy the TimelineAPI Folder to your project's directory and include the required files.

## Documentation

See https://github.com/fletchto99/PHPebbleTimeline/blob/master/Readme.md for indepth documentation regarding the API.

## Sample

```php
//Include the timeline API
require_once 'TimelineAPI/Timeline.php';

//Import the required classes
use TimelineAPI\Pin;
use TimelineAPI\PinLayout;
use TimelineAPI\PinLayoutType;
use TimelineAPI\PinIcon;
use TimelineAPI\PinReminder;
use TimelineAPI\Timeline;

//Create some layouts which our pin will use
$reminderlayout = new PinLayout(PinLayoutType::GENERIC_REMINDER, 'Sample reminder!', null, null, null, PinIcon::NOTIFICATION_FLAG);
$pinlayout = new PinLayout(PinLayoutType::GENERIC_PIN, 'Our title', null, null, null, PinIcon::NOTIFICATION_FLAG);

//Create a reminder which our pin will push before the event
$reminder = new PinReminder($reminderlayout, (new DateTime('now')) -> add(new DateInterval('PT10M')));

//Create the pin
$pin = new Pin('<YOUR USER TOKEN HERE>', (new DateTime('now')) -> add(new DateInterval('PT5M')), $pinlayout);

//Attach the reminder
$pin -> addReminder($reminder);

//Push the pin to the timeline
Timeline::pushPin('sample-userToken', $pin);
```
