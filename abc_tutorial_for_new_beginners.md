_By Dee Schaedler_

This tutorial assumes that you have never programmed before. If you have programming experience, the [Ruby on Wings tutorial](https://github.com/DSchaedler/Ruby_for_Dragons/wiki/Ruby-on-Wings) will provide an overview of the Ruby language for use with DragonRuby.

This tutorial does not assume that you are dumb, or don't know how to use computers. It uses adult language, and ways of explaining things. However, most people who want to start programming have never used the more difficult parts of their computer, and this tutorial tries to compensate for that. 

If at any point, something happens that I don't describe in the tutorial, or if it seems like something breaks, don't panic. I'll always include the full code at regular intervals. Compare what you have written to what I provide and try to spot the difference. Common culprits are missing commas, missing `]` brackets, or just spelling something incorrectly.

I encourage you to take this tutorial in multiple sections, and across multiple sessions. If you've never programmed before, there's a lot of information here to digest. Take the time to understand what new information is there, and play with the code until you understand what it's doing. You can't break anything permanently in DragonRuby, and if you're code gets completely messed up, copy it back in from here.

You've got this!

## Table of Contents
* [Step 0 - Install the Egine](https://github.com/DSchaedler/Ruby_for_Dragons/wiki/ABC-Tutorial-for-New-Programmers#step-0---install-the-engine)
* [Step 1 - Understanding the Sample Code](https://github.com/DSchaedler/Ruby_for_Dragons/wiki/ABC-Tutorial-for-New-Programmers#step-1---understanding-the-sample-code)
* [Step 2 - Hello World](https://github.com/DSchaedler/Ruby_for_Dragons/wiki/ABC-Tutorial-for-New-Programmers#step-2---hello-world)
  * [Step 2.5 - What about the other numbers?](https://github.com/DSchaedler/Ruby_for_Dragons/wiki/ABC-Tutorial-for-New-Programmers#step-25---what-about-the-other-numbers)
* [Step 3 - Putting a square on the screen](https://github.com/DSchaedler/Ruby_for_Dragons/wiki/ABC-Tutorial-for-New-Programmers#step-3---putting-a-square-on-the-screen)
* [Intermission - Code Editors](https://github.com/DSchaedler/Ruby_for_Dragons/wiki/ABC-Tutorial-for-New-Programmers#intermission---code-editors)
* [Step 4 - Our visual toolbox](https://github.com/DSchaedler/Ruby_for_Dragons/wiki/ABC-Tutorial-for-New-Programmers#step-4---our-visual-toolbox)
* [Step 5 - Variables](https://github.com/DSchaedler/Ruby_for_Dragons/wiki/ABC-Tutorial-for-New-Programmers#step-5---variables)

# Step 0 - Install the Engine
You've come across DragonRuby somehow, and you have a desire to make a game. DragonRuby is a great choice for making games! It is lightweight, easy to iterate ideas in, and has an affectionate community.

The first thing we'll have to do is get a copy of the game engine. You may have already received one through a game jam or bundle. If you haven't, head on over to [DragonRuby's Itch.io page](https://dragonruby.itch.io/dragonruby-gtk) to purchase a standard license. The game toolkit is available on Windows, macOS, Linux and Raspberry Pi. This tutorial will assume that you are making a game on Windows.

Once you've purchased a license for the engine, you should receive an email with a download link. Download the `dragonruby-gtk-windows-amd64.zip` file, or the correct file for your computer. If you need to download it again later, you can also find download links in your Itch.io library.

After downloading the file it will be in your `Downloads` folder, or wherever you saved it. It's fine to leave it there for now. Double click the `.zip` file to open it, then click `Extract All` at the top of the screen. If the option isn't there, click "Compressed Folder Tools" first. Leave the default options in place, and click `Extract`. Your computer will do some work, then open a folder containing a file `.itch.toml` and a folder `dragonruby-windows-amd64`. Whenever we reference the "DragonRuby Folder" going forward, this is the folder we mean. I'll attempt to reference it by it's full name, but I may occasionally call it just the "DragonRuby Folder".

Open the folder `dragonruby-windows-amd64`. This is where the game engine lives. If you double click `dragonruby.exe`, the engine will start and you will be greeted with a welcome screen. If you receive a screen that "Windows protected your PC", you can click `More info` and then `Run anyway`. If you get a "Windows Security Alert", click both checkboxes on the screen, and then press `Allow Access`.

The welcome screen will encourage you to read the official docs, which can be found by opening the `docs` folder, then double clicking `docs.html`. This will open a website with the "manual" for DragonRuby.

The welcome screen will also encourage you to join the [Official DragonRuby Discord](http://discord.dragonruby.org/). This is highly recommended, as it is a great resource to ask questions, share your work, and meet other people using DragonRuby (people who use DragonRuby call themselves "Dragonriders"). No question is too small to ask in the community discord.

The last thing we need to do before moving on to Step 1 is open the code. Unlike other game engines or game toolkits, DragonRuby does not come with any built-in editors. You have to edit the files directly, and then the engine will read them and run the code inside.

Leaving the engine window open, open the `dragonruby-windows-amd64` folder. Open the `mygame` folder, and then the `app` folder. This folder contains three files; `main.rb`, `repl.rb`, and `tests.rb`. Focus on `main.rb` for now, and ignore the other two files.

Either right click the `main.rb` file and choose `Edit` from the menu, or choose `Open with`, then `Choose another app`, then `More apps` then `Notepad`. Also select the checkbox to make `Notepad` the default app, then click `OK`.

A window will open with some text in it. This is the code that determines what shows on the engine screen! It will be helpful to "snap" the windows side by side, with the code on one side, and the engine window on the other.

You're now ready to write some code!

# Step 1 - Understanding the Sample Code

Let's take a minute to review what's in Notepad on our screen. This is what the code should look like:

```
def tick args
  args.outputs.labels  << [640, 500, 'Hello World!', 5, 1]
  args.outputs.labels  << [640, 460, 'Go to docs/docs.html and read it!', 5, 1]
  args.outputs.labels  << [640, 420, 'Join the Discord! http://discord.dragonruby.org', 5, 1]
  args.outputs.sprites << [576, 280, 128, 101, 'dragonruby.png']
end
```

Let's walk through this line by line.

`def tick args`  
A tick is the most basic unit of time in a video game. In DragonRuby, a Tick is the same thing as a Frame in games and other engines. All of the code that you write will happen within a single tick, and and visual changes you make will happen at the end of the tick. In DragonRuby, you are limited to 60 ticks per second.

This line of code is just telling the game engine where to start the tick. `def` means that we're starting a block or section of code. `tick` is the name of that section. `args` is a parameter what we use to interact with the game engine.

`args.outputs.labels << [640, 500, 'Hello World!', 5, 1]`  
This line of code is making the first line of text appear on the screen; `Hello World!`. This is a common first program to create in programming languages, and we'll unpack each part of this line later.

`args.outputs.labels  << [640, 460, 'Go to docs/docs.html and read it!', 5, 1]`  
This line of code makes the second line of text appear, the one instructing the programmer to read the manual.

`args.outputs.labels  << [640, 420, 'Join the Discord! http://discord.dragonruby.org', 5, 1]`  
This line of code makes the third line of text appear, the one directing the programmer to join the DragonRuby Discord server.

`args.outputs.sprites << [576, 280, 128, 101, 'dragonruby.png']`  
This line of code loads the image file for the DragonRuby logo that is shown under the text.

`end`  
This line of code ends the section or block that we started with `def tick args`. It tells the game engine that tick is done, and it can move on to the next step, in this case, running tick again.

Altogether, this code creates the screen that shows when you launch `dragonruby.exe`. You can see that each line of text on the screen has a corresponding line in the code, and the logo does as well. This code, contained in the `tick` block, is actually running 60 times per second. 60 times per second, DragonRuby is clearing the screen, and drawing each of these elements back onto it. Because none of the elements are changing though, it looks like nothing is moving at all.

***

To Review:
- We learned that all of the code in DragonRuby runs inside of a block named `tick`.
- We start this block with `def tick args` and end it with `end`.
- We can make text and images appear on the screen, using code that we'll explore later.
- Anything that is on the screen gets cleared, and then replaced 60 times each second, whenever `tick` starts again from the top.

# Step 2 - Hello World
We're finally going to edit the text that's in the notepad window. Go ahead and remove everything that's there. Just trust me, we're going to put stuff back. Type everything out the long way, instead of copying and pasting. It will give you much needed practice and understanding.

Lets start with a basic template. Once your notepad screen is empty, type this in.

```
def tick args
end
```

If you hit save now and check the DragonRuby screen, you'll see that all of the text and the image has disappeared. That's because we took out all of the lines telling DragonRuby to put stuff on the screen. Remember that everything on the screen gets cleared when `tick` starts, and then stuff is added when `tick` ends. If there's no code telling DragonRuby what to draw, then it won't draw anything.

DragonRuby will try to automatically load any changes you save to the `main.rb` file, which lets us make and see improvements in real time. 

Lets add some more code to what we have already.
```
def tick args
  args.outputs.labels << [640, 360, 'Hello World']
end
```

Be sure to put 2 spaces before the line we're adding. This helps us keep the code organized and reminds us that it runs inside of the `tick` block.

If you save the notepad file now, you should see the text "Hello World" appear on the DragonRuby screen, near the center. Let's break down each part of the line we added.

`args`  
This is a keyword we use to interact with DragonRuby. It basically tells the game engine, "Hey, listen to me! I need you to do something!".

`outputs`  
This keyword tells the game engine that we want it to make something happen, usually, put something on the screen. Our command is now "Hey! I need you to put something on the screen!"

`labels`  
This keyword tells DragonRuby what kind of thing we want. In this case it's a label, or piece of text. Our command is now "Hey! I need you to put a label on the screen!"

`<<`  
This is called the "append" operator. We're using it to signal that what comes next is the thing we want on screen. Our command is now "Hey! The thing after this is the label I want you to put on the screen!"

`[640, 360, 'Hello World!']`  
This part is the instructions for the label we want.

The `[` symbol at the beginning means that we're starting a list (called an *array*) of things.

The first number, `640`, is the horizontal position of the label. Imagine the DragonRuby screen as a grid, with the bottom left being horizontal (x) position 0 and vertical (y) position 0. The maximum horizontal size is 1280, and the maximum vertical size is 720. Anything outside of that will be drawn off screen. `640` is therefore, halfway across the screen horizontally.

The second number, `360`, is the vertical position of the label; It is halfway up the screen height vertically.

The last part, `'Hello World!'`, is the text we want to put on screen. We signal to DragonRuby that it is text by putting single quote marks ( ' ) on either side of it. Anything inside of the quote marks will be treated as text, and all of it together is called a "string".

The last part, the `]` symbol, is telling DragonRuby that we're done with our list.

Each individual part of the list is separated by a comma and a space. This is how DragonRuby tells the individual parts of the list apart.

The label drawing part of DragonRuby, `args.outputs.labels`, is expecting a list just like this one, with those numbers and that string, all in that order. We use `<<` to send that list into it.

So our final command, `args.outputs.labels << [640, 360, 'Hello World!']` is read by the computer as "Hey! I want you to put the text 'Hello World!' on the screen at horizontal position 640, and vertical position 360. I'm doing this by appending an array with what I want to `args.outputs.labels`.

***

To review:
- We ask DragonRuby to write text on the screen using `args.outputs.labels`.
- We do this by appending ( `<<` ) an array with the information we want to `args.outputs.labels`.
- The array is contained by the `[ ]` bracket symbols, and each part is separated by commas.
- The first two parts of the array are the location of the text on screen.
- The last part of the array is the text we want to write. It is all surrounded by single quote ( ' ) marks.
- The minimum horizontal position is 0. The maximum horizontal position is 1280
- The minimum vertical position is 0. The maximum horizontal position is 720.

Try playing around with the numbers and text in the array. You should notice that the position of the text on screen changes, or the words change. Remember that the screen will only change when the file is saved.

Next, we'll explore how to get a square onto the screen.

***

# Step 2.5 - What about the other numbers?
If you are paying attention, you may have noticed that the "Hello World!" code in the default sample looks like this

`args.outputs.labels  << [640, 500, 'Hello World!', 5, 1]`

while ours looks like this

`args.outputs.labels << [640, 360, 'Hello World']`

So what are those two extra numbers at the end of the sample code?

The first number is the text size. Increasing this number will make the text on screen bigger. The second number is the "Alignment Enumerator". This is a special number, and can be `0`, `1`, or `2`. When it is 0, the text starts writing at the point specified by the first two numbers, and continues to the right. When it is 1, the text centers its location on the point you specify, and when it is 2, the end of the text lines up with the point.

You can add these parts to the code we wrote earlier, to look like this:

```
def tick args
  args.outputs.labels << [640, 360, 'Hello World', 5, 1]
end
```

When you save, you should notice the text get bigger, and it is in the center of the screen better.

We didn't include these numbers earlier because they are optional. You only have to provide the horizontal position, vertical position, and text to draw a label, but there are other options you can add on to the end. They have to be added in the correct order, so you can't skip any.

***

# Step 3 - Putting a square on the screen
Text on the screen is nice, but lets make some more standard gameplay elements. Edit the code that we have to move the text out of the way.

```
def tick args
  args.outputs.labels << [10, 30, 'Hello World', 1, 0]
end
```

When you save, this will move the text to a small label in the bottom corner of the screen, giving us space to work. Now, we'll add what's called a `solid`. We do this in a similar way that we added a label.

```
def tick args
  args.outputs.labels << [10, 30, 'Hello World', 1, 0]

  args.outputs.solids << [640, 360, 20, 20]
end
```

Once this code is saved, we'll still have the small text in the corner, but a small black box has been added to the center of the screen. It is defined by an array, the same way the string was, but with different conditions. We also send it to `args.outputs.solids` instead of `args.outputs.labels`. Sending it to a different location tells DragonRuby that we want something different, and so it expects different values to be in the array.

The first value is the horizontal position, same as the label. The second value is the vertical position, again, the same as the label. The third value is the width of the box, and the fourth value of the array is the height of the box.

Try adjusting the values of the `solid` to see what they do. Move it around the screen and adjust it's width and height.

A black box and black text isn't very interesting though. Lets add some optional conditions to the `solid`

```
def tick args
  args.outputs.labels << [10, 30, 'Hello World', 1, 0]

  args.outputs.solids << [640, 360, 20, 20, 200, 100, 50]
end
```

Once saved, the `solid` is now an orange-red color. The conditions that we added control the color of the solid. The first one is the amount of red in the color, the second one is the amount of green, and the third one is the amount of blue. We can add another condition to make the box slightly transparent.

```
def tick args
  args.outputs.labels << [10, 30, 'Hello World', 1, 0]

  args.outputs.solids << [640, 360, 20, 20, 200, 100, 50, 127]
end
```

It's not just `solids` that can have their color changed. Let's add some conditions to the label to make it a nice turquoise color.

```
def tick args
  args.outputs.labels << [10, 30, 'Hello World', 1, 0, 0, 127, 127, 255]

  args.outputs.solids << [640, 360, 20, 20, 200, 100, 50, 127]
end
```

The minimum for the color and transparency values is 0. The maximum is 255. White is all three color values set to 255, and black is all three set to 0. Black is the default color for output elements.

***

To Review:
- We can ask DragonRuby to put a square on the screen similarly to a label, but using `args.outputs.solids`
- Solids are made of arrays that look like `[x_position, y_position, width, height]`
- Most output types have optional arguments, like size, alignment or color values that can be provided.
- Colors are defined by providing an amount of red, green, and blue to mix together.
- Output elements can be made to be slightly transparent.
- The minimum for a color or tranparency value is 0. The maximum is 255.
- White is the color values `[255, 255, 255, 255]`. Black is the color values `[0, 0, 0, 255]`.
- Black is the default color value for DragonRuby.

Next, We'll show all of the different kinds of things DragonRuby can put on screen.

***

# Intermission - Code Editors
Notepad has been fine until this point, but it's annoying sometimes, doesn't help us any, and will cause formatting problems in the future. We suggest you download a different code editor. 

One that's friendly to beginners is [Notepad Plus Plus](https://notepad-plus-plus.org/downloads/). Click the release at the top of the linked page, then click the green download button. It will install the same way as any other program. Just follow the prompts until it says that installation is complete. 

From there, you can right click the `main.rb` file, and select "Edit with Notepad++", or select "Open With, choose another app, more apps". Find and pick Notepad ++, click the checkmark to always use this app to open .rb files, and click ok. From now on, you can double click `main.rb` to open it, and it will open in Notepad++.

Notepad++ will detect that we are programming in Ruby, and will highlight certain parts of the code, like `def`, `end`, and the values in the arrays. From now on, code on this tutorial will have similar highlighting. The colors will be different, but having code highlighting helps to understand what parts of the code are control words, names, numbers, strings, etc.

This is how the code highlighting will look for the rest of this tutorial.

```ruby
def tick args
  args.outputs.labels << [10, 30, 'Hello World', 1, 0, 0, 127, 127, 255]

  args.outputs.solids << [640, 360, 20, 20, 200, 100, 50, 127]
end
```

***

# Step 4 - Our visual toolbox
The first thing I'm going to do in order to compare all of the different output types is remove all of the optional arguments, and move the existing elements to a more visible location.

```ruby
def tick args
  args.outputs.labels << [50, 500, 'Hello World']

  args.outputs.solids << [200, 500, 20, 20]
end
```

Now, when we save the file, both elements should be in the upper left corner of the screen, and both are black. Let's add a new element, called a `border`.

```ruby
def tick args
  args.outputs.labels << [50, 500, 'Hello World']

  args.outputs.solids << [200, 500, 20, 20]

  args.outputs.borders << [250, 500, 20, 20]
end
```

This element appears as a black square, but unlike a `solid` this one is hollow, with just a thin border. It uses the same set of numbers as a `solid`

Next we'll add a `line`.

```ruby
def tick args
  args.outputs.labels << [50, 500, 'Hello World']

  args.outputs.solids << [200, 500, 20, 20]

  args.outputs.borders << [250, 500, 20, 20]
  
  args.outputs.lines << [300, 500, 350, 450]
end
```

This element just draws a thin line from one point to another. The first two numbers are the x and y location of the first point, and the second two numbers are the x and y location of the second point.

Finally, we'll add a `sprite`.

```ruby
def tick args
  args.outputs.labels << [50, 500, 'Hello World']

  args.outputs.solids << [200, 500, 20, 20]

  args.outputs.borders << [250, 500, 20, 20]
  
  args.outputs.lines << [300, 500, 350, 450]
  
  args.outputs.sprites << [400, 300, 100, 100, 'sprites/misc/dragon-0.png']
end
```

When you save, there should now be a picture of a dragon on the screen.

Sprites are arguably the most powerful kind of element we can ask DragonRuby to draw. The first four parameters in the array are the same ones used in the `solid` and `border`. The last parameter is the location of the `.png` file we want to load. DragonRuby only accepts `.png` image files.

DragonRuby starts looking for files in the folder `dragonruby-windows-amd64/mygame`. If you look, inside of the `mygame` folder, there is a folder called `sprites`. Inside of the `sprites` folder is a folder called `misc`. and inside of the `misc` folder, is an image file called `dragon-0.png`.

We call the location of the image file it's path, and it's full path is `sprites/misc/dragon-0.png`. We pass this as a string in the array, which is why it is surrounded by single quotes.

Just like with the solids, borders, and other screen elements, we can move sprites around on the screen. Try changing the location and size numbers for the sprite to see how they are reflected. Also, try changing the path to be a different file in the `sprites` folder. It should load a new image in place of the dragon once you save.

***

To Review:
- We can draw `label`s, `solid`s, `border`s, `line`s, and `sprite`s.
- Sprites draw a pre-made image onto the screen.
- We can re-size sprites to stretch them bigger or smaller.
- DragonRuby starts looking for files inside of the `mygame`folder.
- Sprites can only be `.png` files.
- The location of a file is called it's path, and is passed as a `string`.

***

# Step 5 - Variables

`Variables` are a type of container that we can use to hold information. In order to make a `variable`, we first have to pick a name. A `variable`'s name should describe what it is going to be used for.

First, let's clean up our code so that only the `sprite` is left on screen.

```ruby
def tick args
  args.outputs.sprites << [400, 300, 100, 100, 'sprites/misc/dragon-0.png']
end
```

Now, let's create some of these variables. To create them, we just use their name, and use the `equals sign` to fill the container with a value.

```ruby
def tick args

  x_position = 400
  
  y_position = 300
  
  width = 100
  
  height = 100

  args.outputs.sprites << [400, 300, 100, 100, 'sprites/misc/dragon-0.png']
end
```

Notice that I set each variable to be the same number as one of the numbers in the sprite array. We can replace the numbers in the sprite array with the variable name to use the number that is stored in the variable.

```ruby
def tick args

  x_position = 400
  
  y_position = 300
  
  width = 100
  
  height = 100

  args.outputs.sprites << [x_position, y_position, width, height, 'sprites/misc/dragon-0.png']
end
```

If done correctly, the dragon should still be on the screen, exactly where it was before; But now, if you change the value of the variable and save, the dragon will move to the variable's new value.

Variables can also be set to the value of other variables, or of math operations. Try these two replacements for the line `height = 100`.

`height = width`

`height = width * 2`

In the example above, `*` is being used to multiply `width` by `2`. Other math operators are more straightforward.

`+` - Addition

`-` - Subtraction

`*` - Multiplication

`/` - Division

We can also set the image path to a variable. Remember that `args.outputs.sprites` is still expecting to receive the right kind of information, in the right order, so we have to be careful how things are set and which order they are placed in the array.

```ruby
def tick args
  x_position = 400
  y_position = 300
  width = 100
  height = 100

  path = 'sprites/misc/dragon-0.png'

  args.outputs.sprites << [x_position, y_position, width, height, path]
end
```

***

To Review:
- Variables are containers that hold information.
- Variables are defined by setting their name equal to some information (`height = 20`).
- Variables can be used in other places in the code, in place of the information they hold.
- Variables can be set equal to other variables.
- Variables can be set equal to math operations.
- Variables can be used in math operations.
- The basic math operations are `+`, `-`, `*`, `/`.

***

To be Continued...
