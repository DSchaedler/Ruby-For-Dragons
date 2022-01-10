---
title: Cheatsheet & FAQ
desc: Tips and Tricks to tame the Dragon.
layout: default
resource: true
categories: [Tutorials]
---

{% include header.html %}

_By Pineapple_

DragonRuby Starters
-------------

- Ruby is strongly-typed (not stringly-typed, like JavaScript), but you don't need to explicitly state a type
- You can use `.class` to find out what type you actually have

***

- Integers ("Fixnum") are signed 64-bit; there is a BigNum type available, but i've not tried to use it
- Floats are double-precision
- Strings are their own type (but this isn't important for you unless you're used to a language without them)

***

- A `?` at the end of a method name indicates that it will return a boolean
- A `!` at the end of a method name indicates that the method is "dangerous" (usually available for "modiy in-place" on methods that would return a changed copy)
- Type conversion will use a method named `.to_` followed by a letter indicating the type: Integer, Float, String, Array, Hash, probably some others too (note that not all conversions may be sensible)

***

- You generally don't need parenthesis around things (like `if` conditions and function calls)

***

- `elsif` is a five-letter word that will make you say a lot of four-letter words

***

- repl.rb is an incredibly useful tool for experimenting with syntax and techniques

***

For loops still exist, but there's often better choice
------------------------------------------------------

```rb
(1..10).each do |i|
  puts i
end
```

does a thing 10 times  
- `(1...10)` excludes the final number  
- if you just want to start at 0, then `10.times do` is easier  

`.each` is a thing to iterate over an array

```rb
a = [3, 6, 8, 4, 5]

a.each do |n|
  puts n
end
```

and if you need it, `a.each_with_index do |n, i|` exists as well

but if you just want to do the same operation on the whole array, `.map` might be more suitable  
and if you just want to get the sum of the array, `.reduce(:+)` will do that as well

My little dragon: arrays are magic
----------------------------------

There are some powerful tricks that can be done with arrays (and with anything that's Enumerable, which includes arrays and hashes)  
the trick is trying to understand it all...

- `.length` exists

- `.pop` and `.push` remove and add items from the high-index end ("the end") of the array
- `.shift` and `.unshift` remove and add items from the zero end ("the beginning") of the array

```rb
a = [3, 6, 8, 4, 5]
puts a.pop      # 5
puts a          # [3, 6, 8, 4]
a.push(7)
puts a          # [3, 6, 8, 4, 7]
puts a.shift    # 3
puts a          # [6, 8, 4, 7]
a.unshift(2)
puts a          # [2, 6, 8, 4, 7]
```

- `.append` adds to the end, `.prepend` adds to the beginning
- `<<` is another way of doing an append (which is often used in adding things to the outputs lists)
- `.delete_at()` deletes a specific index
- `.insert()` inserts a thing at a position

- Maybe useful things (that i'm used to having to write entire functions to do): `.reverse`, `.sort`, `.shuffle`, `.rotate` (can take a rotation distance)

- `.permutation` !!! this thing is a chunky function that you don't need to write. if you just want to get a list of permutations, apply `.to_a` as well

and i haven't even started on array maths yet...
this example from https://www.ruby-lang.org/en/ still feels incredibly game-changing to me (as primarily a C programmer):

```rb
# Ruby knows what you
# mean, even if you
# want to do math on
# an entire Array
cities  = %w[ London
              Oslo
              Paris
              Amsterdam
              Berlin ]
visited = %w[Berlin Oslo]

puts "I still need " +
     "to visit the " +
     "following cities:",
     cities - visited
     
# => I still need to visit the following cities:
# => London
# => Paris
# => Amsterdam
```

- Nested arrays are considered to be multi-dimensional, and have some tricks as well

- I'm not quite sure how to use `.map_2d`, but it exists
- Also `.transpose` (warning: this will error if the array is not rectangular)

Sometimes, hashes are better
----------------------------

If you don't need an order, but need paired data values, a hash is probably more suitable

Comparisons to arrays:
- `.map` becomes `.transform_keys` or `.transform_values`
- `.each` still exists, but expected to pass out both key and value (or an array of size 2, if you just give one iteration variable); in this way, it's more like how `.each_with_index` works on arrays (`.each_pair` is an alias in case this is more useful). `.each_key` and `.each_value` are available as well

- '.size' exists (and `.length` might also exist as an alias)

- `.merge` is useful. `newhash = hash1.merge(hash2)` will have hash2's values overrule hash1 where keys match (`.merge!` does the same thing, but modifies the object it is called on)
