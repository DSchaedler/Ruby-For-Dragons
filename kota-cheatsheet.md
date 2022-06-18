---
title: Kota's Cheatsheet
desc: A sample description of the Sample Page
layout: default
published: true
indexed: false
categories: [Tutorials]
---

{% include header.html %}

_Kota_

# Basic App

```rb
def tick args
  args.outputs.solids << {
    x: 300, y:200,
    w: 30, h: 30
  }
end
```

# Primitive Types
Rendered Bottom to Top
```rb
solids
static_solids
sprites
static_sprites
primitives
static_primitives
labels
static_labels
lines
static_lines
borders
static_borders
```

## args.outputs.solids
```rb
args.outputs.solids << {
  x: x_pos, y: y_pos,
  w: width, h: height,
  r: red, g: green,
  b: blue, a: alpha
}
```

## args.outputs.sprites
```rb
args.outputs.sprites << {
  x: x, y: y, w: w, h: h, r: r, g: g, b: b, a: a,
  angle: rotation_degrees,
  source_x: x_from_image,
  source_y: y_from_image,
  source_w: w_from_image,
  source_h: h_from_image,
  flip_vertically: true_or_false,
  flip_horizontally: true_or_false,
  angle_anchor_x: 0.3, # 0 is left, 1 is right, center of rotation
  angle_anchor_y: 0.3, # 0 is left, 1 is right, center of rotation
  blendmode_enum: 0 # See Blendmode Section
}
```
