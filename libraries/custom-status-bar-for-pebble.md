---
name: Custom Status Bar for Pebble
creator: Jonathan LaRocque (Reboot's Ramblings)
license: mit
link: https://github.com/rebootsramblings/custom-status-bar-for-pebble
language: c
---

A plug and play custom status bar implementation for pebble apps and watch faces. Easily populate 3 text layers and/or 5 bitmap layers.

Use:

Choose a status bar height and icon size. Icons should be square with a maximum of 28 pixels.
```c
#define BAR_HEIGHT 20

#define ICON_WIDTH_HEIGHT 15
```

Declare
`c
static CustomStatusBarLayer *custom_status_bar;
`

Create
`c
custom_status_bar = custom_status_bar_layer_create(BAR_HEIGHT, GColorBlack, ICON_WIDTH_HEIGHT);
`

Set Text and Icons

Text layers, use positions CSB_TEXT_LEFT, CSB_TEXT_RIGHT, CSB_TEXT_CENTER
```c
char *t = ...;

custom_status_bar_layer_set_text(custom_status_bar, CSB_TEXT_LEFT, t);
```

Icons, use positions CSB_ICON_0 to CSB_ICON_4 (positions are left to right, 0 indexed)
`c
custom_status_bar_layer_set_bitmap(custom_status_bar, CSB_ICON_4, your_gbitmap); 
`

When you're done, destroy
`c
custom_status_bar_layer_destroy(custom_status_bar);
`

One last note! Your window should have a height of 168 - BAR_HEIGHT.

See the header file for more details. Enjoy!

![](http://rebootsramblings.ca/forumpictures/icons.png "Icons")

![](http://rebootsramblings.ca/forumpictures/textlayers.png "Text")
