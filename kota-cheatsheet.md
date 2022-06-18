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
  angle_anchor_x: 0.3, # 0 = left, 1 = right, center of rotation
  angle_anchor_y: 0.3, # 0 = left, 1 = right, center of rotation
  blendmode_enum: 0 # See blendmode section
}
```

## args.outputs.primitives
This example is for a `solid` primitive. Other types include

```rb
:solid
:sprite
:label
:line
:border
```

```rb
args.outputs.primitives << {
  x: x_pos, y: y_pos,
  w: width, h: height,
  r: red, g: green,
  b: blue, a: alpha,
  primitive_marker: :solid
}
```

## args.outputs.labels
```rb
args.outputs.labels << {
  x: x, y: y, r: r, g: g, b: b, a: a,
  alignment_enum: 0, # 0 = left, 1 = center, 2 = right, horizontal alignment
  vertical_alignment_enum: 0, # 0 = top, 1 = center, 2 = bottom
  font: 'font.ttf', # path to font file
  size_enum: 0 # less than 0 is smaller, more than 0 is larger
}
```

## args.outputs.lines
```rb
args.outputs.lines << {
  x: 0, y: 0, # point 1 coordinates
  w: 100, h: 100, # relative coordinates
  x2: 100, y2: 100, # point 2 coordinates
  r: r, g: g, b: b, a: a,
  x3: 200, y3: 200, # define a triangle
  source_x2: x_from_image, source_y2: y_from_image, # triangle image fill
  source_x3: x_from_image, source_y3: y_from_image
}
```

## args.outputs.borders
Same arguments as `solids`.
```rb
args.outputs.borders << {
  x: x_pos, y: y_pos,
  w: width, h: height,
  r: red, g: green,
  b: blue, a: alpha
}
```
