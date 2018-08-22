# Code School
### Level 1

- ```ruby
"Isil".reverse;
"Isil".length;
"Isil"*5
```

### Level 2

- reverse is not for integers but for strings.
- `.to_s`; `.to_i`; `.to_a`

- `[12, 47, 35].max`; `ticket.sort` vs `ticket.sort!`

### Level 3

- ```ruby
poem['toast'] = 'honeydew'
# (poem is a string.)
# []: I am looking for ... somewhere in here. target and find things.
poem.lines.to_a.reverse
print poem.lines.to_a.reverse.join
```

### Level 4

- ```ruby
poem.include? "my hand"
poem.downcase
poem.delete
```

- ```ruby
books = {} # (empty hash/ dictionary)
books["Gravity's Rainbow"] = :splendid
books
# => {"Gravity's Rainbow"=>:splendid}
# ratings (e.g., splendid) are not strings, *symbols*
books.length
books["Gravity's Rainbow"] # => :splendid
# Gravity's Rainbow = *key*; splendid = *value*
# books.keys: the list of hash.
```

- Block: a chunk of Ruby code surrounded by {}. And are always attached to methods:
```ruby
5.times {print "Odelay!"}
books.values.each { |rate| ratings[rate] += 1 }
```

### Level 5

- Dir.entries "/" : listing out everything in the top directory (called as **root**)
- Dir: has a collection of methods for checking out file directories.
- entries: is being called on the Dir variable. this method just lists everything in the directory you've indicated.

- print poem vs print "pre", "event" ; **attachment vs argument**

- Dir["/*.txt"]

- Level 5 challenge 4: print File.­read("/com­ics.txt"); FileUtils.­cp('/comic­s.txt', '/Hom­e/comics.t­xt');
- Level 5 challenge 5: File.open("/Home/comics.txt", "a") do |f| end

- File.mtime("/Home/comics.txt"): what time was it when you changed your file. # => 2017-01-09 19:25:36 UTC
- File.mtime­("/Home/co­mics.txt")­.hour # => 19
- mtime method gives a Ruby Time object.

### Level 6: Building your own method.

- Level 6 challenge 1
```ruby
def load_­comics(pat­h)
	comics = {}
	File.foreach(path) do |line|
    	name, url = line.split(': ')
    	comics[name] = url.strip
	end
	comics
end
```
comics = load_­comics('/c­omics.txt'­) # => {"Achewood"=>"http://achewood.com/", "Dinosaur Comics"=>"http://qwantz.com/", "Perry Bible Fellowship"=>"http://cheston.com/pbf/archive.html", "Get Your War On"=>"http://mnftiu.cc/"}

- Level 6 challenge 2: aciklamalar.

- Level 6 challenge 3

- ```ruby
Popup.make {
  h1 "My Links"
  link "Go to Bing", "http://bing.com"
}
```

- ```ruby
Popup.make do
  h1 "Things To Do"
  list do
    p "Try out Ruby"
    p "Ride a tiger"
    p "(down River Euphrates)"
  end
end
```

- ```ruby
Popup.make do
  h1 "Comics on the Web"
  list do
    comics.each do |name, url|
      link name, url
    end
  end
end
```

# Ruby in 100 Minutes (jumpstartlab)

### 1. Instructions

- In commandline: ruby my_program.rb
- In Irb: in terminal type irb

### 2. Variables

- Naming variables:(VM requirements) starting with lower case(or _ but uncommon); no spaces; no specific characters(like $, @, &)
- Rubyists prefer: snake_case, naming after meaning, non-abbreviated.

### 3. Strings

- **Substring and position**
```ruby
greeting = "Hello Everyone!"
greeting[0..2]
greeting[-1..-3]
```
- greeting.length; greeting.split (=> ["Hello", "Everyone!"]: default is splitting to each spaces) greeting.split("o") (=> ["Hell", " Every", "ne!"])

- ```ruby
greeting.gsub("Everyone!", "Friends!")
```

- **String concatenation/interpolation**
```ruby
name = "Frank"
puts "Good morning, " + name + "!"
puts "Good morning, #{name}!"

modifier = "very "
mood = "excited"
puts "I am #{modifier * 3 + mood} for today's class!"

### 4. Symbols

### 5. Numbers

- For loops are common, but they’re not very readable. Because Ruby’s integers are objects they have methods. One of those is the times method.

```ruby
5.times do
	puts "Hello, World!"
end

5.times{ puts "Hello, World!"}
```

### 6. Blocks

- They’re a parameter passed into a method call. If, for instance, we just called 5.times, Ruby wouldn’t know what we want to be done five times.
```ruby
"this is a sentence".gsub("e"){ puts "Found an E!"}
# Found an E!
# Found an E!
# Found an E!
# => "this is a sntnc"
```

- **Block parameters**
```ruby
5.times do |i|
  puts "#{i}: Hello, World!"
end
```
```ruby
"this is a sentence".gsub("e"){|letter| letter.upcase}
# => "this is a sEntEncE"
```

### 7. Arrays

```ruby
meals = ["Breakfast", "Lunch", "Dinner"]
meals << "Dinner"
# => ["Breakfast", "Lunch"]
meals[2]
meals.last
meals.sort
meals.join
meals.index
meals.each
meals.include?
meals.collect
meals.first
meals.shuffle
```

### 8. Hashes

```ruby
produce = {"apples" => 3, "oranges" => 1, "carrots" => 12}
puts "There are #{produce['oranges']} oranges in the fridge."
produce["oranges"] = 6
```
- when all the keys are symbols: (Notice that the keys end with a colon rather than beginning with one, even though these are symbols. This simplified syntax works with Ruby version 1.9 and higher.)

```ruby
produce = {apples: 3, oranges: 1, carrots: 12}
puts "There are #{produce[:oranges]} oranges in the fridge."
```

-----
###### How can we determine if key is a symbol or not? (e.g., apples)
-----

### 9. Conditionals

### 10. Nil & Nothingness

### 11. Objects, Attributes, and Methods

- Each piece of data is an **object**. Objects hold information, called *attributes*, and they can perform actions, called *methods*.

- In Object-Oriented programming we define **classes**, which are abstract descriptions of a category or type of thing. It defines what attributes and methods all objects of that type have.

- Defining a class namely Student and defining attributes by the method namely attr_accesor.
```ruby
class Student
  attr_accessor :first_name, :last_name, :primary_phone_number

  def introduction
    puts "Hi, I'm #{first_name}!"
  end
end
```
- Creating instances: Imagine you’re a student. You’re not an abstract concept, you’re an actual person. This actual person is an instance of Student - it is a realization of the abstract idea. It has actual data for the attributes first_name, last_name, and primary_phone_number.

```ruby
class Student
  attr_accessor :first_name, :last_name, :primary_phone_number

  def introduction(target)
    puts "Hi #{target}, I'm #{first_name}!"
  end

  def favorite_number
    7
  end
end

frank = Student.new
frank.first_name = "Frank"
frank.introduction('Katrina')
puts "Frank's favorite number is #{frank.favorite_number}."
```
# Learn To Program *Chris Pine*

### 1. Numbers

### 2. Letters

- 'pig' * 5 vs 5 * 'pig'. The former: 5 sets of 'pig': that is ok. The latter: 'pigs' set(s) of 5: an error.

### 3. Variables and Assignment

### 4. Mix it up

### 5. More About Methods

- clock.tick : "calling clock's  tick method," or that we "called tick on clock."
- ```ruby
5 + 5 = 5.+ 5
'Hello'.+ 'world!' = 'Hello' + 'world!'
```

- In Ruby, if I say puts 'to be or not to be', what I am really saying is self.puts 'to be or not to be'. So what is self? It's a special variable which points to whatever object you are in. We don't even know how to be in an object yet, but until we find out, we are always going to be in a big object which is... the whole program! And lucky for us, the program has a few methods of its own, like puts and gets.

```ruby
letters = 'aAbBcCdDeE'
puts letters.upcase
puts letters.downcase
puts letters.swapcase
puts letters.capitalize
puts ' a'.capitalize
puts letters

# AABBCCDDEE
# aabbccddee
# AaBbCcDdEe
# Aabbccddee
#  a
# aAbBcCdDeE
```

```ruby
lineWidth = 50
puts(                'Old Mother Hubbard'.center(lineWidth))
puts(               'Sat in her cupboard'.center(lineWidth))
puts(         'Eating her curds an whey,'.center(lineWidth))
puts(          'When along came a spider'.center(lineWidth))
puts(         'Which sat down beside her'.center(lineWidth))
puts('And scared her poor shoe dog away.'.center(lineWidth))

#                Old Mother Hubbard
#               Sat in her cupboard
#            Eating her curds an whey,
#             When along came a spider
#            Which sat down beside her
#        And scared her poor shoe dog away.
```

```ruby
lineWidth = 40
str = '--> text <--'
puts str.ljust  lineWidth
puts str.center lineWidth
puts str.rjust  lineWidth
puts str.ljust(lineWidth/2) + str.rjust(lineWidth/2)

#--> text <--
#              --> text <--
#                            --> text <--
#--> text <--                --> text <--
```

- **#{variable} kullanirken ' ' vs " "**

```ruby
lineWidth = 75
chp = 'Chapter '
p = 'page '
puts 'Table Of Contents'.center lineWidth
puts ''
puts "#{chp}1:  Numbers".ljust(lineWidth/2) + '#{p}1'.rjust(lineWidth/2)

#                             Table Of Contents

# Chapter 1:  Numbers                                                  #{p}1
```
```ruby
puts 5**2
puts 5**0.5
puts((5-2).abs)
puts((2-5).abs)

# 25
# 2.23606797749979
# 3
# 3
```

```ruby
puts rand
puts(rand(100))
puts(rand(1))
puts('The weatherman said there is a '+rand(101).to_s+'% chance of rain,')
puts(rand(3..8)) # between two number

# 0.5357456897902644. Default is bet 0.0-1.0
# 82 If there is a parameter, then it will be the same type of it.
# 0 Always gives 0 as an output.
# The weatherman said there is a 9% chance of rain, but you can never trust a weatherman.
# 5
```
```ruby
srand 1776
puts(rand(100))
puts(rand(100))
puts(rand(100))
puts ' '
srand 1776
puts(rand(100))
puts(rand(100))
puts(rand(100))

# 24
# 35
# 36

# 24
# 35
# 36
```
```ruby
puts(Math::PI)
puts(Math::E)
puts(Math.cos(Math::PI/3))
puts(Math.tan(Math::PI/4))
puts(Math.log(Math::E**2))
puts((1 + Math.sqrt(5))/2)

# 3.141592653589793
# 2.718281828459045
# 0.5000000000000001
# 0.9999999999999999
# 2.0
# 1.618033988749895
```
### 6. Flow Control

```ruby
puts 1>2
puts 1<2
puts 'cat' < 'dog'
puts 'Zoo' < 'ant' # Capital letter comes first.

# false
# true
# true
# true
```

### 7. Arrays & Iterators

```ruby
languages = ['English', 'Ruby']

languages.each do |lang|
  puts 'I love ' + lang + '!'
  puts 'Don\'t you?'
end

# I love English!
# Don't you?
# I love Ruby!
# Don't you?
```

- Methods like each which "act like" loops are often called iterators. One thing to notice about iterators is that they are always followed by do...end.  while and if never had a do near them; we only use do with iterators.
```ruby
3.times do
  puts 'Hip-Hip-Hooray!'
end
```

```ruby
foods = ['artichoke', 'brioche', 'caramel']

puts foods
puts
puts foods.to_s
puts
puts foods.join(', ')
puts
puts foods.join('  :)  ') + '  8)'

200.times do
  puts []
end

# artichoke
# brioche
# caramel

# ["artichoke", "brioche", "caramel"]

# artichoke, brioche, caramel

# artichoke  :)  brioche  :)  caramel  8)
```
```ruby
favorites = []
favorites.push 'raindrops on roses'
favorites.push 'whiskey on kittens'

puts favorites[0]
puts favorites.last
puts favorites.length

puts favorites.pop
puts favorites
puts favorites.length

# raindrops on roses
# whiskey on kittens
# 2
# whiskey on kittens
# raindrops on roses
# 1
```
- For swapping the elements due to the alphabetical order; see manyWordsWithoutSortMethod.rb.
- For splitting a string and transforming it into an array also see manyWordsToType.rb

### 8. Writing Your Own Methods

------
- But don't methods always have to be associated with objects? Well, yes they do, and in this case (as with puts and gets), **the method is just associated with the object representing the whole program.** In the next chapter we'll see how to add methods to other objects. **when we use objects but the hole program as an object?**

- a = 3. **puts a vs puts a.to_s** Sam for split method using in strings. see manyWordsToType.rb

----

```ruby
returnVal = puts 'This puts returned:'
puts returnVal

# This puts returned:
#
```
- The first puts didn't seem to return anything, and in a way it didn't; it returned nil. Though we didn't test it, the second puts did, too;  puts always returns nil. hEvery method has to return something, even if it's just nil.

- ```ruby
2.2.4 :001 >
2.2.4 :002 >   def sayMoo numberOfMoos
2.2.4 :003?>   puts 'moooo...'*numberOfMoos
2.2.4 :004?>   'yellow submarine'
2.2.4 :005?>   end
 => :sayMoo
2.2.4 :006 > x = sayMoo 2
moooo...moooo...
 => "yellow submarine"
2.2.4 :007 > puts x
yellow submarine
 => nil
2.2.4 :008 >  def sayMoo numberOfMoos
2.2.4 :009?>   'yellow submarine'
2.2.4 :010?>   puts 'moooo...'*numberOfMoos
2.2.4 :011?>   end
 => :sayMoo
2.2.4 :012 > x = sayMoo 2
moooo...moooo...
 => nil
2.2.4 :013 >
2.2.4 :014 >   puts x

 => nil
2.2.4 :015 >
```
- Were you surprised? Well, here's how it works: the value returned from a method is simply the last line of the method. In the case of sayMoo, this means it returns puts 'mooooooo...'*numberOfMoos, which is just  nil since puts always returns nil. If we wanted all of our methods to return the string 'yellow submarine', we would just need to put that at the end of them.

### 9. Classes

```ruby
a = Array.new  + [12345]  # Array  addition.
b = String.new + 'hello'  # String addition.
c = Time.new

puts 'a = '+a.to_s
puts 'b = '+b.to_s
puts 'c = '+c.to_s

# a = [12345]
# b = hello
# c = 2016-01-29 11:35:38 -0800
```

```ruby
time  = Time.new   # The moment I generated this web page.
time2 = time + 60  # One minute later.

puts time
puts time2

# 2016-01-29 11:35:38 -0800
# 2016-01-29 11:36:38 -0800
```
```ruby
puts Time.mktime(2000, 1, 1)          # Y2K.
puts Time.mktime(1976, 8, 3, 10, 11)  # When I was born.

# 2000-01-01 00:00:00 -0800
# 1976-08-03 10:11:00 -0700
```

```ruby
colorHash['strings']  = 'red'
colorHash['numbers']  = 'green'
colorHash['keywords'] = 'blue'
colorHash.each do |codeType, color|
  puts codeType + ':  ' + color
end

# strings:  red
# numbers:  green
# keywords:  blue
```
- **Extending Classes** At the end of the last chapter, you wrote a method to give the English phrase for a given integer. It wasn't an integer method, though; it was just a generic "program" method. Wouldn't it be nice if you could write something like 22.to_eng instead of englishNumber 22? Here's how you would do that:

```ruby
class Integer
  def to_eng
    if self == 5
      english = 'five'
    else
      english = 'fifty-eight'
    end

    english
  end
end

puts 5.to_eng
puts 58.to_eng

# five
# fifty-eight
```
**Class integer diye yazmamiz neyi degistiriyor?**

```ruby
class Die

  def roll
    1 + rand(6)
  end

end

dice = [Die.new, Die.new]

dice.each do |die|
  puts die.roll
end

# 6
# 2
```
- So instance variables are just an object's variables. A method's local variables last until the method is finished. An object's instance variables, on the other hand, will last as long as the object does. To tell instance variables from local variables, they have @ in front of their names:

```ruby
class Die

  def roll
    @numberShowing = 1 + rand(6)
  end

  def showing
    @numberShowing
  end

end

die = Die.new
die.roll
puts die.showing
puts die.showing
die.roll
puts die.showing
puts die.showing

# 4
# 4
# 6
# 6
```
```ruby
# On the above programme: puts Die.new.showing =>   ; nil

class Die

  def initialize
    # I'll just roll the die, though we
    # could do something else if we wanted
    # to, like setting the die with 6 showing.
    roll
  end

  def roll
    @numberShowing = 1 + rand(6)
  end

  def showing
    @numberShowing
  end

end

puts Die.new.showing

# 1
```
- When an object is created, its initialize method (if it has one defined) is always called.

- To see a detsiled example see https://pine.fm/LearnToProgram/chap_09.html , the Dragon example

### 10. Blocks and Procs

- It's the ability to take a block of code (code in between do and end), wrap it up in an object (called a proc), store it in a variable or pass it to a method. it's kind of like a method itself, except that it isn't bound to an object (it is an object), and you can store it or pass it around like you can with any object.

```ruby
toast = Proc.new do
  puts 'Cheers!'
end

toast.call

# Cheers!
```

```ruby
doYouLike = Proc.new do |aGoodThing|
  puts 'I *really* like '+aGoodThing+'!'
end

doYouLike.call 'chocolate'
doYouLike.call 'ruby'

# I *really* like chocolate!
# I *really* like ruby!
```

- **Methods which take procs**

```ruby
def doSelfImportantly someProc
  puts 'Everybody just HOLD ON!  I have something to do...'
  someProc.call
  puts 'Ok everyone, I\'m done.  Go on with what you were doing.'
end

sayHello = Proc.new do
  puts 'hello'
end

sayGoodbye = Proc.new do
  puts 'goodbye'
end

doSelfImportantly sayHello
doSelfImportantly sayGoodbye

# Everybody just HOLD ON!  I have something to do...
# hello
# Ok everyone, I'm done.  Go on with what you were doing.
# Everybody just HOLD ON!  I have something to do...
# goodbye
# Ok everyone, I'm done.  Go on with what you were doing.
```

```ruby
def maybeDo someProc
  if rand(2) == 0
    someProc.call
  end
end

def twiceDo someProc
  someProc.call
  someProc.call
end

wink = Proc.new do
  puts '<wink>'
end

glance = Proc.new do
  puts '<glance>'
end

maybeDo wink
maybeDo glance
twiceDo wink
twiceDo glance

# <wink>
# <wink>
# <glance>
# <glance>
```
```ruby
def doUntilFalse firstInput, someProc
  input  = firstInput
  output = firstInput

  while output
    input  = output
    output = someProc.call input
  end

  input
end

buildArrayOfSquares = Proc.new do |array|
  lastNumber = array.last
  if lastNumber <= 0
    false
  else
    array.pop                         # Take off the last number...
    array.push lastNumber*lastNumber  # ...and replace it with its square...
    array.push lastNumber-1           # ...followed by the next smaller number.
  end
end

alwaysFalse = Proc.new do |justIgnoreMe|
  false
end

puts doUntilFalse([5], buildArrayOfSquares).inspect
puts doUntilFalse('I\'m writing this at 3:00 am; someone knock me out!', alwaysFalse)

# [25, 16, 9, 4, 1, 0]
# I'm writing this at 3:00 am; someone knock me out!
```
- Methods Which Return Procs ar not so common:

```ruby
def compose proc1, proc2
  Proc.new do |x|
    proc2.call(proc1.call(x))
  end
end

squareIt = Proc.new do |x|
  x * x
end

doubleIt = Proc.new do |x|
  x + x
end

doubleThenSquare = compose doubleIt, squareIt
squareThenDouble = compose squareIt, doubleIt

puts doubleThenSquare.call(5)
puts squareThenDouble.call(5)

# 100
# 50
```
- 3 steps: defining the method, making the proc, calling the method with proc. it sort of feels like there should only be two (defining the method, and passing the block right into the method, without using a proc at all), since most of the time you don't want to use the proc/block after you pass it into the method. Well, wouldn't you know, Ruby has it all figured out for us! In fact, you've already been doing it every time you use iterators:

```ruby
class Array
  def eachEven(&wasABlock_nowAProc)
    # We start with "true" because arrays start with 0, which is even.
    isEven = true

    self.each do |object|
      if isEven
        wasABlock_nowAProc.call object
      end

      isEven = (not isEven)  # Toggle from even to odd, or odd to even.
    end
  end
end

['apple', 'bad apple', 'cherry', 'durian'].eachEven do |fruit|
  puts 'Yum!  I just love '+fruit+' pies, don\'t you?'
end

# Remember, we are getting the even-numbered elements
# of the array, all of which happen to be odd numbers,
# just because I like to cause problems like that.
[1, 2, 3, 4, 5].eachEven do |oddBall|
  puts oddBall.to_s+' is NOT an even number!'
end

# Yum!  I just love apple pies, don't you?
# Yum!  I just love cherry pies, don't you?
# 1 is NOT an even number!
# 3 is NOT an even number!
# 5 is NOT an even number!
```

```ruby
def profile descriptionOfBlock, &block
  startTime = Time.now

  block.call

  duration = Time.now - startTime

  puts descriptionOfBlock+':  '+duration.to_s+' seconds'
end

profile '25000 doublings' do
  number = 1

  25000.times do
    number = number + number
  end
# Show the number of digits in this HUGE number.
  puts number.to_s.length.to_s+' digits'
end

profile 'count to a million' do
  number = 0

  1000000.times do
    number = number + 1
  end
end

# 7526 digits
# 25000 doublings:  0.055202 seconds
# count to a million:  0.073473 seconds
```

```ruby
def doItTwice(&block)
  block.call
  block.call
end

doItTwice do
  puts 'murditivent flavitemphan siresent litics'
end

#def doItTwice
#  yield
#  yield
#end

#doItTwice do
#  puts 'buritiate mustripe lablic acticise'
#end
```

`
Variable names cannot begin with a capital letter. If an identifier begins with a capital letter, it is considered to be a constant in Ruby.
`
- **Map** & **Each**
```ruby
[1, 2, 3].map { |n| n * n }
#=> [1, 4, 9]
```

```ruby
names = ['danil', 'edmund']

# here we map one array to another, convert each element by some rule
names.map! {|name| name.capitalize } # now names contains ['Danil', 'Edmund']

names.each { |name| puts name + ' is a programmer' } # here we just do something with each element

# The output: Danil is a programmer
# Edmund is a programmer
```

- **Inject** Takes an accumulator (sum) and changes it as many times as there are elements in the array. Returns the final value of the accumulator.

```ruby
[1,2,3,4,5].inject({}) do |hash, item|
  hash[item] = item * item
  hash
end

# {1=>1, 2=>4, 3=>9, 4=>16, 5=>25}
```

```ruby
[1,"a",Object.new,:hi].inject({}) do |hash, item|
  hash[item.to_s] = item
  hash
end

# {"1"=>1, "a"=>"a", "#<Object:0x007fc7f90ed760>"=>#<Object:0x007fc7f90ed760>, "hi"=>:hi}
```

```ruby
# Specifying initial value as parameter before the block
["bar","baz","quux"].inject("foo") {|acc,elem| acc + "!!" + elem }
# returns "foo!!bar!!baz!!quux"
```

**array.inject{|sum,e| sum += e} VS array.inject(0){|sum,e| sum += e}**
the former returns nil if array is empty; the latter returns 0

- `collect` alias for `map`
- `reduce` alias for `inject`

```ruby
[1,2,3,4].reduce(&:+)
# => 10
[1,2,3,4].reduce(100, &:+)
# => 110
```

- **Select** Runs an expression for each array element and, if it is `true`, that element gets added to the output which is returned. This is called filter in other languages.
```ruby
[1,2,3,4,5,6,7,8,9,10].select{|el| el%2 == 0 }
# returns [2,4,6,8,10]
```

- **Find** Take an expression and returns the first element for which the expression returns `true`
```ruby
[1,2,3,4,5,6,7,8,9,10].find{|el| el % 2 == 1 }
# returns 1
```

- `detect` alias for `find`

- **Reject** The opposite of select: runs an expression for each array element and includes that element in the output if the expression is `false`

```ruby
[1,2,3,4,5,6,7,8,9,10].reject{|e| e==2 || e==8 }
# returns [1, 3, 4, 5, 6, 7, 9, 10]
```

- For detailed explanations check on [this link](http://queirozf.com/entries/ruby-map-each-collect-inject-reject-select-quick-reference)

- **Default value**

```ruby
def some_method(a, b, c=25)
end

some_method(25,"hello")

some_method(25,"hello", 48)

# In the first case you don’t supply a value for the third parameter, so it’s default value (i.e. 25) will be used in the method body. In  the second case you do supply a value, so it will be used in place of the default value.
```

```
describe "repeat" do
  it "should repeat" do
    expect(repeat("hello")).to eq("hello hello")
  end

  it "should repeat a number of times" do
    expect(repeat("hello", 3)).to eq("hello hello hello")
  end
end

def repeat (string, no = 2)
  (string.split * no).join(" ")
end
```

```ruby
def titleize (string)
  array = string.capitalize.split
  little_words = ["the", "over", "and"]
  array.map! { |element|
    if little_words.include?(element)
      element
    else
      element.capitalize
    end}
  array.join(" ")
end
```

-  attr_reader & attr_writer & attr_accessor [From codecademy](https://www.codecademy.com/en/forum_questions/50f0192b102455349200372d)

Well, attr_reader and attr_writer are connected in some way to private and public.

You use private and public for methods. So with private and public you can make methods accessible or not outside of the class.

With instance variables, you can make them accessible or not with attr_reader and attr_writer outside of the class.

Let's use this example:

```ruby
class Person
  def initialize(name)
    @name = name
  end
end
```

Let's say you create one Person
p1 = Person.new("John")
With the above class there is no way to change the name John to anything else. You would need to create another Person object with different name. Sometimes that is what you want and by not using attr_reader and attr_writer you are achieving that.

Now let's look at this:

```ruby
class Person
  attr_reader :name
  attr_writer :name
  def initialize(name)
    @name = name
  end
end
```

Now we can change the name of our Person (p1.name = "Other Name") without creating another Person object.

OR, if you want you can use methods for reaching instance variables instead of attr_reader and attr_writer but that is not in Rubys style since it is more code
Example:

```ruby
class Person
  def initialize(name)
    @name = name
  end

  def name
    @name
  end

  def name=(value)
    @name = value
  end
end
```

- **Metaclass** is a class whose instances are classes. Just as an ordinary class defines the behaviour of certain objects, a metaclass defines the behavior of certain classes and their instances.

#### What is an interpreted language? What is a compiled language?

An interpreted language is a programming language for which most of its implementations execute instructions directly, without previously compiling a program into machine-language instructions.

An compiled language is a programming language whose implementations are typically compilers (translators that generate machine code from source code), and not interpreters (step-by-step executors of source code, where no pre-runtime transltaion takes place)

#### Machine code vs Source code

Machine code is the directly executable binary representation of a computer program. ... Object code is the result of compilation of a module or program written in a programming language, stored for later use. Source code is a program written in a programming language (or in assembly language).


```ruby
class Onur
  attr_accessor :age
  def age=(value)
    puts "in age="
    @age = value
  end

  def age
    puts "in age"
    @age
  end

  def set_age(value)
    # self.age # => in age value
    # self.age = value # => in age= value
    @age = value
  end

end
```

```ruby
def title=(value)
  @title = value
end

# book.title = "x". Can be considered as calling

def title
  @title
end

# book.title . Can be considered as calling.
```

-----------------------

> To understand Bundler's set-up process check this [link](https://www.brianstorti.com/understanding-bundler-setup-process/)
















