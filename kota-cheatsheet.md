---
title: Kota's Cheatsheet
desc: A sample description of the Sample Page
layout: default
published: true
indexed: true
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
  path: 'sprites/circle/red.png', # path to the source image
  angle: rotation_degrees,
  source_x: x_from_image,
  source_y: y_from_image,
  source_w: w_from_image,
  source_h: h_from_image,
  flip_vertically: true_or_false,
  flip_horizontally: true_or_false,
  angle_anchor_x: 0.3, # 0 = left, 1 = right, center of rotation
  angle_anchor_y: 0.3, # 0 = left, 1 = right, center of rotation
  blendmode_enum: 0 # see blendmode section
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

## Render Targets
To use a render target, use `args.outputs.sprites` with `:render_target_name` as the `path`.
```rb
args.outputs[:render_target_name].primitives << some_primitive

args.outputs.sprites << {
  x: x, y: y, w: w, h: h, r: r, g: g, b: b, a: a,
  path: :render_target_name
}
```

# State
Store arbitrary data between ticks.
```rb
args.state.game_name = "Name of the Game"
```

# Fullscreen
```rb
args.set_window_fullscreen_enabled = true
```

# Text Size
```rb
w, h = args.gtk.calcstringbox(string, size_enum, path_to_font)
```

# Inputs
## args.inputs.mouse
```rb
args.inputs.mouse = {
  :x,
  :y,
  :click,
  :down,
  :previous_click,
  :up,
  :inside_rect?,
  :inside_circle?,
  :moved,
  :button_left,
  :button_right,
  :button_middle,
  :button_bits,
  :wheel
}
```

## Directional
```rb
args.inputs.left
args.inputs.right
args.inputs.up
args.inputs.down
```

## args.inputs.keyboard
```rb
args.inputs.keyboard = {
  :key_held.KEY,
  :key_down.KEY,
  :key_up.KEY,
  :KEY,
  :up_down,
  :left_right,
  :raw_key
}
```

# Background Color
```rb
args.outputs.background_color = [red, green, blue]
```

# Sound Output
Using an `.ogg` file will cause the sound to loop.
```rb
args.outputs.sound << 'sounds/file.ogg'
```
For non-looping sounds:
```rb
args.gtk.queue_sound << 'sounds/file.ogg'
```

# Cursor Controls
```rb
args.show_cursor
args.hide_cursor
args.cursor_shown?
```

# See Also
[matrix](http://docs.dragonruby.org/#----advanced-rendering---15-matrix-and-triangles-2d---main-rb)
[geometry](http://docs.dragonruby.org/#---args-geometry-)
[grid](http://docs.dragonruby.org/#---args-grid-)
[write_file](http://docs.dragonruby.org/#----args-gtk-write_file-path--contents-)
[read_file](http://docs.dragonruby.org/#----args-gtk-read_file-path-)
[audio](http://docs.dragonruby.org/#--docs---gtk--args#audio-)
[server](http://docs.dragonruby.org/#----http---in-game-web-server-http-get---main-rb)
[http](http://docs.dragonruby.org/#----args-gtk-http_get-url--extra_headers-=-{}-)
