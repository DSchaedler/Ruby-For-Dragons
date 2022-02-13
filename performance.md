---
title: Performance
desc: Common methods to improve engine speed
layout: default
published: false
indexed: false
categories: [Tutorials]
---

{% include header.html %}

_By Dee Schaedler_

DragonRuby, when you first start using it, can seem to be a very slow engine. However, when pushed to it's full potential, it can outcompete ~~Unity~~ other popular game eninges. There are several methods to improve performance, most of which are ways of optimizing the render phase of a game tick. Outputs is the slowest thing you can do in DragonRuby, so managing it is crucial.

# 1. Use Output Hashes
The default method for rendering primititves is like this:  
`args.outputs.labels << [580, 400, 'Hello World!']`  
This works fine, but the engine has to search every spot in the array to determine which data is being provided, and validate it before it can be used. Explicitly telling the engine which data you're providing is much faster:  
`args.outputs.labels << { x: 200, y: 550, text: "dragonruby", size_enum: 2 }`  
This works for all primitve types that can be sent to `args.outputs`. Hashes in general are insanely fast in DragonRuby, and should be used whenever you need to work with a set of data that isn't in a specific order.

# 2. Send Primitives to `outputs` in Bulk
It is tempting, if you are looping through something multiple times to structure a loop like
```
label_height = 0
10.times do
    args.outputs.labels << [100, label_height, "Hello, World!"]
    lablel_height += 20
end
```
However, this is very slow. The code above sends things to outputs 10 times. Instead, we can structure the loop like:
```
label_height = 0
10.times do
    args.state.labels << [100, label_height, "Hello, World!"]
    label_height += 20
end
args.outputs.labels << args.state.labels
```
This calculates all of the labels, but draws them all at once.

# 3. Combine Primitives in a Render Target
Render Targets are a way of creating sprites dynamically in the engine. This reduces the overhead when drawing.
```
def tick args
  if args.state.tick_count == 0
    args.render_target(:rect).solids << { x: 540, y: 260, w: 200, h: 200, r: 255, g: 0, b: 0, primitive_marker: :solid }

    args.render_target(:rect).solids << { x: 490, y: 210, w: 200, h: 200, r: 0, g: 255, b: 0, primitive_marker: :solid }

    args.render_target(:rect).solids << { x: 590, y: 310, w: 200, h: 200, r: 0, g: 0, b: 255, primitive_marker: :solid }
  end
  
  args.outputs.sprites << {x: 0, y: 0, w: 1280, h: 720, path: :rect}
end
```

# 4. Use Static Outputs
If on-screen elements never, or rarely change, it may be appropriate to set them as static. Once sent to a static output, they will be re-drawn every frame, without needing to have them sent to `outputs` again. Elements in static outputs can still have their properties changed if they are stored in variables.
```
# Code by Kota
def tick args
  if args.state.tick_count.zero?
    args.state.my_solid = { x: 100, y: 300, w: 30, h: 30 }
    args.outputs.static_solids << args.state.my_solid
  end

  args.state.my_solid.x = (args.state.my_solid.x + 10) % 1270
end
```

# 5. Use `while` Loops
While `10.times do` seems like a very convenient way to create a loop, `while` loops have been proven to be the fastest loop type in DragonRuby by a significant margin. Changing to `while` loops may provide performance improvements in parts of your game that rely on loops during caclulation.
```
loop_index = 0
while loop_index < 10
  # Do Some Code Here
  loop_index += 1
end
```