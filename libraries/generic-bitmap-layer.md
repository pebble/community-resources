---
name: GenericBitmapLayer
creator: Grégoire Sage
license: mit
link: https://github.com/gregoiresage/generic_bitmap_layer
language: c
---

# Generic Bitmap Layer Library

Just give a resource_id to this layer, it will detect automatically the type of the resource and it will display it correctly.
Supported resource types are : PNG / APNG / PDCI / PDCS

# Usage

Create and destroy your layer with `generic_bitmap_layer_create` and `generic_bitmap_layer_destroy` like every pebble XXX_layer.

Set the resource of your layer with `generic_bitmap_layer_set_resource(GenericBitmapLayer* gbl, uint32_t resource_id)`. You can change the resource dynamically, your layer will be updated.
