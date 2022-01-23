---
title: Demos
desc: Demos of frequently used code.
layout: default
published: true
indexed: true
categories: [Tutorials]
---

{% include header.html %}

# Bouncing Box
_By Dee Schaedler_  
[Live Demo](https://deeschaedler.itch.io/border-bounce)
```ruby
def tick(args)
  args.state.border ||= { x: 100, y: 100, w: 1080, h: 520 }
  args.outputs.borders << args.state.border

  args.state.box ||= { x: 300, y: 300, w: 32, h: 32 }
  box = args.state.box
  args.outputs.solids << box

  args.state.speed ||= [3, 3]
  speed = args.state.speed

  future_ball_rect = { x: box.x + speed[0], y: box.y + speed[1],
                       w: box.w, h: box.h }

  if args.geometry.inside_rect?(future_ball_rect, args.state.border)
    box.x += speed[0]
    box.y += speed[1]
  elsif future_ball_rect.x < 100 || future_ball_rect.x + future_ball_rect.w > 1180
    speed[0] *= -1
  elsif future_ball_rect.y < 100 || future_ball_rect.y + future_ball_rect.h > 620
    speed[1] *= -1
  end
end

```

# Z-Height
_By Dee Schaedler_
```ruby
def tick(args)
  z_layer = Array.new(3) { [] }

  z_layer[2] << { x: 590, y: 310, w: 200, h: 200, r: 0, g: 0, b: 255, primitive_marker: :solid }
  z_layer[0] << { x: 540, y: 260, w: 200, h: 200, r: 255, g: 0, b: 0, primitive_marker: :solid }
  z_layer[1] << { x: 490, y: 210, w: 200, h: 200, r: 0, g: 255, b: 0, primitive_marker: :solid }

  z_draw(args, layers: z_layer)
end

def z_draw(args, layers:, debug: nil)
  args.outputs.primitives << layers if layers
  args.outputs.debug << debug if debug
end

```

# Z-Height with Render Targets
_By Dee Schaedler_
```ruby
def tick(args)
  initialize(args)

  args.outputs.sprites << {x: 0, y: 0, w: 1280, h: 720, path: :layer_0}
  args.outputs.sprites << {x: 0, y: 0, w: 1280, h: 720, path: :layer_1}
  args.outputs.sprites << {x: 0, y: 0, w: 1280, h: 720, path: :layer_2}
end

def initialize(args)
  args.render_target(:layer_0).solids << { x: 540, y: 260, w: 200, h: 200,
                                     r: 255, g: 0, b: 0,
                                     primitive_marker: :solid }

  args.render_target(:layer_1).solids << { x: 490, y: 210, w: 200, h: 200,
                                     r: 0, g: 255, b: 0,
                                     primitive_marker: :solid }

  args.render_target(:layer_2).solids << { x: 590, y: 310, w: 200, h: 200,
                                     r: 0, g: 0, b: 255,
                                     primitive_marker: :solid }
end

```
