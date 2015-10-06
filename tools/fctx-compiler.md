---
name: fctx-compiler
creator: JR Mobley
link: https://github.com/jrmobley/pebble-fctx-compiler
---

Compiles SVG resources into a binary format for use with the pebble-fctx library.

Currently supports SVG font definitions.  Multiple output files can be generated
from each input.  The outputs are written to the resources directory with file
names derived from the id param of the element in the SVG.
