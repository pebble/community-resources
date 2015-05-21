---
name: Color Selector
creator: Jason Brand
license: mit
link: https://github.com/jas-b/color_select_lib/
language: c
---

##Description
This library opens a seperate window for color selections.
Useful for converting existing apps to color.

##Usage

#### 1. Add color_sel_lib.h and color_sel_lib.c to your Pebble project.
```c
#include "color_sel_lib.h"
```
#### 2. Define a handler to use the selected color:
```c
void handle_CS_close(int color_argb) {
  GColor color = (GColor){.argb = color_argb};
  // Do something
  
  // or use directly
  text_layer_set_background_color(text_layer_name, (GColor){.argb = color_argb});
}
```
#### 3. Create the window and show it:
```c
CSWindow * myCSWindow = cswindow_create(
  default_color, false, 
  (CSCloseHandler)handle_CS_close);

cswindow_show(myCSWindow, true);
```

|Parameter|Description|
|---|---|
|**default_color**|The default color that the window will try to match.|
|**full_palette**|true to use all 64 color, false to use a subset of 11 main colors. The user can switch between the two palettes by holding the select button.|
|**closeHandler**|The CSCloseHandler to fire when the keyboard closes.|
