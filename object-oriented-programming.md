---
title: Object Oriented Programming
desc: A short OOP Tutorial.
layout: default
published: true
indexed: true
categories: [Tutorials]
---

{% include header.html %}

_By Kniknoo_

# Using Classes in DragonRuby

A common point of confusion for experienced Rubyists coming into DragonRuby is
"Can I use Objects instead of global state?". Absolutely!

This documents aims to help users get started writing their own classes. If
you've tried this on your own, you may have noticed that the Dragon doth protest
and offers some cryptic clues about solutions. There are 3 common gotchas that
will be covered before expanding into several distinct approaches to using these
classes in DragonRuby.

The first two gotchas come up when trying to use classes to represent the basic
building blocks of DragonRuby, the primitives. When the renderer is trying to
directly render a class reference, there are two key groups of data that it is
always looking for, the attributes and the inspect method.

# Attributes

Attributes or Instance Variables are a key component to how an Object talks to
the outside world and to itself. The Dragon Renderer will be looking for a
certain set of these for each primitive type that correspond to the keys used in
hash form.

The most basic and universal of these are

```
attr_accessor :x, :y, :r, :g, :b, :a, :primitive_marker, :blendmode_enum
```

`x` and `y` are the coordinates of the bottom left corner, `r` `g` `b` and `a` are the
red green blue and alpha components of the color, and a primitive marker tells
the `args.outputs.primitives` array what kind of primitive this class represents.
`blendmode_enum` gets into some more advanced uses of color mixing, but for now
it's only important to know that it's a required attribute.

In addition to the above universals, each primitive type has its own set of
attributes that also need to be set.

Labels:
```
attr_accessor :text, :size_enum, :alignment_enum, :font
```

Borders and Solids:
```
attr_accessor :w, :h
```

Lines:
```
attr_accessor :x2, :y2
```

Sprites:
```
attr_accessor :w, :h, :path, :angle, :source_x, :source_y, :source_w, :source_h,
              :tile_x, :tile_y, :tile_w, :tile_h, :flip_horizontally,
              :flip_vertically, :angle_anchor_x, :angle_anchor_y
```

I write it out this way so that you can see exactly which attributes exist with
each primitive type. In theory, this works fine, but in practice, this can lead
to headaches from breaking changes when new attributes are added. Because of
this, there are special `attr` calls that do the above and evolve with the system.
`attr_sprite` will fill in all of the universals plus the sprite `attr`s, and
`attr_rect` will fill in the universals plus the Solid and Border `attr`s. In
addition, there is an `attr_gtk` that will offer access to `args` using the
method signature described at [https://github.com/DragonRuby/dragonruby-game-toolkit-contrib/blob/a1b8552ae442d1fa22df1e569652eb99750dcebf/dragon/attr_gtk.rb](https://github.com/DragonRuby/dragonruby-game-toolkit-contrib/blob/a1b8552ae442d1fa22df1e569652eb99750dcebf/dragon/attr_gtk.rb)

All of these are declared like `attr_accessor`, that is, preferably near the top
of your class declaration. Unlike `attr_accessor`, they take no arguments.

The next thing to know about are three methods that are commonly called on
`object`s by DragonRuby, and will cause errors that obscure your actual error
within a class if they aren't at least present. These are `#serialize`, `#inspect`,
and `#to_s`. While you can get away with leaving these defined but empty, you'll
be doing yourself favors in the future by filling these out with useful info.
`#inspect` is a representation that will show up if you add your `object` to `state`,
and is also displayed when an exception occurs in the terminal. `#to_s` is called
on a number of terminal operations involving the `object`, such as passing its
reference to another variable. `#serialize` will be displayed in exception logs
outside of the terminal.

# Require

The final gotcha that will come up is when you inevitably decide to start
breaking your program into multiple files. If you're used to the Ruby way of
doing require, you will wind up with errors that don't seem to make sense, like
claims that the class you've made doesn't exist. First off, there is no require
relative method. Require will work a lot like `require_relative` though. Secondly,
the relative path from your game folder's root and the file extension are
mandatory.

Instead of

`require "my_library"`

you'll want

`require "lib/my_library.rb"`

Require is done in an asynchronous way, meaning that your `tick` method in `main`
will already be running while `require`s are loading data from other files. If
you're expecting a specific order of operations, this can be very confusing. In
order to get around this, you can delay the onset of `tick` be putting it into
a file that is `require`d last instead of leaving it in `main`. My own usual setup
is to have `main.rb` responsible for requiring everything and doing any tasks that
I want to be complete before the first `tick` happens. So for example:

```
#main.rb

require "lib/my_lib1.rb"
require "lib/my_lib2.rb"
require "lib/my_lib3.rb"
require "app/tick.rb"
```
```
#tick.rb

def tick(args)
  my_lib ||= MyLib.new
  #game methods and so on
end
```

When you `require` a file, Ruby adds everything inside of it to its memory and
treats everything together like one gigantic file. This means, for instance,
you might have a `constant` defined in `file_one` while being referenced in `file_two`
and this all works as if they were in the same file. By extension of this, if
you reopen and redefine a class or method Ruby will only see the last definition
of it. So you wouldn't want to have a `my_method` in one file that is relied upon
by parts of that file and another `my_method` in another file that does something
different. Only one of these would be remembered, and only the most recently
evaluated version will be that one. The same goes for classes. If you're afraid
you might accidentally cause a naming collision like this, your best solution
is to put your class or method inside of a module and use a fully qualified
name.

```
module MyLib1
  def self.my_method
    "Look I made a method!"
  end
end
```
```
module MyLib2
  def self.my_method
    "And here is another method!"
  end
end
```
```
MyLib1.my_method
#=> Look I made a method!
MyLib2.my_method
#=> And here is another method!
```
