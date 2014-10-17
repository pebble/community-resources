---
name: ToastLayer Library
creator: Chris Lewis
link: https://github.com/C-D-Lewis/ToastLayer/
language: c
---

## Description

ToastLayer UI element for showing a time-limited notification within your app.
Use just like a normal `Layer`, such as `TextLayer` or `MenuLayer`.

## Instructions

1. Copy `ToastLayer.c` and `ToastLayer.h` into your project's `src` directory.
2. Include in your C file with `#include "ToastLayer.h"`
3. Create a ToastLayer with `toast_layer_create()`.
4. Pop up the toast notification when desired with `toast_layer_show()`.
5. The toast will slide out of view when the duration has elapsed. Use
   `toast_layer_hide()` to hide early.