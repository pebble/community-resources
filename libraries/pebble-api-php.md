---
name: Pebble API PHP
creator: David Moreau
license: mit
link: https://github.com/dav-m85/pebble-api-php/
language: php
---

Library for interacting with Pebble Timeline Pin from a server running php.

**Work In Progress**, this project is currently under development, basic features are already functional. Feel free to contribute.

##  Advantages

Tested, object-oriented, leveraging Guzzle.

## Usage

```bash
php composer.phar require dav-m85/pebble-api-php:dev-master
```

```php
$client = new PebbleApi\Client();

// Create (or update) a pin
$pin = new PebbleApi\Pin("reservation-1395203", array(
	"id" => "reservation-1395203",
    "time" => "2014-03-07T09:01:10.229Z",
    "layout" => array(
    	...
    )
));
$user = new PebbleApi\User($userToken);
$client->put($user, $pin);

// Delete a pin
$client->delete($user, $pin);

// Create a pin for all users (shared pin)
$sharedTopic = new PebbleApi\SharedTopic($apiToken, array('baseball', 'giants'));

$client->put($sharedTopic, $pin);

```
