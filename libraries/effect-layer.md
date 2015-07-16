---
name: EffectLayer
creator: Yuriy Galanter, Ron64, Eric Arrigo, Grégoire Sage, mikalgow, Colin, Martin Norland
license: mit
link: https://github.com/ygalanter/EffectLayer
language: c
---

EffectLayer is a visual effect layer for Pebble Smartwatch. User places the layer over screen at set coordinates and special effects are applied to that area of the screen. Effects work both on Aplite/Classic Pebble and Basalt/Pebble time unless specified (e.g. Blur works only on Basalt)

To use the library place the source files in your SRC directory and add #include "effect_layer.h" to your source. EffectLayer library is implemented in efficient pay-to-play way so only effects that you actually use get compiled into your binary.

Currently supported effects:
<ul>
<li>Invert</li>
<li>Invert b/w only</li>
<li>Invert brightness, preserve hue</li>
<li>Vertical Mirror</li>
<li>Horizontal Mirror</li>
<li>Rotate 90 degrees (counter- or clock-wise)</li>
<li>Blur</li>
<li>Zoom</li>
<li>Lens</li>
<li>Mask</li>
<li>FPS</li>
<li>Shadow</li>
<li>Outline</li>
<li>effect_colorize</li>
<li>effect_colorswap</li>
</ul>

![Inverter](http://i.imgur.com/6t9r3qa.gif "Inverter")
![Bitmap Mask](http://i.imgur.com/JspSsx1.gif "Bitmap Mask")
![Text Mask](http://i.imgur.com/EdKu49w.png "Text Mask")





