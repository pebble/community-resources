---
name: PebbleTimeline API Ruby
creator: Salim Hbeiliny
license: mit
link: https://github.com/salimhb/pebble_timeline
language: ruby
---

A Ruby wrapper for the Pebble Timeline API

This is currently a work in progress and contributions are welcome. It currently offers the ability to push/delete/update shared pins or user pins.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'pebble_timeline'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install pebble_timeline

## Usage

```
require 'pebble_timeline'

api = PebbleTimeline::API.new(ENV['PEBBLE_TIMELINE_API_KEY'])

# Shared pins
pins = PebbleTimeline::Pins.new(api)
pins.create(id: "test-1", topics: 'test', time: "2015-06-10T08:01:10.229Z", layout: { type: 'genericPin', title: 'test 1' })
pins.delete("test-1")

# User pins
user_pins = PebbleTimeline::Pins.new(api, 'user', USER_TOKEN)
user_pins.create(id: "test-1", time: "2015-06-12T16:42:00Z", layout: { type: 'genericPin', title: 'test 1' })
user_pins.delete("test-1")
```
