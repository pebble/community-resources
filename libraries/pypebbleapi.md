---
name: pypebbleapi
creator: Alessio Bogon
license: mit
link: https://github.com/youtux/pypebbleapi
language: python
---

Python library to interact with the Pebble Timeline APIs. It supports Python 2.7, 3.3 and 3.4.

This is basically a port of the [pebble-api](https://www.npmjs.com/package/pebble-api) library for NodeJS.

## Installation
Just use `pip`:

    pip install pypebbleapi

## Usage
This snippet shows the basic usage:

```python
from pypebbleapi import Timeline, Pin
import datetime

timeline = Timeline(my_api_key)

my_pin = Pin(id='123', datetime.date.today().isoformat())

timeline.send_shared_pin(['a_topic', 'another_topic'], my_pin)
```
