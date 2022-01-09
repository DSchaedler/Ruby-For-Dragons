---
title: Ruby on Wings
layout: default
resource: true
categories: [Tutorials]
---

{% include header.html %}

_By Kniknoo_

***

[Def](#methods)  
[Array](#arrays)  
[Variable](#variables)  
[String](#strings)  
[Numeric](#numerics)  
[Boolean](#booleans)  
[If/Unless/Case](#if-unless-and-case)  
[While/Until](#while-and-until)  
[Blocks](#beginning-blocks)  
[Range/Step/Times](#ranges-and-step)  
Map  
Hash - ADV  
Class - ADV  
API Listing  




# A Few Words about Ruby
  TODO Brief history and touch on ruby culture, including Matz and Why?
  TODO Overview of ruby paradigms. AKA What IS Ruby?


#  Methods
  Our overview of Ruby starts with defining a method. Why? In DragonRuby, everything we do will be
  centered around a particular method called "tick". For now, we'll demonstrate the basic structure
  of a method. Why do we say "method" instead of "function"? Everything in ruby is "secretly" an
  object. That's not important to dwell on now, but note you'll see Ruby folk favor the "method"
  terminology.
  A Basic method:

```rb
def a_basic_method
  "I am a basic method!"
end
a_basic_method
```

  This is about as basic as a method can get, We start with the "def" keyword and end with "end".
  After def we have the name of the method. In Ruby these are always snake_cased. On the middle line,
  indented by two spaces, is the body of the method. In this case it simply returns the message
  written as is. Note that return is always implied. Most other languages want you to explicitly
  return values from a function. In ruby, however, the last evaluation in a method is returned as the
  result of the entire method.
  Here is an example of a method with arguments:

```rb
def echo(word)
  word
end

echo("Hello")
echo "Hello"
echo 2
echo "Doowutyalike"
```


  The echo method takes in a value of any kind and hands it right back to you. Nothing too special,
  but you can see an argument can be passed after the name of the method. When defining a method,
  parentheses are optional if there is a single value, eg "def echo word ...". When calling a method,
  parentheses are completely optional but be sure not to confuse yourself or the parser. When in
  doubt, use the parentheses.
  Here are two more methods demonstrating default values.

```rb
def echo_hello_or(word = "Hello!")
  word
end

def echo_word(word: "World")
  word
end

echo_hello_or
echo_hello_or "World"

echo_word
echo_word(word: "Hello")
```

  When a default argument is defined, there is no need to add any further information. When starting
  out, favor the " = " notation. especially when using multiple arguments. There are some nuances to be
  aware of about the order of arguments that will come up as you try more advanced methods. In short,
  " = " represents positional arguments, while "word:" can be given in any order.
  for example:
  (note "p", "print", and "puts" all display results on the screen. We'll see them more in a later section)

```rb
def print_two_words(word1 = "Hello", word2 = "World!")
  p word1
  p word2
end

print_two_words
print_two_words "Goodbye"
print_two_words "Goodbye", "Dave"
```

In the example above, we can only give values in order. On the other hand:

```rb
def puts_two_words(word1: "Hello", word2: "World!")
  puts word1
  puts word2
end

puts_two_words word2: "Dave!"
```

  (If you're following along with Ruby, you may see the subtle difference between p and puts in their
  Implied Returns. We'll discuss the implications of that difference when we get to Booleans.)
  By using a named argument, we can choose what value to change. Again be carfeul mixing the two
  together, ALL positional arguments must come before named ones.
  That's the basics of methods. There's always more to learn, this is far from an exhaustive look
  at how they can work, but we'll expand on this as we continue along.

#  Arrays
  First Methods and then Arrays?! What kind of backwards Ruby tutorial is this?
  Besides the tick construct you'll be spending a lot of time in DragonRuby, especially early on,
  "feeding" Arrays to the Dragon. So what is an array? It's a list of data accessed by an index. This
  could be any kind of data: words, numbers, truth values, more arrays, hashes, or any combination. So
  what does that look like and how do we use it?

```rb
[1, 2, 3, 4, 5]
[12345, "?", "an idiot's luggage", true, ["space", "ball"], {luggage: 12345}]
```
To grab a piece of data in the list, use an index number, starting from 0 in square brackets:
```rb
puts [1,2,3,4,5][0]
```
that will result in "1" because it is the element at index 0. You can also accomplish this with:
```rb
puts [1,2,3,4,5].first
```
To access the last value, use a -1 for the index. This works for any negative index to get the nth
Value from the end. Ex:
```rb
puts [1,2,3,4,5][-1]
```
or
```rb
puts [1,2,3,4,5].last
```
 to get "5". We can also ask for a sub-list by giving a pair of  comma-seperated values. The first is
 the starting index while the second is the number of values.
```rb
puts [1,2,3,4,5][1,3]
```

  will give [2,3,4] because we start at index 1 and ask for three values. Another core feature of
  arrays that we'll look at in more detail soon is the ability to concatenate a new array or value
  to a list of arrays. For example:

```rb
puts [1,2,3,4,5] << 6
```
  will put the 6 at the end of the array before showing the result.
  In DragonRuby you'll generally spend more time creating arrays than acessing them. For now we'll
  leave it there. It's more important that we can recognize an array and its square notation than worry
  about all the available methods it can use for now. You haven't seen the last of the array,


#  Variables
  Yes, finally, a true intro topic.
  Data can be very hard to process if it isn't stored in some fashion. This is where the variable comes in.
  Variables are developer defined words that store data or object refrences. For now we'll just talk about
  data. Before showing any examples, it's worth mentioning variable scope and that DragonRuby has some
  different rules from many other Ruby implementations. We do not have a top level local variable like
  you may be used to. Instead I will commit a Ruby sin and use the global variable scope when showing
  these examples. The correct DragonRuby way will be brought up once we've covered a few of its particular
  features. And now, without further ado... a variable!

```rb
$five = 5
```

  Marvelous isn't it? It's just pouring out meaning an expression in a way that a digit can't. Ahem...
  Well, maybe not, but that's the example and I'm sticking to it. The "$" at the beginning means
  that it's a global variable. You should use these sparingly if ever, but it can be a quick and
  easy tool for developing, so don't discount its value. Now for some more examples:
```rb
$word = "bird"
$summer_of_love = 1969
$shopping_list = ["eggs", "whipped cream", "hammer"]
$the_answer = 6 * 8 #I swear!
$the_world_is_flat = false
$best_pizza_toppping = "pineapple"
$cheese_available = [["cheddar", false], ["swiss", false]]
```

  As you can see, there are many uses for a variable, both practical and impractical. In DragonRuby, you'll
  have a structure called args.state that will hold you variables for you, more on that soon. There are
  a couple more type of variables you may run across, like an instance variable (@ttribute) and a class
  variable (@@ttribute). We'll cover those more when discussing classes. You'll also occasionally see
  a :symbol. While they have uses beyond Hashes, we'll discuss them in more detail when we start looking
  at Hashes.
  Now let's combine some elements from the last three sections.

```rb
def array_of_five
  [1,2,3,4,5]
end

$my_array = array_of_five
```
We've stored the return value of array_of_five into $my_array.
```rb
$my_array << 6
```
`[1,2,3,4,5,6]`

Now we'll set a value in the array by index.
```rb
$my_array[2] = 10
```
`[1,2,10,4,5,6]`
```rb
def return_first_element(array)
  array.first
end

puts return_first_element($my_array)
```
`1`

  As you can see, there are a number of uses for variables just with arrays. As we add in more data
  types, we'll begin to really unlock the power of Ruby.


#  Strings
  We've already seen a couple examples of strings in previous examples."Hello", "World", "Dave", etc. There
  are two common ways to denote strings, with either single or double quotes. The general rule of thumb
  is to use single quotes if you don't plan to change the string and double quotes if you do. The reason
  for this will bring us to the main topic of strings in ruby, String Interpolation. Interpolating a
  string means to substitute the values of variables or methods inline. You should pretty much always
  use this method of creating a complex string for the sake of speed efficiency. Here are some examples:

```rb
p "Two plus three equals #{2 + 3}"
p "The time is currently #{Time.now}"

def hello_to(name)
  "Hello, #{name}, it's  pleasure to meet you!"
end

p hello_to("Rasputin")
```

  Take note of a few things in these examples. First off, "p" is being used to show the result on the
  screen. It's subtle difference from other print commands is that it returns its value in addition to
  showing it on the screen. "puts" behaves very similarly except it returns "nil", a value we'll discuss
  shortly. Finally there is "print", which does not put a newline at the end of the string, meaning it
  shows successive print calls on the same line. Another thing to note is that all of these examples
  use double quotes because of interpolation, it would not work, and give you a literal result with
  single quotes. One more way to work with strings that can be helpful, especially when formatting
  digits is to use % format strings. It's a bit of a complex topic but here are two common examples:
```rb
p "$%d.%02d" % [30,3]

# $30.03

p "%02d:%02d" % [7, 15]

# 07:15
```

  The first example starts with a literal $. The percent sign (in double quotes) starts a format string.
  The 0 is the padding we want to use. The 2 is the number of digits we want represented, regardless of
  how few digits the number has. The d states that it will be a digit value, as opposed to a float. From
  there everything else is either literal or a variation of the above formula. So what happens if you
  want to actually us a "%" ? This is where we "escape" a character by prefixing it with an escape
  character. In this case it will be "%" (%%) in most others it will be "\". For example:

```rb
p "Gotta give it %3d%%" % [110]

# Gotta give it 110%

puts "Look at the pretty pattern I\'ve made: \#\{\}"

# Look at the pretty pattern I've made:  #{}

puts "We\nare\neach\non\nnew\nlines."

# We
# are
# each
# on
# new
# lines.
```

  As the message above implies, "\n" is a signal to the output to go to the next line. You'll see this
  along with the occasional "\t" for <TAB> and rarely "\r\n" on Windows files.
  This should be enough to get started on Strings. As with everything, there is a lot more to learn!




#  Numerics
  Ah, the mighty number. Along with logic, it makes up the core of any computer programming langauge. Ruby
  supports a variety of numeric types, but in DragonRuby we'll typically focus on Integers (Fixnums) and
  Floats. Most basic math operations work just as you'd expect them to, with the exception of integer
  division, which is what would typically be called "floor division".

```rb
2 + 3

# 5

3 - 2

# 1

2 * 3

# 6

3 / 2

# 1

# You see that only the integer part of the answer is shown, not the expected "1.5". Instead:

3 / 2.0

# or

3 / 2.to_f

# 1.5

# Just as to_f "casts" the number to a float, to_i will remove the decimal places.

1.5.to_i

# 1

# Note this is a floor, not a rounding operation. For that there's

1.7.round

# 2

# To get the modulo (remainder of division) we use %

5 % 3

# 2

# To get both the integer and remainder, there's divmod

5.divmod(3)

# [1, 2]

# For powers we usee **

2**3

# 8

2**-2

# 0.25

# With an array of numerics, you can find the maximum and minimum value in the list.

[2,3,4,1].max

# 4

[0,5,100, -3, 6].min

# -6
```

  As always, there is plenty more to cover, but this should get you started
  working with mathematic operations.



#  Booleans
  The next few sections will cover some of the logical operations we can perform in Ruby. First, a bit
  a Boolean values. At its core, any Boolean system is going to refer to True and False and logical
  operations that can be berformed with them, such as "and" and "or". In Ruby, we take it one step
  further and think of everything having a "truthy" state. Ruby has 2 Falsey values, "false" and "nil".
  In Ruby, "nil" is equivalent to "null" in many other language, a variable with no defined value. It's
  not 0, zero is defined as zero. "nil" is nothing. In practice, any other value is considered "truthy",
  whether it be "1", "bob", "true"... whatever. This seems a strange point to bring up, but it will be
  very important when controlling logical flow in a loop or if statement.
  While we have a full range of logical operations we can perform, such as bit-shifting, the most
  important early operations to understand are "and / &&" and "or / ||". I'll be using the symbols in
  the examples, but the words (almost) work the same.

```rb
true && true

# true

true || false

# true

true && false

# false

false || false

# false
```

  Ruby uses what is called "short circuit logic" when doing logical comparison. This means that if it
  can determine the state of truth in a series of booleans, it will skip the extra work to compare
  everything. For example:

```rb
true || false || true || false

# true at the first value, remaining three are ignored.

false && true && true && true

# false at the first value, remaining three are ignored.
```

  While you will occasionally directly use boolean values to represent game state, you will often use
  comparisons to generate Boolean values. The comparison operators in Ruby are "==, !=, >, <, >=, <=". In
  many cases these comparisons will be done as Numerics, but equality in strings works just as well.

```rb
5 > 0

# true

0 != 0

# false

5 >= 5

# true

(2 >= 5) || (true != false)

# true

"bob" == "bob"

# true

"steve" == "dave"

# false
```

  Beware of a common mistake that everyone makes from time to time. If you accidentally try to compare
  with something like "$bob = 'bob'" instead of "==" you will always get true because of the truthiness
  mentioned above. Setting a variable returns the contents of that variable, itself a truthy state...
  unless you set "false" or "nil". Odd, no? Try not to confuse yourself, even though you CAN, don't
  do variable assignments in a comparison, and look there first for strange Boolean results. Note there
  is also a "===" comparison, but that one works in a very unusual and loose way that will make more
  sense in the next section. Which brings us to...





#  If, Unless, and Case
  At the heart of any computer language down to assembly, decision making is a critical part of program
  flow. Now that we've taken a look at Truthiness, let's see how to use this to make decisions in Ruby.
  First let's look at If and Unless. Both of these keywords can be used to set up an "if" structure, but
  unless has the excat opposite meaning. If something were to work when true on an if, it would work with
  false on an Unless. Let's see what I mean.


```rb
def bool_or_echo(word)
  if word == true
    puts "You got true!"
  elsif word == false
    puts "That is false"
  else
    puts word
  end
end

bool_or_echo(true)

# You got true!

bool_or_echo(false)

# That is false

bool_or_echo("Hello!")

# Hello!

$flat_world = false

unless $flat_world
  puts "That's legit."
else
  puts "I wholly disagree."
end

# That's legit.

# There is also a shorthand one-liner for when no else or elsif is necessary.

puts "Truth remains truth!" if true

puts "Mathematics has not broken down." unless 1 == 0
```

  So what happens if you have some very detailed ways of interpreting a value? Do yo just keep typing
  "elsif" after "elsif"? Fortunately we have a shorthand for complex comparisons called a "case"
  statement. At the end of the last section, I mentioned a "===" operator. Behind the scenes, that
  is what the case statement uses, so a good way to understand the nuances of "===" is to see how a
  case responds to your assertion. For the most part it can work like "==" but "===" will also allow
  you to check within groups to see if it is included, rather than a one to one comparison. For now
  we'll treat everything as a "==", but I'll bring up this point again when discussing ranges in a few
  sections. Let's look at a simple case example.

```rb
def truth_or_dave(word)
  case word
  when true then "That is true."
  when false then "That is false"
  when "Dave" then "That is Dave"
  when "dave"
    "You should capitalize your name, Dave!"
  else
    "I don't know what to make of that kind of talk."
  end
end

truth_or_dave "Dave"

# That is Dave.
```

  Notice that if you write it as a one-liner, you need the word "then", but for a multi-line response
  you should NOT use "then". In some other languages, you need to explicitly add a break (or similar)
  after each response so it doesn't "fall through" to the next comparison. In Ruby this is automatic,
  in the rare case that fall-through is a desired behavior, you'll have to set it up.
  There is one other related structure that you'll occasionally see called a Ternary. This is used when
  you have exactly one true or false decision and a succinct response. It comes in the form
  "comparison ? true_result : false_result" For instance:

```rb
$balance = 30

p $balance > 0 ? "We owe you." : "You owe us."
```
Of course this isn't a great example, what happens if $balance == 0 ?


  I wouldn't recommend jumping right into Ternary, but it will be important that you recognize when
  somebody uses them in code you're reading.
  A useful tip to know is that Ruby has a convention of writing question marks at the end of methods
  that return a boolean. For example "0,zero?" and "5.positive?" When writing a method that returns a
  boolean, keep this convention in mind.




#  While and Until
  The ability to create loops is another fundamental tool of any programming language. One of Ruby's
  biggest quirks that you'll notice first thing comes from the way "idiomatic" Ruby handles iteration.
  This is one place that we'll break conventions with idiomatic Ruby to talk about a lesser used,
  but efficient and familiar looping structure, the "while" loop. A basic example:

```rb
def print_times(word, times)
  x = 0
  while x < times
    print word
    x = x + 1
  end
end

print_times("Hello!", 5)

# Until works on the reverse logic.

def print_until(word, times)
  x = 0
  until x == times
    print word
    x = x + 1
  end
end

print_until("Hello!", 5)
```

  While I've written it out explicitly above, you'll rarely actually see "x = x + 1". Instead, there is
  a common shorthand.

```rb
def puts_count(count)
  x = 0
  while x < count
    x += 1
    puts x
  end
end

puts_count(10)
```

  Ruby has for loops, but I've barely ever seen one. There are other ways to express this that we'll cover
  shortly. If you must, you'll find the syntax online, it's about like c or python.



#  Beginning Blocks
  We'll start into our look at "blocks" by exploring Times and Each.
  Times is similar to while above, but will use a "block" to achieve the same thing. A block in Ruby can
  be a bit hard to define in a way that doesn't sound like a method, but blocks tend to be made to work
  procedurally over an array of data with minimal syntax. Let's look at an example that mimics behavior
  in our while loop from the last section.

```rb
def counting_block(count)
  count.times do |index|
    puts index + 1
  end
end

counting_block(5)

def multiply_all_by_two(count)
  count.times {|index| puts (index + 1) * 2}
end

multiply_all_by_two(5)
```

  Everything that comes after "times" in the above two examples are blocks. Inside of the pair of pipes,
  or goalposts | | , times will provide an iterator starting at 0. In both cases I've named this "index"
  though you will often see people use "i" here as is common in for loops.
  Notice that there is both a long and a short form. While both CAN work, it is standard to use {} for
  one line blocks while using do and end for multiline blocks.
  Another block you'll wind up seeing and using is "each". Before I say anything else about "each", it
  should be noted that this block is very attractive to use, but very expensive when used a lot. For
  now we'll look at how it works in order to build on the idea when we look at "map". You use "each"
  when you want to perform an operation on each element of an of array. For example:

```rb
$numbers = [3, 8, 2, 6, 1]
$numbers.each {|number| print number}

# 38261

$things = ["cat", "bat", "language by Matz"]
$things.each {|thing| puts "I have a #{thing}."}

# I have a cat.
# I have a bat.
# I have a language by Matz.
```

  Much like "times" provided an index from the | | , each provides each element. While these are simple
  and trivial examples to introduce you to blocks, the can be very powerful and complex array processors.
  As I said before, however, this can be a very expensive operation when a lot of data is involved, so do
  not rely on it. Using a while to access the index of an array can be more efficient. It's always about
  the right tool for the job.



#  Ranges and Step
  In addition to writing out a collection of data, yo may wish to programmatically generate it. For this
  we have Ranges. While ranges can exist in a few forms, you'll intially recognize them by a pair of
  numbers separated by two or three dots: (1..5)  (1...10) . These are an inclusiive and exclusive range,
  respectively. Let's find out what that means.

```rb
(1..10).each {|number| puts number}
(1...10).each {|number| puts number}
```

  In the first example above, "10" is printed. In the second example, it is not. The latter is "exclusive",
  meaning it excludes the final number. Pay close attention to the number of dots and think of a mnemonic
  to remind you early on, maybe that the final number has backed away and left a dot in its place.
  Beyond a simple value range, you can "chain" a method called step that will give you regular intervals of
  numbers in a range. For instance:

```rb
(0..20).step(2).each {|number| puts number}

# will give you every even number from 0 to 20, while

(3..24).step(3).each {|number| puts number}

# will give you every third number from 3 to 24
```

  "step" is the first "chained" method we've seen. First a range is generated, then step filters down the
  numbers by intervals of the argument, then each takes that array and puts each element of it. Method
  chains and blocks in conjunction can make for some very powerful expressions when practiced regularly.
  Listing every method is beyond the scope of this, but a lot of your Ruby progress will involve leraning
  how, when, and why to use powerful and concise syntax. We'll see a few practical examples at the end of
  the next section.



  We'll conclude the beginner section with an intermediate level method that you'll use frequently in
  DragonRuby, "map". On its surface, map is a lot like each, but they work in slightly different ways. The
  big difference with map is that it always returns an array of every evaluation from its input. Let's
  first look at a trivial example.

```rb
$num_array = (2..10).step(2).map {|num| num**2}
p $num_array

# [4, 16, 36, 64, 100]

$the_letters = ('a'..'z').map {|letter| "The letter #{letter}"}
p $the_letters

# ["The letter a", "The letter b", ... "The letter z"]
```

  The first example returns the square of every other number from 2 to 10. The second makes a range out
  of the alphabet, interpolates into into a message, and returns an array of the message repeated for
  each letter. While these examples are trivial, this is how you will start out building large numbers of
  primitives in Dragonruby, ready to directly feed the output arrays.
  I'll finish this off with two non-trivial examples that may come in handy. These are two methods I've
  made to convert between hex colors that you find online and the 3 decimal values that DragonRuby wants.
  There will be some new syntax here and I leave it as an exercise to you to figure out how they work.
  Everything can be found by googling or looking through the Ruby API, now is a good time to get to know
  how to do a lot of both. ;)

```rb
def hex_to_rgb(hex)
  hex.gsub("#", "").chars.each_slice(2).map {|e| e.join.to_i(16)}
end

def rgb_to_hex(rgb, prefix = '#')
  "#{prefix}#{rgb.map {|e| e.to_s(16).rjust(2, "0").upcase}.join}"
end

p hex_to_rgb '#FF00FF'
p rgb_to_hex [255, 0, 255]
```

{% include footer.html %}
