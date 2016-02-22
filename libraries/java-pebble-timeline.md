---
name: Java Pebble Timeline
creator: Jeroen Idserda
license: mit
link: https://github.com/idserda/java-pebble-timeline
language: Java
---

## java-pebble-timeline

This is a Java library for the Pebble Timeline API. Documentation for the full api can be found [here](https://developer.getpebble.com/guides/timeline/pin-structure/). 

### Installation

Using maven:

```
<dependency>
	<groupId>nl.palolem</groupId>
	<artifactId>pebble-timeline</artifactId>
	<version>1.1</version>
</dependency>
```

### Usage

```
Pin pin = new Pin.Builder().id("example-pin-generic-1")
				.time(new Date())
				.layout(new GenericPin.Builder()
						.title("News at 6 o'clock")
						.tinyIcon(Icon.NOTIFICATION_FLAG)
						.build())
				.build();
				
Timeline.sendPin("my-token", pin);
```

See [tests](src/test/java/nl/palolem/timeline) for more examples. 
