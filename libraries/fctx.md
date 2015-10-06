---
name: fctx
creator: JR Mobley
license: mit
link: https://github.com/jrmobley/pebble-fctx
language: c
---

Subpixel accurate, anti-aliased rendering of filled shapes and text.

The library complements the built-in rendering functions,
providing quality rendering above and beyond the faster rendering available in the SDK.
Even though the library is fast and efficient, it is doing quite a lot of work
and is not meant for animations.

The library also supports the aplite platform, which can benefit from the sub-pixel
coordinates and accuracy for rendering of small, detailed shapes.
Anti-aliasing is only available on the basalt platform.

The supported drawing primitives are straight line segments, cubic spline (bezier) segments,
and circles.

Text rendering is built on top of the primitive operations, and supports
scaling and rotation of text.

![Demo](http://jrmobley.github.io/pebble-fctx-demo/images/fctx-demo-aa.gif)

Also see the [fctx-demo](https://github.com/jrmobley/pebble-fctx-demo) app and the [fctx-compiler](https://github.com/jrmobley/pebble-fctx-compiler) tool.
