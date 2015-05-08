---
name: Sliding Text Layer
creator: Matthew Tole
link: https://github.com/smallstoneapps/sliding-text-layer/
language: c
---

# Sliding Text Layer

A Layer for your Pebble apps that lets you vertically scroll a line of text.

![](http://zippy.gfycat.com/TenderSecondhandDromedary.gif)

## Usage

1. Add sliding-text-layer.h and sliding-text-layer.c to your src folder.
2. Include sliding-text-layer.h in your code.

    ```
    #include "sliding-text-layer.h"
    ```
3. Create a new SlidingTextLayer.

    ```
    SlidingTextLayer* stl = sliding_text_layer_create(GRect(0, 60, 144, 24));
    ```
4. Set the initial text for the layer.

    ```
    sliding_text_layer_set_text(stl, "Line 1");
    ```
5. When you want to animate to the next line of text.

    ```
    sliding_text_layer_set_next_text(stl, "Line 2");
    sliding_text_layer_animate_down(stl);
    ```
