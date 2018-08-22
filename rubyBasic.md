# Codecademy [Learn Ruby](https://www.codecademy.com/en/courses/learn-ruby/lessons/introduction-to-ruby/exercises/overview--sneak-peek)

## Intro to Ruby

- **Interpreted**: you don't need a compiler to write and run Ruby. *vs non-interpreted ones*

- **Object-oriented**: users can manipulate data structures to build and execute programs. Everything in Ruby is an object. *not object-oriented languages*

- **Case-sensitive**: *not case-sensitive languages*

- **puts vs print:**
The `print` command just takes whatever you give it and prints it to the screen. `puts` adds a new (blank) line after the thing you want it to print.

- Multi-line comments
```
=begin
I'm a comment!
I don't need any # symbols.
=end
```

- By convention, local variable names should start with a lowercase letter and words should be separated by underscores (e.g. this_variable).

- **gets.chomp:** When getting input, Ruby automatically adds a blank line (or newline) after each bit of input; `chomp` removes that extra line. (Your program will work fine without `chomp`, but you'll get extra blank lines everywhere.)

## Control Flow

- The kinds of program can take user input, but they always produce the same result based on that input; they don't change their behavior in reaction to the **environment** (the collection of all variables and their values that exist in the program at a given time). **Control flow** gives us the flexibility we're looking for.

- Ruby's `if` statement takes an **expression**, which is just a fancy word for something that has a value that evaluates to either `true` or `false`.

- Ruby doesn't care about **whitespace** (spaces and blank lines), so the indentation of the print statement isn't *necessary*. However, it's a convention that Rubyists (Ruby enthusiasts) follow, so it's good to get in the habit now. The block of code following an `if` should be indented two spaces.

- assignment operator: '='; comparator (also called a relational operator): '=='

- logical or boolean operators: ruby has three: **&&**, **||** (called as inclusive or), **!** (e.g. `2 != 3`; `!(false)` )

```ruby
print "Thtring, pleathe!: "
user_input = gets.chomp
user_input.downcase!

if user_input.include? "s"
  user_input.gsub!(/s/, "th") # gsub method stands for global substitution
else
  puts "Nothing to do here!"
end

puts "Your string is: #{user_input}"
```
> When we get to later lessons, we'll explain why the **/s/** has to be between slashes instead of between quotes. Note: you *cannot* put a space between **gsub!** and the bit in parentheses.

## Looping

- **Until**
```ruby
i = 0
until i == 6
  i += 1 # +=, -=, *=, /=
end
puts i
```

- **1..3** vs **1...3**: the former includes 3 the latter does not.
```ruby
for num in 1..10
  puts num
end
```

- **loop** method
```ruby
loop { print "Hello, world!" }
```

- **break** keyword
```ruby
i = 0
loop do
  i += 1
  print "#{i}"
  break if i > 5
end
```

- **next** keyword

```ruby
# if we don't want to print out the even numbers, we can write:

for i in 1..5
  next if i % 2 == 0
  print i
end
```

- **.each** method: The **loop** iterator is the simplest, but also one of the least powerful. A more useful iterator is the .each method, which can apply an expression to **each** element of an object, one at a time.

```ruby
object.each { |item|
  # Do something
}
```
You can also use the **do** keyword instead of **{}**
```ruby
object.each do |item|
  # Do something
end
```
The variable name between `| |` can be anything you like: it's just a placeholder for each element of the object you're using `.each` on.

- **.times** method is like a super compact **for** loop: it can perform a task on each item in an object a specified number of times.
```ruby
10.times { print "Chunky bacon!" }
```

- **.split**: it takes in a string and returns an array. If we pass it a bit of text in parentheses, .split will divide the string wherever it sees that bit of text, called a *delimiter*. (e.g. `text.split(",")` tells Ruby to split up the string `text` whenever it sees a comma)

## Arrays and Hashes

- Arrays of arrays are called *multidimensional* arrays.

- Hashes are sort of like JavaScript objects or Python dictionaries. If you haven't studied those languages, all you need to know that a hash is a collection of *key-value pairs*.

```ruby
my_hash = Hash.new
your_hash = {}
# `Hash` must be capitalized, or Ruby won't know what you're talking about!
```

```ruby
family = { "Homer" => "dad",
  "Marge" => "mom"}

family.each { |x, y| puts "#{x}: #{y}" }
```
- Hash has a default value:

```ruby
h = Hash.new("nothing here")

puts h
# {}

puts h["kitty"]
# nothing here
```
If you have a hash with a default value, and you try to access a non-existent key, you get that default value.

- Sorting by

```ruby
colors = {
  "blue" => 3,
  "green" => 1,
  "red" => 2
}
colors = colors.sort_by do |color, count|
  count
end
colors.reverse!
```

## Methods, Blocks, Sorting

- If a method takes arguments, we say it *accepts* or *expects* those arguments.

- **Parameter** vs **argument**

```ruby
def square(n)
  puts n ** 2
end

square(12)
```
The *argument* is the piece of code you actually put between the method's parentheses when you call it, and the *parameter* is the name you put between the method's parentheses when you *define* it. For instance, when we defined `square` above, we gave it the parameter **n** (for "number") and passed it the argument **12** when we called it.

- **Splat** arguments are arguments preceded by a *****, which tells the program that the method can receive one or more arguments.

```ruby
def what_up(greeting, *friends)
  friends.each { |friend| puts "#{greeting}, #{friend}!" }
end

what_up("What up", "Ian", "Zoe", "Zenas", "Eleanor")
```

- You can think of blocks as a way of creating methods that don't have a name. (These are similar to anonymous functions in JavaScript or lambdas in Python.)

- **The Combined Comparison (Spaceship) Operator** looks like this: ** <=>**. It returns **0** if the first operand (item to be compared) equals the second, **1** if the first operand is greater than the second, and **-1** if the first operand is less than the second. A block that is passed into the **sort** method must return either **1**, **0**, or **-1**. It should return **-1** if the first block parameter should come before the second, **1** if vice versa, and **0** if they are of equal weight, meaning one does not come before the other (i.e. if two values are equal)

```ruby
books = ["Charlie and the Chocolate Factory", "War and Peace", "Utopia", "A Brief History of Time", "A Wrinkle in Time"]

# To sort our books in ascending order, in-place
books.sort! { |firstBook, secondBook| firstBook <=> secondBook }

books.sort! { |firstbook, secondbook|
  secondbook <=> firstbook
  }
# Sort your books in descending order, in-place below

```

```ruby
fruits = ["orange", "apple", "banana", "pear", "grapes"]

fruits.sort! do |fruit1, fruit2|
   fruit2 <=> fruit1
end

# to sort the fruits array in descending (that is, reverse) alphabetical order.
```

```ruby
def alphabetize(arr, rev=false)
  if rev
    arr.sort { |item1, item2| item2 <=> item1 }
  else
    arr.sort { |item1, item2| item1 <=> item2 }
  end
end

books = ["Heart of Darkness", "Code Complete", "The Lorax", "The Prophet", "Absalom, Absalom!"]

puts "A-Z: #{alphabetize(books)}"
puts "Z-A: #{alphabetize(books, true)}"

```
What this does is tell Ruby that **alphabetize** has a second parameter, **rev** (for "reverse") that will *default* to **false** if the user doesn't type in two arguments.

## Hashes and Symbols

- Along with `false`, `nil` is one of two non-`true` values in Ruby. (Every other object is regarded as "truthy," meaning that if you were to type `if 2` or `if "bacon"`, the code in that **if** statement would be **run**.)

- You can **specify a default** like so:

```ruby
my_hash = Hash.new("Trady Blix")
```

- Those funny-looking variables that start with colons are **symbols**.

```ruby
menagerie = { :foxes => 2,
  :giraffe => 1,
  :weezards => 17,
  :elves => 1,
  :canaries => 4,
  :ham => 1
}
```

- Above and beyond the different syntax, there's a key behavior of symbols that makes them different from strings. While there can be multiple different strings that all have the same value, there's only one copy of any particular symbol at a given time.

```ruby
puts "string".object_id
puts "string".object_id

puts :symbol.object_id
puts :symbol.object_id
```
The `.object_id` method gets the ID of an object—it's how Ruby knows whether two objects are the exact same object. Run the code in the editor to see that the two `"strings"` are actually different objects, whereas the `:symbol` is the *same object* listed twice.

- **Syntax:** Symbols always start with a colon (:). They must be valid Ruby variable names, so the first character after the colon has to be a letter or underscore (_); after that, any combination of letters, numbers, and underscores is allowed.

- **What are Symbols Used For?** Symbols pop up in a lot of places in Ruby, but they're primarily used either as hash keys or for referencing method names.

- Symbols make good hash keys for a few reasons:
  1. They're immutable, meaning they can't be changed once they're created;
  2. Only one copy of any symbol exists at a given time, so they save memory;
  3. Symbol-as-keys are faster than strings-as-keys because of the above two reasons.

- **Converting btw Symbols and Strings**

```ruby
:sasquatch.to_s
# ==> "sasquatch"

"sasquatch".to_sym
# ==> :sasquatch
```
```ruby
strings = ["HTML", "CSS", "JavaScript", "Python", "Ruby"]

symbols = []

strings.each do |s|
  symbols.push(s.to_sym)
end

print symbols
```

```ruby
"hello".intern
# ==> :hello
```

- The hash syntax changed. If you're used to JavaScript objects or Python dictionaries, it will look very familiar:

```ruby
new_hash = {
  one: 1,
  two: 2,
  three: 3
}

# Notice the colon is at the end (not at the beginning); and no need the hash rocket anymore.
```
> It's important to note that even though these keys have colons at the end instead of the beginning, they're still symbols!

```ruby
grades = { alice: 100,
  bob: 92,
  chris: 95,
  dave: 97
}

grades.select { |name, grade| grade <  97 }
# ==> { :bob => 92, :chris => 95 }

grades.select { |k, v| k == :alice }
# ==> { :alice => 100 }
```

- Can we iterate over *just keys* or *just values*? `.each_key` and `.each_value`

```ruby
my_hash = { one: 1, two: 2, three: 3 }

my_hash.each_key { |k| print k, " " }
# ==> one two three

my_hash.each_value { |v| print v, " " }
# ==> 1 2 3
```

- **If/else/elsif** vs **case**: if and else are powerful, but we can get bogged down in ifs and elsifs if we have a lot of conditions to check. Thankfully, Ruby provides us with a concise alternative: the case statement. The syntax looks like this:

```ruby
case language
  when "JS"
    puts "Websites!"
  when "Python"
    puts "Science!"
  when "Ruby"
    puts "Web apps!"
  else
    puts "I don't know!"
end
```

- Movie list: add, display, update, delete

```ruby
movies = {
  Memento: 3,
  Primer: 4,
  Ishtar: 1
}

puts "What would you like to do?"
puts "-- Type 'add' to add a movie."
puts "-- Type 'update' to update a movie."
puts "-- Type 'display' to display all movies."
puts "-- Type 'delete' to delete a movie."

choice = gets.chomp.downcase
case choice
when 'add'
  puts "What movie do you want to add?"
  title = gets.chomp
  if movies[title.to_sym].nil?
    puts "What's the rating? (Type a number 0 to 4.)"
    rating = gets.chomp
    movies[title.to_sym] = rating.to_i
    puts "#{title} has been added with a rating of #{rating}."
  else
    puts "That movie already exists! Its rating is #{movies[title.to_sym]}."
  end
when 'update'
  puts "What movie do you want to update?"
  title = gets.chomp
  if movies[title.to_sym].nil?
    puts "Movie not found!"
  else
    puts "What's the new rating? (Type a number 0 to 4.)"
    rating = gets.chomp
    movies[title.to_sym] = rating.to_i
    puts "#{title} has been updated with new rating of #{rating}."
  end
when 'display'
  movies.each do |movie, rating|
    puts "#{movie}: #{rating}"
  end
when 'delete'
  puts "What movie do you want to delete?"
  title = gets.chomp
  if movies[title.to_sym].nil?
    puts "Movie not found!"
  else
    movies.delete(title.to_sym)
    puts "#{title} has been removed."
  end
else
  puts "Sorry, I didn't understand you."
end
```

## Refactoring: The Zen of Ruby

Refactoring is just a fancy way of saying we're improving the structure or appearance of our code without changing what it actually does.

```ruby
ruby_is_eloquent = true
ruby_is_ugly = false

puts "Ruby is eloquent!" if ruby_is_eloquent
puts "Ruby's not ugly!" unless ruby_is_ugly

# Ruby is eloquent!
# Ruby's not ugly!
```
**If** and **unless**: If the *do something* is a short, simple expression, however, we can move it up into a single line (as you saw in the last exercise). The syntax looks like this:

```
expression if boolean

puts "It's true!" if true

# but not this:

if true puts "It's true!"
```
- An even more concise version of **If/else** is the ternary conditional expression. It's called "ternary" because it takes three arguments: a boolean, an expression to evaluate if the boolean is `true`, and an expression to evaluate if the boolean is `false`.

```ruby
isil = true
puts isil ? "Hey isil" : "Hey Onur"

puts 3 < 4 ? "3 is less than 4!" : "3 is not less than 4."
```

- **when** and **then**: `case` example above can be written as the following:

```ruby
case language
  when "JS" then puts "Websites!"
  when "Python" then puts "Science!"
  when "Ruby" then puts "Web apps!"
  else puts "I don't know!"
end
```

- **Conditional Assignment Operator**: what if we only want to assign a variable if it hasn't already been assigned? For this, we can use the conditional assignment operator: `||=` :

```ruby
favorite_book = nil
puts favorite_book

favorite_book ||= "Cat's Cradle"
puts favorite_book

favorite_book ||= "Why's (Poignant) Guide to Ruby"
puts favorite_book # it won't change because our variable already has a value

favorite_book = "Why's (Poignant) Guide to Ruby"
puts favorite_book

#
# Cat's Cradle
# Cat's Cradle
# Why's (Poignant) Guide to Ruby
```

- **What if we don't put a return statement in our method definition, though?** For instance, if you don't tell a JavaScript function exactly what to return, it'll return undefined. For Python, the default return value is None. But for Ruby, it's something different: Ruby's methods will return the result of the last evaluated expression. This means, you can write this method:

```ruby
def add(a,b)
  return a + b
end
```
as simply follows:

```ruby
def add(a,b)
  a + b
end
```
Also;

```ruby
isil = true
isil ?  "Hey isil" : "Hey Onur"

#  => "Hey isil"
```

- **Short-circuit Evaluation**: That means that Ruby doesn't look at both expressions unless it has to; if it sees:

```
false && true
```
it stops reading as soon as it sees `&&` because it knows `false &&` anything *must* be false. To see this check out the following code:

```ruby
def a
  puts "A was evaluated!"
  return true
end

def b
  puts "B was also evaluated!"
  return true
end

puts a || b
puts "------"
puts a && b

# A was evaluated!
# true
# ------
# A was evaluated!
# B was also evaluated!
# true
```

- **for** vs **.times**: If we want to do something a specific number of times, we can use the `.times` method, like so:

```ruby
5.times { puts "Odelay!" }
```

- **for** vs **.each**: If we want to repeat an action for every element in a collection, we can use `.each`:

```
[1, 2, 3].each { |x| puts x * 10 }
```

- `even?` method:

```ruby
my_array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

my_array.each {|n| puts n if n.even?}
# or
# my_array.each {|n| puts n if n % 2 == 0}
```

- **for** vs **.upto** and **.downto**: This is a much more Rubyist solution than trying to use a `for` loop that stops when a counter variable hits a certain value or that prints out a specific range of values:

```ruby
95.upto(100) { |num| print num, " " }
# Prints 95 96 97 98 99 100

"L".upto("P") {|letter| puts letter }
# Puts L M N O P
```

- **Symbols are awesome for referencing method names**: Well, `.respond_to?` takes a symbol and returns `true` if an object can receive that method and `false` otherwise. For example,

```ruby
[1, 2, 3].respond_to?(:push)
# would return true, since you can call .push on an array object. However,

[1, 2, 3].respond_to?(:to_sym)
# would return false, since you can't turn an array into a symbol.

age = 26
age.respond_to?(:next)
# Rather than checking to see if our age variable is an integer, check to see if it will .respond_to? the .next method.
```

- **.push** vs **<<**: Instead of typing out the `.push` method name, you can simply use `<<`, the **concatenation operator** (also known as "the shovel") to add an element to the end of an array:

```ruby
[1, 2, 3] << 4
# ==> [1, 2, 3, 4]

"Yukihiro " << "Matsumoto"
# ==> "Yukihiro Matsumoto"
```
> It basically works as same as plain old +

- **String Interpolation**. The syntax looks like this:

```ruby
"I am #{age} years old."

# The one on the above is a better way rather than this:

"I am " << age.to_s << " years old."
```

- `.nil?` **vs** `||=`:

```ruby
prime_array = [] if prime_array.nil?

# VS

prime_array ||= []

# It is better to use conditional assignment.
```

## Blocks, Procs, and Lambdas

- **Collect method**

```
my_nums = [1, 2, 3]
my_nums.collect { |num| num ** 2 }
# ==> [1, 4, 9]

my_nums
# ==> [1, 2, 3]
# This is because `.collect` returns a copy of `my_nums`, but doesn't change (or mutate) the original `my_nums` array.
```

- **Yield** runs the block inside a method

```ruby
def yield_name(name)
  puts "In the method! Let's yield."
  yield("Kim")
  puts "In between the yields!"
  yield(name)
  puts "Block complete! Back in the method."
end

yield_name("Rick") { |n| puts "My name is #{n}." }

# In the method! Let's yield.
# My name is Kim.
# In between the yields!
# My name is Rick.
# Block complete! Back in the method.
```

- **Blocks** *are not* objects, and this is one of the very few exceptions to the "everything is an object" rule in Ruby. Because of this, blocks can't be saved to variables and don't have all the powers and abilities of a real object. For that, we'll need... **procs**!

- You can think of a **proc as a "saved" block**: just like you can give a bit of code a name and turn it into a method, you can name a block and turn it into a proc. With blocks, you have to write your code out each time you need it; with a proc, you write your code once and can use it many times!

```ruby
multiples_of_3 = Proc.new do |n|
  n % 3 == 0
end

print (1..100).to_a.select(&multiples_of_3)
```

```ruby
cube = Proc.new { |x| x ** 3 }

[1, 2, 3].collect!(&cube)
# ==> [1, 8, 27]
[4, 5, 6].map!(&cube)
# ==> [64, 125, 216]
```
> (The `.collect!` and `.map!` methods do the exact same thing.) The **&** is used to convert the **cube** proc into a block (since `.collect!` and `.map!` normally take a block).

```ruby
# Here at the amusement park, you have to be four feet tall
# or taller to ride the roller coaster. Let's use .select on
# each group to get only the ones four feet tall or taller.

group_1 = [4.1, 5.5, 3.2, 3.3, 6.1, 3.9, 4.7]
group_2 = [7.0, 3.8, 6.2, 6.1, 4.4, 4.9, 3.0]
group_3 = [5.5, 5.1, 3.9, 4.3, 4.9, 3.2, 3.2]

# Complete this as a new Proc
over_4_feet = Proc.new {|n| n >= 4.0}

# Change these three so that they use your new over_4_feet Proc
can_ride_1 = group_1.select(&over_4_feet)
can_ride_2 = group_2.select( &over_4_feet)
can_ride_3 = group_3.select( &over_4_feet)

puts can_ride_1
puts can_ride_2
puts can_ride_3

# ==>  [4.1, 5.5, 6.1, 4.7]
# ==>  [7.0, 6.2, 6.1, 4.4, 4.9]
# ==>  [5.5, 5.1, 4.3, 4.9]
```

```ruby
def greeter
  yield
end

phrase = Proc.new {puts "Hello there!"}

greeter(&phrase)

# ==> Hello there!
```

- Unlike blocks, we can **call** procs directly by using Ruby's `.call` method.

```ruby
hi = Proc.new {puts "Hello!"}
hi.call

# ==> Hello!
```

- **Symbols, meet Procs**: remember when we told you that you could pass a Ruby method name around with a symbol? Well, you can *also* convert symbols to procs using that handy little **&**:

```ruby
strings = ["1", "2", "3"]
nums = strings.map(&:to_i)
# ==> [1, 2, 3]
```

- Like procs, **lambdas** are objects. The similarities don't stop there: with the exception of a bit of syntax and a few behavioral quirks, lambdas are identical to procs:

```ruby
# Typing
lambda { puts "Hello!" }
# Is just about the same as
Proc.new { puts "Hello!" }
```

```ruby
def lambda_demo(a_lambda)
  puts "I'm the method!"
  a_lambda.call
end

lambda_demo(lambda { puts "I'm the lambda!" })

# ==> I'm the method!
# ==> I'm the lambda!
```
```ruby
strings = ["leonardo", "donatello", "raphael", "michaelangelo"]

symbolize = lambda {|string| string.to_sym}

symbols = strings.collect(&symbolize)
print symbols

# ==> [:leonardo, :donatello, :raphael, :michaelangelo]
```

- **Lambdas vs. Procs**
      1. A lambda checks the number of arguments passed to it, while a proc does not. This means that a lambda will throw an error if you pass it the wrong number of arguments, whereas a proc will ignore unexpected arguments and assign `nil` to any that are missing.
      2. When a lambda returns, it passes control back to the calling method; when a proc returns, it does so immediately, without going back to the calling method. A lambda is just like a proc, only it cares about the number of arguments it gets and it returns to its calling method rather than returning immediately.
To see how this works, take a look at the code in the editor. Our first method calls a proc; the second calls a lambda:

```ruby
def batman_ironman_proc
  victor = Proc.new { return "Batman will win!" }
  victor.call
  "Iron Man will win!"
end

puts batman_ironman_proc

def batman_ironman_lambda
  victor = lambda { return "Batman will win!" }
  victor.call
  "Iron Man will win!"
end

puts batman_ironman_lambda

# ==> Batman will win!
# ==> Iron Man will win!
```

> See how the proc says Batman will win? This is because it returns immediately, without going back to the `batman_ironman_proc` method.

> Our lambda, however, goes back into the method after being called, so the method returns the last code it evaluates: `"Iron Man will win!"`.

```ruby
my_array = ["raindrops", :kettles, "whiskers", :mittens, :packages]

# Add your code below!
symbol_filter = lambda {|param| param.is_a? Symbol}
symbols = my_array.select(&symbol_filter)

puts symbols

# ==> [:kettles, :mittens, :packages]
```

```ruby
odds_n_ends = [:weezard, 42, "Trady Blix", 3, true, 19, 12.345]

checking = lambda {|i| i.is_a? Integer}
ints = odds_n_ends.select(&checking)

puts ints

# ==> [42, 3, 19]
```

```ruby
crew = {
  captain: "Picard",
  first_officer: "Riker",
  lt_cdr: "Data",
  lt: "Worf",
  ensign: "Ro",
  counselor: "Troi",
  chief_engineer: "LaForge",
  doctor: "Crusher"
}
first_half = lambda {|k, v| v < "M"}
a_to_m = crew.select(&first_half)

puts a_to_m
# ==> {:lt_cdr=>"Data", :chief_engineer=>"LaForge", :doctor=>"Crusher"}
```

## Object-Oriented Programming, Part 1

```ruby
"Matz".length
# ==> 4
```
In the "Matz" object is a string with a .length method and a length attribute of 4.

- By **convention**, class names start with a capital letter and use CamelCase instead of relying_on_underscores.

- **@**: In Ruby, we use `@` before a variable to signify that it's an *instance variable*. This means that the variable is attached to the instance of the class.

```ruby
class Car
  def initialize(make, model)
    @make = make
    @model = model
  end
end

kitt = Car.new("Pontiac", "Trans Am")
```
The code in the example above creates an instance, `kitt`, of the class `Car`. `kitt` has his own `@make` ("Pontiac") and `@model` ("Trans Am"). Those variables belong to the `kitt` instance, which is why they're called instance variables.

```ruby
class Person
  def initialize(name)
    @name = name
  end
end
```
This tells Ruby that whenever it creates a `Person`, it has to have a name, and each instance of `Person` will have its own `@name`.

- **Scope:** Another important aspect of Ruby classes is *scope*. The scope of a variable is the context in which it's visible to the program.
  - It may surprise you to learn that not all variables are accessible to all parts of a Ruby program at all times. When dealing with classes, you can have variables that are available everywhere (*global variables*, starts with `$`), ones that are only available inside certain methods (*local variables*), others that are members of a certain class (*class variables*, starts with `@@`), and variables that are only available to particular instances of a class (*instance variables*, starts with `@`).
  - The same goes for methods: some are available everywhere, some are only available to members of a certain class, and some are only available to particular instance objects.

- **Class variables** are like **instance variables**, but instead of belonging to an instance of a class, they belong to the class itself. Class variables always start with two `@`s, like so: `@@files`.

- **Global variables** can be declared in two ways. The first is one that's already familiar to you: you just define the variable outside of any method or class, and voilà! It's global. If you want to make a variable global from inside a method or class, just start it with a `$`, like so: `$matz`.

```ruby
class MyClass
  my_variable = "Hello!" # $my_variable = "Hello!"
end

puts my_variable # puts $my_variable
```

The variable `my_variable` is inside a class, so it's not reachable by the `puts` method outside it. But you can fix this by adding `$`as prefix.

- **Global variables** can be changed from anywhere in your program, and they are generally not a very good idea. It's much better to create variables with limited scope that can only be changed from a few places! For example, **instance variables** belong to a particular object (or "instance").

- **Class variables** are attached to entire classes, not just instances of classes, like so:

```ruby
class MyClass
  @@class_variable
end
```

Because there's only one copy of a class variable shared by all instances of a class, we can use them to pull off some cool Ruby tricks. For example, we can use a class variable to keep track of the number of instances of that class we've created:

```ruby
class Person

  def initialize(name)
    @name = name
  end

  def self.number_of_instances
    return @@people_count
  end
end

matz = Person.new("Yukihiro")
dhh = Person.new("David")

puts "Number of Person instances: #{Person.number_of_instances}"
```

- **Inheritance Syntax**, You can read "<" as "inherits from."

```ruby
class DerivedClass < BaseClass

end
```

Here, DerivedClass is subclass and BaseClass is called as a parent or superclass.

- **Override:**

```ruby
class Creature
  def initialize(name)
    @name = name
  end

  def fight
    return "Punch to the chops!"
  end
end

class Dragon < Creature
  def fight
    return "Breathes fire!"
  end
end
```

- **super** keyword: You can directly access the attributes or methods of a superclass with Ruby's built-in super keyword if you've overwritten in your sub class.

The syntax looks like this:
```ruby
class Creature
  def initialize(name)
    @name = name
  end

  def fight
    return "Punch to the chops!"
  end
end

class Dragon < Creature
  def fight
    puts "Instead of breathing fire..."
    return super
  end
end
```
When you call `super` from inside a method, that tells Ruby to look in the superclass of the current class and find a method with the same name as the one from which `super` is called. If it finds it, Ruby will use the superclass' version of the method.

- Any given Ruby class can have only one superclass. Some languages allow a class to have more than one parent, which is a model called **multiple inheritance**. However, there are instances where you want to incorporate data or behavior from several classes into a single class, and Ruby allows this through the use of *mixins*. We'll learn about mixins in a later lesson.

- **Usage of semicolon:** If you want to end a Ruby statement without going to a new line, you can just type a semicolon:

```ruby
class Dragon < Creature; end
```

- If we need to reach a class variable, we use a **class method** to grab it. A class method belongs to the class itself, and for that reason, it's prefixed with the class name:

```ruby
class Machine
  def Machine.hello
    puts "Hello from the machine!"
  end
end
```

```ruby
class Computer
  @@users = {}

  def initialize(username, password)
    @username = username
    @password = password
    @files = {}
    @@users[username] = password
  end

  def create(filename)
    time = Time.now
    @files[filename] = time
    puts "#{filename} is created! at #{time} by #{@username}"
  end

  def Computer.get_users
    @@users
  end
end

my_computer = Computer.new("idil", 1315)
my_computer.create("Todo.txt")

puts "Users: #{Computer.get_users}"
```

## Object-Oriented Programming, Part 2

- **Public** vs **Private** Methods:
  - Public methods allow for an **interface** with the rest of the program; they say, "Hey! Ask me if you need to know something about my class or its instances."
  - Private methods, on the other hand, are for your classes to do their own work undisturbed. They don't want anyone asking them anything, so they make themselves unreachable!

- Methods are public by default in Ruby, so if you don't specify `public` or `private`, your methods will be public. In this case, however, we want to make it clear to people reading our code which methods are public. We do this by putting `public` before our method definitions, like so:

```ruby
class ClassName
  # Some class stuff
  public
  def public_method
    # public_method stuff
  end
end
```
Note that everything after the `public` keyword through the `end` of the class definition will now be public unless we say otherwise.

- `private` methods are just that: they're private to the object where they are defined. This means you can only call these methods from other code inside the object. Another way to say this is that the method cannot be called with an *explicit receiver*. You've been using receivers all along—these are the objects on which methods are called! Whenever you call `object.method`, `object` is the receiver of the `method`.

- In order to access private information, we have to create public methods that know how to get it. This separates the private *implementation* from the public *interface*.

- **attr_reader, attr_writer**
Ruby needs methods in order to access attributes. For instance, if we want to access a @name instance variable, we had to write something like

```ruby
def name
  @name
end
```
Well, no longer! We can use **attr_reader** to access a variable and **attr_writer** to change it. If we write

```ruby
class Person
  attr_reader :name
  attr_writer :name
  def initialize(name)
    @name = name
  end
end
```
Ruby does something like this for us automatically:

```ruby
def name
  @name
end

def name=(value)
  @name = value
end
```
Like magic, we can read and write variables as we please! We just pass our instance variables (as symbols) to `attr_reader` or `attr_writer`.
> (That `name=` might look funny, but you're allowed to put an `=` sign in a method name. That's just a Ruby convention saying, "hey, this method sets a value!")

- **attr_accessor:** If we want to both read and write a particular variable, there's an even shorter shortcut than using `attr_reader` and `attr_writer`. We can use `attr_accessor` to make a variable readable and writeable in one fell swoop.

- **Module**
You can think of a module as a toolbox that contains a set methods and constants. There are lots and lots of Ruby tools you might want to use, but it would clutter the interpreter to keep them around all the time. For that reason, we keep a bunch of them in modules and only pull in those module toolboxes when we need the constants and methods inside! You can think of modules as being very much like classes, only modules can't create instances and can't have subclasses. They're just used to store things!

```ruby
module ModuleName
  FAVE_FILM = "The Brand New Testament"
end
```
- Like class names, module names are written in CapitalizedCamelCase, rather than lowercase_with_underscores.

- It doesn't make sense to include variables in modules, since variables (by definition) change (or vary). Constants, however, are supposed to always stay the same, so including helpful constants in modules is a great idea.

- Ruby doesn't *make* you keep the same value for a constant once it's initialized, but it will warn you if you try to change it. Ruby constants are written in ALL_CAPS and are separated with underscores if there's more than one word.

- An example of a Ruby constant is `PI`, which lives in the `Math` module and is approximately equal to 3.141592653589793.

- One of the main purposes of modules is to separate methods and constants into named spaces. This is called (conveniently enough) **namespacing**, and it's how Ruby doesn't confuse `Math::PI` and `Circle::PI`.

- See that double colon we just used? That's called the **scope resolution operator**, which is a fancy way of saying it tells Ruby *where* you're looking for a specific bit of code. If we say `Math::PI`, Ruby knows to look inside the `Math` module to get that `PI`, not any other `PI` (such as the one we created in `Circle`).

- **require:** Some modules, like `Math`, are already present in the interpreter. Others need to be explicitly brought in, however, and we can do this using `require`. We can do this simply by typing as follows:

```ruby
require 'date'

puts Date.today
```

- **include:** Any class that `include`s a certain module can use those module's methods!

- A nice effect of this is that you no longer have to prepend your constants and methods with the module name. Since everything has been pulled in, you can simply write PI instead of Math::PI.

- In this case, we want to use `Math::cos` but we don't want to type `Math::`. Then, we use `include Math`.

```ruby
class Angle
  include Math
  attr_accessor :radians

  def initialize(radians)
    @radians = radians
  end

  def cosine
    cos(@radians)
  end
end

acute = Angle.new(1)
acute.cosine
```
> What we did above might not have seemed strange to you, but think about it: we mixed together the behaviors of a class and a module!

- When a module is used to mix additional behavior and information into a class, it's called a **mixin**. Mixins allow us to customize a class without having to rewrite code!

- Check out the code. See how we define the `jump` method in the `Action` module, then mix it into the `Rabbit` and `Cricket` classes:

```ruby
module Action
  def jump
    @distance = rand(4) + 2
    puts "I jumped forward #{@distance} feet!"
  end
end

class Rabbit
  include Action
  attr_reader :name
  def initialize(name)
    @name = name
  end
end

class Cricket
  include Action
  attr_reader :name
  def initialize(name)
    @name = name
  end
end

peter = Rabbit.new("Peter")
jiminy = Cricket.new("Jiminy")

peter.jump
jiminy.jump
```

```ruby
module MartialArts
  def swordsman
    puts "I'm a swordsman."
  end

end
class Ninja
  include MartialArts
  def initialize(clan)
    @clan = clan
  end
end

class Samurai
  include MartialArts
  def initialize(shogun)
    @shogun = shogun
  end
end
```

- Whereas `include` mixes a module's methods in at the instance level (allowing instances of a particular class to use the methods), the `extend` keyword mixes a module's methods at the *class* level. This means that *class itself* can use the methods, as opposed to *instances* of the class.

```ruby
module ThePresent
  def now
    puts "It's #{Time.new.hour > 12 ? Time.new.hour - 12 : Time.new.hour}:#{Time.new.min} #{Time.new.hour > 12 ? 'PM' : 'AM'} (GMT)."
  end
end

class TheHereAnd
  extend ThePresent
end

TheHereAnd.now
# ==> It's 12:38 AM (GMT).
```

```ruby
module Languages
  FAVE = "Ruby"
end

class Master
  include Languages
  def initialize; end
  def victory
    puts FAVE
  end
end

total = Master.new
total.victory
# ==> Ruby
```

```ruby
class Account
  attr_reader :name, :balance
  def initialize(name, balance=100)
    @name = name
    @balance = balance
  end
end
```

- What's that `balance=100` doing? It's signifying an **optional parameter**. Ruby is saying that you can pass one or *two* arguments to `initialize`; if you pass two, it uses your `balance` argument to set `@balance`; if you only pass a `name`, `balance` gets a default value of `100`, and that's what gets stored in `@balance`.

# Beginning Ruby: From Novice to Professional by Peter Cooper

## CHAPTER 3: Ruby’s Building Blocks: Data, Expressions, and Flow Control

### Numbers and Expressions

- `between?` **method*:* age.between?(13, 19) is equivalent to age >= 13 && age <= 19

- `step` **method**

```ruby
0.step(10, 5){|number| puts number}
0
5
10
 => 0
```

- Constants are unchanging values and can also be represented in Ruby by a variable name beginning with a capital letter (e.g.
Pi = 3.141592)
- If you try to change the value of Pi, it will let you do it, but
you’ll get a warning: `(irb): warning: already initialized constant Pi`
> Class names also begin with capital letters such as `class Dog`. This is because once a class is defined, it’s a constant part of the program and therefore acts as a constant, too.

### Text and Strings

- When a string is embedded directly into code, using quotation marks such as `puts "Hello World!".class`, the construction is called a **string literal**.

#### Substitutions

> `sub` vs `gsub`: The difference is that `sub` only replaces the first occurrence of the pattern specified, whereas `gsub` does it for all occurrences (that is, it replaces globally).

```ruby
"hello".sub('l', '*')
# => "he*lo"
"hello".gsub('l', '*')
# => "he**o"
```

```ruby
puts "foobar".sub('bar', 'foo')
# ==> foofoo

puts "this is a test".gsub('i', '')
# ==> ths s a test

x = "This is a test"
puts x.sub(/^../, 'Hello')
# ==> Hellois is a test
```
In the last case, you make a single substitution with `sub`. The first parameter given to sub isn’t a string but
a regular expression—forward slashes are used to start and end a regular expression. Within the regular expression is ^... The ^ is an *anchor*, meaning the regular expression will match from the beginning of
any lines within the string. The two periods each represent “any character.” In all, /^../ means “any two characters immediately after the start of a line.” Therefore, `Th` of `"This is a test"` gets replaced with `Hello`.
Likewise, if you want to change the last two letters, you can use a different anchor:

```ruby
x = "This is a test"
puts x.sub(/..$/, 'Hello')

# ==> This is a teHello
```
This time the regular expression matches the two characters that are anchored to the end of any lines within the string.

#### Iteration with a Regular Expression

What if you want to iterate through a string and have access to each section of it separately? `scan` is the iterator method you require:

```ruby
"xyz".scan(/./) { |letter| puts letter }
# x
# y
# z
```
In this case, you’ve supplied a regular expression that looks for a single character at a time. That’s why you get x, y, and z separately in the output. Each letter is fed to the block, assigned to `letter`, and printed to the screen. Try this more elaborate example:

```ruby
"This is a test".scan(/../) { |x| puts x }
# Th
# is
# i
# s
# a
# te
# st
```
This time you’re scanning for two characters at a time. Easy! Scanning for all characters results in some weird output, though, with all the spaces mixed in. Let’s adjust our regular expression to match only letters and digits, like so:

```ruby
"This is a test".scan(/\w\w/) { |x| puts x }
# Th
# is
# is
# te
# st
```
**Basic Special Characters and Symbols Within Regular Expressions**

| Character     | Meaning
| ------------- |:-------------:
| ^             |Anchor for the beginning of a line
| $             |Anchor for the end of a line
| \A            |Anchor for the start of a string
| \z            |Anchor for the end of a string
| .             |Any character
| \w            |Any letter, digit, or underscore
| \W            |Anything that \w doesn’t match
| \d            |Any digit
| \D            |Anything that \d doesn’t match (non-digits)
| \s            |Whitespace (spaces, tabs, newlines, and so on)
| \S            |Non-whitespace (any visible character)

```ruby
"The car costs $1000 and the cat costs $10".scan(/\d+/) do |x|
  puts x
end
# 1000
# 10

"The car costs $1000 and the cat costs $10".scan(/\d/) do |x|
 puts x
end
# 1
# 0
# 0
# 0
# 1
# 0
```
In the first one, the `+` that follows `\d` makes `\d` match as many digits in a row as possible. This means it matches both `1000` and `10`, rather than just each individual digit at a time. So, + after a character in a regular expression means match one or more of that type of character. There are other types of modifiers, and please search for *Regular Expression Character and Sub-Expression Modifiers*

- The last important aspect of regular expressions you need to understand at this stage is *character classes*. These allow you to match against a specific set of characters. For example, you can scan through all the vowels in a string:

```ruby
"This is a test".scan(/[aeiou]/) { |x| puts x }
# i
# i
# a
# e
```
[aeiou] means “match any of a, e, i, o, or u.” You can also specify ranges of characters inside the square brackets, like so:

```ruby
"This is a test".scan(/[a-m]/) { |x| puts x }
# h
# i
# i
# a
# e
```
This scan matches all lowercase letters between a and m.

#### Matching

- **To check quickly** e.g. if a string contains any vowels:

```ruby

puts "String has vowels" if "This is a test" =~ /[aeiou]/

puts "String contains no digits" unless "This is a test" =~ /[0-9]/
```
> =~ is another form of operator: a *matching* operator. If the string has a match with the regular expression following the operator, then the expression returns the position of the first match (`2` in the first case—which logically is non-false, so the if condition is satisfied; and `nil` for the second case)

--------

For more matching examples and problems please check this great little [Regex Tutorial](https://regexone.com/)

### Arrays and Lists
#### Splitting Strings into Arrays

```ruby
puts "This is a test".scan(/\w/).join(',')
# T,h,i,s,i,s,a,t,e,s,t
```

```ruby
puts "Short sentence. Another. No more.".split(/\./).inspect
# ["Short sentence", " Another", " No more"]
```
There are a couple of important points here. First, if you’d used `.` in the regular expression rather than
`\.`, you’d be splitting on every character rather than on full stops, because . represents “any character” in a regular expression. Therefore, you have *to escape* it by prefixing it with a backslash (*escaping* is the process of specifically denoting a character to make its meaning clear). Second, rather than joining and printing out the sentences, you’re using the inspect method to get a tidier result.

- The `inspect` method is common to almost all built-in classes in Ruby and it gives you a textual representation of the object. For example, the preceding output shows the result array in the same way that you might create an array yourself. `inspect` is incredibly useful when experimenting and debugging!

```ruby
puts "Words with lots of spaces".split(/\s+/).inspect
# ["Words", "with", "lots", "of", "spaces"]
```
It is also important to cover p, an alternative to using inspect. The previous example could also be written in this way:

```ruby
p "Words with lots of spaces".split(/\s+/)
# ["Words", "with", "lots", "of", "spaces"]
```

> p is an extremely useful alternative to using puts when playing with expressions in irb. It automatically shows you the structure of the object(s) returned by the expression following it. We will use p extensively throughout the rest of this chapter. You will almost never need to use it in a production application, but for debugging and learning, it’s excellent—not to mention quick to type!

#### Accessing the first elements of the Array

```ruby
x = [1, 2, 3]
puts x.first(2).join("-")
# 1-2
```

#### Reversing the Order of the Array’s Elements

```ruby
x = [1, 2, 3]
p x.reverse
# [3, 2, 1]
```
### Hashes
#### Hashes within Hashes

```ruby
people = {
 'fred' => {
 'name' => 'Fred Elliott',
 'age' => 63,
 'gender' => 'male',
 'favorite painters' => ['Monet', 'Constable', 'Da Vinci']
 },
 'janet' => {
 'name' => 'Janet S Porter',
 'age' => 55,
 'gender' => 'female'
 }
}
puts people['fred']['age']
puts people['janet']['gender']
p people['janet']

# 63
# female
# {"name"=>"Janet S Porter", "age"=>55, "gender"=>"female"}

puts people['fred']['favorite painters'].length
puts people['fred']['favorite painters'].join(", ")

# 3
# Monet, Constable, Da Vinci
```
### Flow Control
#### ?, the Tenary Operator

```ruby
age = 10
type = age < 18 ? "child" : "adult"
puts "You are a " + type
```
The second line contains the ternary operator. It starts by assigning the result of an expression to the variable,type.The expression is `age < 18 ? "child" : "adult"`. Thestructureisasfollows:

`<condition> ? <result if condition is true> : <result if condition is false>`

In our example, age < 18 returns true, so the first result, "child", is returned and assigned to type. However, if age < 18 were to be false, "adult" would be returned.

```ruby
age = 10
puts "You are a " + (age < 18 ? "child" : "adult")
```
### Other Useful Building Blocks
#### Ranges

```ruby
a = [2, 4, 6, 8, 10, 12]
p a[1..3]

# [4, 6, 8]
```

#### Symbols

```ruby
current_situation = :good
puts "Everything is fine" if current_situation == :good
puts "PANIC!" if current_situation == :bad

# Everything is fine
```
In this example, `:good` and `:bad` are symbols. Symbols don’t contain values or objects, like variables do. Instead, they’re used as a consistent name within code. For example, in the preceding code, you could easily replace the symbols with strings, like so:

```ruby
current_situation = "good"
puts "Everything is fine" if current_situation == "good"
puts "PANIC!" if current_situation == "bad"
```
This gives the same result, but isn’t as efficient. In this example, every mention of “good” and “bad” creates a new object stored separately in memory, whereas symbols are single reference values that are only initialized once. In the first code example, only `:good` and `:bad exist`, whereas in the second example, you end up with the full strings of "good", "good", and "bad" taking up memory.

Symbols also result in cleaner code in many situations. Often you’ll use symbols to give method parameters a name. Having varying data as strings and fixed information as symbols results in easier-to-read code.

You might want to consider symbols to be literal constants that have no value, but whose name is the most important factor. If you assign the :good symbol to a variable, and compare that variable with :good in the future, you’ll get a match. This makes symbols useful in situations where you don’t necessarily want to store an actual value, but a concept or an option.

#  Ruby Date and Time explanation from [TutorialsPoint](https://www.tutorialspoint.com/ruby/ruby_date_time.htm).

> I only note some highlights, please check [TutorialsPoint](https://www.tutorialspoint.com/ruby/ruby_date_time.htm) for more details.

#### Getting Current Date and Time

```ruby
time1 = Time.new
puts time1
# 2017-09-05 12:06:47 +0100
# => nil

puts "Current time " + time1.inspect
# Current time 2017-09-05 12:06:47 +0100
# => nil
```

#### Getting components of a date & time

```ruby
time = Time.new
puts time.year # 2017
puts time.wday # 2 (Day of week: 0 is Sunday)
puts time.yday # 248
puts time.min # 23
puts time.zone # "UTC": timezone name
```

#### Time.utc, Time.gm and Time.local Functions

```ruby
# July 8, 2008, 09:10am, local time
Time.local(2008, 7, 8, 9, 10)
# July 8, 2008, 09:10 UTC
Time.utc(2008, 7, 8, 9, 10)
# July 8, 2008, 09:10:11 GMT (same as UTC)
Time.gm(2008, 7, 8, 9, 10, 11)
```

```ruby
time = Time.new

values = time.to_a
puts Time.utc(*values)
# Mon Jun 02 12:15:36 UTC 2008
```

- Scroll down on [this link](https://www.tutorialspoint.com/ruby/ruby_date_time.htm) for **Timezones, Daylight Savings Time** and **Time Formatting**

#### Time Arithmetic

```ruby
now = Time.now
puts now
# 2017-09-05 12:35:32 +0100 (Current time)

past = now - 10
puts past
# 2017-09-05 12:35:22 +0100 (10 seconds ago. Time - number => Time)

future = now + 10
puts future
# 2017-09-05 12:35:42 +0100 (10 seconds from now Time + number => Time)

diff = future - now
puts diff
# 10.0 (=> 10  Time - Time => number of seconds)
```

## CHAPTER 6: Classes, Objects, and Modules

### Object-Orientation Basics

- A *class* is a blueprint for objects.
- You have only one class called `Shape`, but with it you can create multiple *instances* of shapes (`Shape`*objects*), all of which have the methods and attributes defined by the `Shape` class.
- An *object* is an *instance* of a class.

### Local Variables

```ruby
def basic_method
  puts x
end
x = 10
basic_method

# => NameError: undefined local variable or method 'x' for main:Object
```
When you jump to `basic_method`, you’re no longer in the same *scope* as the variable x that you created. Because x is a local variable, it exists only where it was defined.

### Global Variables

- As their name suggests, global variables are available from everywhere within an application, including inside classes or objects
- Global variables can be useful, but aren’t commonly used in Ruby. They don’t mesh well with the ideals of object-oriented programming, as once you start using global variables across an application, your code is likely to become dependent on them. Because the ability to separate blocks of logic from one another is a useful aspect of object-oriented programming, global variables are not favored.

```ruby
def basic_method
  puts $x
end
$x = 10
basic_method

# => 10
```
> The `$` and `@` characters that denote global variables and object variables (as demonstrated in the next section) are technically called *sigils*.

### Class Variables

> In recent years, class variables have begun to fall out of favor among professional Ruby developers. Fashions come and go in the Ruby world but ultimately enable developers to work together more smoothly. Since all classes are themselves objects within Ruby, it has become more popular to simply use object variables within the context of class methods in order to keep things simple.

#### Class Methods versus Instance Methods

```ruby
class Square
def self.test_method
puts "Hello from the Square class!"
end
def test_method
puts "Hello from an instance of class Square!"
end
Square.test_method
Square.new.test_method

# => Hello from the Square class!
# => Hello from an instance of class Square!
```
This class has two methods. The first is a class method, and the second is an instance method, although both have the same name of `test_method`. The difference is that the class method is denoted with `self.`, where `self` represents the current class, so `def self.test_method` defines the method as being specific to the class. However, with no prefix, methods are automatically instance methods.
Alternatively, you could define the method like so:

> The main disadvantage of using the class name rather than self is that using self makes it easier to rename the class later on without having to update the names of all your class methods.

> Consider it as if you’re asking the class to do something that’s relevant to the class as a whole, rather than asking the objects.

```ruby
class Square
  def initialize
    if defined?(@@number_of_squares)
      @@number_of_squares += 1
    else
      @@number_of_squares = 1
    end
  end
  def self.count
    @@number_of_squares
  end
end

a = Square.new
puts Square.count
b = Square.new
puts Square.count
c = Square.new
puts Square.count

# => 1
# => 2
# => 3
```
Notice you don’t refer to a, b, or c at all to get the count. You just use the Square.count class method directly. Consider it as if you’re asking the class to do something that’s relevant to the class as a whole, rather than asking the objects.

#### Inheritance

```ruby
class Person
  def initialize(name)
    @name = name
  end
  def name
    return @name
  end
end
class Doctor < Person
  def name
    "Dr. " + super
  end
end
```
The benefit of using inheritance in this way is that you can implement generic functionality in generic classes, and then implement only the specific functionality that more specific child classes require.

#### Reflection and Discovering an Object’s Methods

*Reflection* is the process by which a computer program can inspect, analyze, and modify itself while it’s running and being used. Ruby takes reflection to an extreme and allows you to change the functionality of great swathes of the language itself while running your own code.

It’s possible to query almost any object within Ruby for the methods that are defined within it. This is another part of reflection.

```ruby
a = "This is a test"
puts a.methods.join(' ')

# <=> == === eql? hash casecmp + * % [] []= insert length size bytesize empty? =~ match
succ succ! next next! upto index rindex replace clear chr getbyte setbyte byteslice scrub
scrub! freeze to_i to_f to_s to_str inspect dump upcase downcase capitalize swapcase
upcase! downcase! capitalize! swapcase! hex oct split lines bytes chars codepoints
reverse reverse! concat << prepend crypt intern to_sym ord include? start_with? end_with?
scan ljust rjust center sub gsub chop chomp strip lstrip rstrip sub! gsub! chop! chomp!
strip! lstrip! rstrip! tr tr_s delete squeeze count tr! tr_s! delete! squeeze! each_line
each_byte each_char each_codepoint sum slice slice! partition rpartition encoding force_
encoding b valid_encoding? ascii_only? unpack encode encode! to_r to_c unicode_normalize
unicode_normalize! unicode_normalized? to_json to_json_raw to_json_raw_object >>= <<=
between? nil? !~ class singleton_class clone dup itself taint tainted? untaint untrust
untrusted? trust frozen? methods singleton_methods protected_methods private_methods
public_methods instance_variables instance_variable_get instance_variable_set instance_
variable_defined? remove_instance_variable instance_of? kind_of? is_a? tap send public_
send respond_to? extend display method public_method singleton_method define_singleton_
method object_id to_enum enum_for equal? ! != instance_eval instance_exec __send__ __id__
```
The methods method on any object (unless it has been overridden, of course!) returns an array of methods made available by that object

```ruby
class Person
  attr_accessor :name, :age
end

p = Person.new
p.name = "Fred"
p.age = 20
puts p.instance_variables

# @age
# @name
```
Another example for reflection from [this website](http://blog.khd.me/blog/2008/12/19/ruby-reflection/)

```ruby
class Demo
  def initialize(n)
    @secret = n
  end
  def getBinding
    return binding()# a method defined in Kernel module
  end
end
k1 = Demo.new(99)
#get the value of the instance variable @secret stored in the binding of object k1
eval("@secret", k1.getBinding)   #=> 99
```

#### Encapsulation

Encapsulation describes the way in which data and methods can be bundled together into objects that operate as a single unit. Within Ruby, however, the term is often used to describe the ability for an object to have certain methods and attributes available for use publicly (from any section of code), but for others to be visible only *within* the class itself or by other objects of the same class.

```ruby
class Person
  def initialize(name)
    set_name(name)
  end
  def name
    @first_name + ' ' + @last_name
  end
  def set_name(name)
    first_name, last_name = name.split(/\s+/)
    set_first_name(first_name)
    set_last_name(last_name)
  end
  def set_first_name(name)
    @first_name = name
  end
  def set_last_name(name)
    @last_name = name
  end
end
```
> Inprevious examples,you would have written this with a single `attr_accessor :name`and simply assigned the name to an object variable. One possible reason for such a construction could be that although you want to work with complete names in your application, the database design might demand you have first names and last names in separate columns. Therefore, you need to hide this difference by handling it in the class code, as in the preceding code.

- However, you may have some problems:

```ruby
p = Person.new("Fred Bloggs")
p.set_last_name("Smith")
puts p.name

# Fred Smith
```
Uh-oh! You wanted to abstract the first name/last name requirement and only allow full names to be set or retrieved. However, the `set_first_name` and `set_last_name` are still public and you can use them directly from any code where you have `Person` objects. Luckily, encapsulation lets you solve the problem:

```ruby
class Person
  def initialize(name)
    set_name(name)
  end
  def name
    @first_name + ' ' + @last_name
  end
private
  def set_name(name)
    first_name, last_name = name.split(/\s+/)
    set_first_name(first_name)
    set_last_name(last_name)
  end
  def set_first_name(name)
    @first_name = name
  end
  def set_last_name(name)
    @last_name = name
  end
end
```
`private` tells Ruby that any methods declared in this class from there on should be kept private. This means that only code within the object’s methods can access those private methods, whereas code outside of the class cannot. For example, this code no longer works:

```ruby
p = Person.new("Fred Bloggs")
p.set_last_name("Smith")
```
You can also use `private` as a command by passing in symbols representing the methods you want to keep private, like so:

```ruby
class Person
  def anyone_can_access_this; ...; end
  def this_is_private; ...; end
  def this_is_also_private; ...; end
  def another_public_method; ...; end
private :this_is_private, :this_is_also_private
end
```
> Ruby supports ending lines of code with semicolons (;) and allows you to put multiple lines of code onto a single line (for example, x = 10; x += 1; putsx). In this case, it’s been done to save on lines of code in the example, although it’s not considered good style in production-quality Ruby code.
- Ruby supports a third form of encapsulation (other than `public` and `private`) called `protected` that makes a method private, but within the scope of a class rather than within a single object. For example, you were unable to directly call a private method outside the scope of that object and its methods. However, you can call a protected method from the scope of the methods of any object that’s a member of the same class:

```ruby
class Person
  def initialize(age)
    @age = age end
  def age
    @age
  end
  def age_difference_with(other_person)
      (self.age - other_person.age).abs
  end
protected :age
end

fred = Person.new(34)
chris = Person.new(25)
puts chris.age_difference_with(fred)
puts chris.age

# => 9
# => protected method 'age' called for #<Person:0x1e5f28 @age=25> (NoMethodError)
```
**protected vs private:** The preceding example uses a protected method so that the age method cannot be used directly, except within any method belonging to an object of the `Person` class. However, if age were made `private`, the preceding example would fail because `other_person.age` would be invalid. That’s because `private` makes methods accessible only by methods of a specific object.

> Some Ruby developers do not believe marking methods as `private` or `protected` provides any significant value and that, indeed, it prevents developers from having free and open access to their code. We’re not going to push a particular opinion here, but you may wish to avoid using these features until you have a strong opinion either way.

#### Polymorphism

Polymorphism is the concept of writing code that can work with objects of multiple types and classes at once. For example, the `+` method works for adding numbers, joining strings, and adding arrays together. What `+` does depends entirely on *what* type of things you’re adding together. (e.g. `.to_s`)

#### Nested Classes

Nested classes are useful when a class depends on other classes, but those classes aren’t necessarily useful anywhere else. They can also be useful when you want to separate classes into groups of classes rather than keep them all distinct. Here’s an example:

```ruby
class Drawing
  class Line
  end

  class Circle
  end
end
```
Nested classes are defined in the same way as usual. However, they’re used differently. From within `Drawing`, you can access the `Line` and `Circle` classes directly, but from outside the `Drawing` class, you can only access `Line` and `Circle` as `Drawing::Line` and `Drawing::Circle`. For example:

```ruby
class Drawing
  def self.give_me_a_circle
    Circle.new
  end

  class Line
  end

  class Circle
    def what_am_i
      "This is a circle"
    end
  end
end

a = Drawing.give_me_a_circle
puts a.what_am_i
a = Drawing::Circle.new
puts a.what_am_i
a = Circle.new
puts a.what_am_i

# => This is a circle
# => This is a circle
# => NameError: uninitialized constant Circle
```

#### The Scope of Constants

A constant appears to work like a global variable, but it’s not. Constants are defined within the scope of the current class and are made available to all child classes, unless they’re overridden. For example:

```ruby
Pi = 3.141592

class OtherPlanet
  Pi = 4.5
  def self.circumference_of_circle(radius)
    radius * 2 * Pi
  end
end

puts OtherPlanet.circumference_of_circle(10)
puts OtherPlanet::Pi
puts Pi

# => 90.0
# => 4.5
# => 3.141592
```
> Pay attention to capitalized variable name. It works with ALL_CAPS as well.

### Modules, Namspaces, and Mix-Ins

Modules provide a structure to collect Ruby classes, methods, and constants into a single, separately named and defined unit. This is useful so you can avoid clashes with existing classes, methods, and constants, and also so that you can add (mix in) the functionality of modules into your classes. First, we’ll look at how to use modules to create *namespaces* to avoid name-related clashes.

#### Namespaces

- As the last file loaded, it turns out to be the latter version of the method should appear onscreen. Unfortunately, however, it means your other random method has been “lost.” This situation is known as a *name conflict*.
- For example, class names can clash similarly, and you could end up with two classes mixed into one by accident. If a class called `Song` is defined in one external file and then defined in a second external file, the class `Song` available in your program will be a dirty mix of the two.

- Modules help to solve these conflicts by providing *namespaces* that can contain any number of classes, methods, and constants, and allow you to address them directly. For example:

```ruby
module NumberStuff
  def self.random
    rand(1000000)
  end
end
module LetterStuff
  def self.random
    (rand(26) + 65).chr
  end
end

puts NumberStuff.random
puts LetterStuff.random

# 184783
# X
```
> The `modules` defined in the preceding code look a little like classes, except they’re defined with the word `module` instead of `class`. However, in reality you cannot define instances of a module, as they’re not actually classes, nor can they inherit from anything. Modules simply provide ways to organize methods, classes, and constants into separate namespaces.

- A more complex example could involve demonstrating two classes with the same name, but in different modules:

```ruby
module ToolBox
  class Ruler
    attr_accessor :length
  end
end

module Country
  class Ruler
    attr_accessor :name
  end
end

a = ToolBox::Ruler.new
a.length = 50
b = Country::Ruler.new
b.name = "Genghis Khan from Moskau"
```
Rather than having the `Ruler` classes fighting it out for supremacy, or ending up with a mutant `Ruler` class with both `name` and `length` attributes (how many measuring rulers have names?), the `Ruler` classes are kept separately in the `ToolBox` and `Country` namespaces.

- The second reason why modules are so useful: Mix-Ins

#### Mix-Ins

Ruby’s inheritance functionality only lets you create simple trees of classes, avoiding the confusion inherent with multiple inheritance systems.
- However, in some cases it can be useful to share functionality between disparate classes. In this sense, modules act like a sort of bundle of methods, classes, and constants that can be *included* into other classes, extending that class with the methods the module offers. For example:

```ruby
module UsefulFeatures
  def class_name
    self.class.to_s
  end
end

class Person
  include UsefulFeatures
end

x = Person.new
puts x.class_name

# Person
```
In this code, `UsefulFeatures` looks almost like a class and, well, it almost is. However, modules are organizational tools rather than classes themselves. The `class_name` method exists within the module and is then *included* in the Person class. Here’s another example:

```ruby
module AnotherModule
  def do_stuff
    puts "This is a test"
  end
end

include AnotherModule
do_stuff

# This is a test
```
As you can see, you can include module methods in the current scope, even if you’re not directly within a class. Somewhat like a class, though, you can use the methods directly:

```ruby
AnotherModule.do_stuff
```
Therefore, `include` takes a module and includes its contents into the current scope.
- Ruby comes with several modules by standard that you can use. For example, the `Kernel` module contains all the “standard” commands you use in Ruby (such as `load`, `require`, `exit`, `puts`, and `eval`) without getting involved with objects or classes. None of those methods are taking place directly in the scope of an object (as with the methods in your own programs), but they’re special methods that get included in all classes (including the `main` scope), by default, through the `Kernel` module.
- However, of more interest to us are the modules Ruby provides that you can include in your own classes to gain more functionality immediately. Two such modules are `Enumerable` and `Comparable`.

### Enumerable

The `Array` class (for one) has pre-included the methods provided by the `Enumerable` module, a module that supplies about 20 useful countingand iteration-related methods, including `collect`, `detect`, `find`, `find_all`, `include?`, `max`, `min`, `select`, `sort`, and `to_a`. All of these use `Array`’s each method to do their jobs,and if your class can implement an `each` method, you can `include Enumerable`, and get all those methods for free in your own class!

### Comparable


The Comparable module provides methods that give other classes comparison operators such as `< `(less than), `<=` (less than or equal to), `==` (equal to), `>=` (greater than or equal to), and `>` (greater than), as well as the `between?` method that returns `true` if the value is between (inclusively) the two parameters supplied (for example, `4.between?(3,10) == true`).

### Using Mix-Ins with Namespaces and Classes

```ruby
module ToolBox
  class Ruler
    attr_accessor :length
  end
end
module Country
  class Ruler
    attr_accessor :name
  end
end
a = ToolBox::Ruler.new
a.length = 50
b = Country::Ruler.new
b.name = "Genghis Khan of Moskau"
```
What if you wanted to assume temporarily that Ruler (with no module name prefixed) was `Country::Ruler`, and that if you wanted to access any other `Ruler` class, you’d refer to it directly? `include` makes it possible.
- In the previous sections, you’ve used `include` to include the methods of a module in the current class and scope, but it also includes the classes present within a module (if any) and makes them locally accessible too. Say, after the prior code, you did this:

```ruby
include Country
c = Ruler.new
c.name = "King Henry VIII"
```
The `Country` module’s contents (in this case, just the `Ruler` class) are brought into the current scope, and you can use `Ruler` as if it’s a local class. If you want to use the `Ruler` class located under `ToolBox`, you can still refer to it directly as `ToolBox::Ruler`.

#### Structs: Quick and Easy Data Classes

A struct is a special class whose only job is to have attributes and to hold data. Here’s a demonstration:

```ruby
Person = Struct.new(:name, :gender, :age)
fred = Person.new("Fred", "male", 50)
chris = Person.new("Chris", "male", 25)
puts fred.age + chris.age

# => 75
```
Simply, the `Struct` class builds classes to store data. On the first line you create a new class called `Person` that has built-in name, gender, and age attributes. On the second line you create a new object instance of `Person` and set the attributes on the fly. The first line is equivalent to this longhand method:

```ruby
class Person
  attr_accessor :name, :gender, :age
  def initialize(name, gender, age)
    @name = name
    @gender = gender
    @age = age
  end
end
```
> In actuality, this code is not *exactly* equivalent to the `struct` code (though pragmatically it’s close enough), because parameters are optional when initializing a `Struct` class, whereas the preceding `Person` class code requires the three parameters (`name`, `gender`, and `age`) be present.

## CHAPTER 7: Projects and Libraries

### Projects and Using Code from Other Files

The most common way to separate functionality in Ruby is to put different classes in different files. This gives you the ability to write classes that could be used in multiple projects simply by copying the file into your other project.

#### Basic File Inclusion

```ruby
puts "This is a test".vowels.join('-')
```
If you try to execute this code, you’ll get an error complaining that the `vowels` method is not available for the `"This is a test"` object of class `String`. This is true because Ruby doesn’t provide that method. Let’s write an extension to the `String` class to provide it:

```ruby
class String
  def vowels
   self.scan(/[aeiou]/i)
  end
end
```
If this definition were included in the same file as the prior puts code—say, my_test.rb—the result
would be as follows:

```ruby
i-i-a-e
```
In this case, you’ve extended String with a vowels method that uses scan to return an array of all the vowels (the i option on the end makes the regular expression case-insensitive).

- However, you might want to write a number of methods to add to `String` that you’d like to use in multiple programs. Rather than copy and paste the code each time, you can copy it to a separate file and use the `require` command to load the external file into the current program. For example, put this code in a file called `string_extensions.rb`:

```ruby
class String
  def vowels
   self.scan(/[aeiou]/i)
  end
end
```
And put this code in a file called `vowel_test.rb`:

```ruby
require './string_extensions'
puts "This is a test".vowels.join('-')
```
If you run `vowel_test.rb`, the expected result would appear onscreen. The first line, `require './ string_extensions'`, simply loads in the `string_extensions.rb` file from the current directory (as signified by the `./`) and processes it as if the code were local. This means that, in this case, the `vowels` method is available, all with a single line.


Ruby does not include the current directory in the path of directories to search for Ruby files by default, so you can either specify the current directory specifically by using `./`, as above, or by using `require_relative`. So this example is operationally identical to the previous one:

```ruby
require_relative 'string_extensions'
puts "This is a test".vowels.join('-')
```

As well as `require` and `require_relative`, you can use `load` to load external source code files into your program. For example, this code would seem to function identically to the preceding code:

```ruby
load 'string_extensions.rb'
puts "This is a test".vowels.join('-')
```
> load requires a full filename, including the .rb suffix, whereas require assumes the .rb suffix.

The output is the same in this case, but let’s try a different example to see the difference. Put this in `a .rb`:

```ruby
puts "Hello from a.rb"
```
And put this in a file called b.rb:

```ruby
require_relative 'a'
puts "Hello from b.rb"
require_relative 'a'
puts "Hello again from b.rb"
```
Run with ruby b.rb to get the result:

```
Hello from a.rb
Hello rom  b.rb
Hello again from b.rb
```
In this example, the `a.rb` file is included only once. It’s included on line 1, and `"Hello from a.rb"` gets printed to the screen, but then when it’s included again on line 3 of `b.rb`, nothing occurs. In contrast, consider this code:

```ruby
load 'a.rb'
puts "Hello from b.rb"
load 'a.rb'
puts "Hello again from b.rb"
```

```
Hello from a.rb
Hello from b.rb
Hello from a.rb
Hello again from b.rb
```
With `load`, the code is loaded and reprocessed anew each time you use the `load` method. `require` and `require_relative`, on the other hand, process external files only once.

> Ruby programmers nearly always use `require` or `require_relative` rather than `load`. The effects of `load` are useful only if the code in the external file has changed or if it contains active code that will be executed immediately. However, a good programmer will avoid the latter situation, and external files will only contain classes and *modules* that will, generally, rarely change.

#### Inclusions from Other Directories

`load` and `require_relative` can bring in local files, but `require` does not. `require 'a'` looks for `a.rb` in a multitude of other directories on your storage drive. By default, these other directories are the various directories where Ruby stores its own files and libraries, although you can override this, when necessary.
- Ruby stores the list of directories to search for included files in a special variable called `$:` (or, if you prefer, `$LOAD_PATH`). You can see what `$:` contains by default, using `irb`:
```
$:.each { |d| puts d }
# If you want to add directories to this, it’s simple:
$:.push '/your/directory/here'
require 'yourfile'
```
`$:` is an array, so you can push extra items to it or use `unshift` to add an element to the start of the list (if you want your directory to be searched before the default Ruby ones—useful if you want to override Ruby’s standard libraries)

#### Logic and Including Code

`require` and `load` both act like normal code in Ruby programs. You can put them at any point in your Ruby code and they’ll behave as if they were processed at that point. For example:
```
$debug_mode = 0
require_relative $debug_mode == 0 ? "normal-classes" : "debug-classes"
```
This gives you the power to include a different source file dependent on the value of a variable, ideal for situations where your application has “regular” and “debug” modes. You could even write an application that works perfectly, but then use a different `require` to include a whole different set of files that have new or experimental functionality.
- A commonly used shortcut uses arrays to quickly load a collection of libraries at once. For example:

```
%w{file1 file2 file3 file4 file5}.each { |l| require l }
```
However, some coders are not keen on this style, as it can make the code harder to read, even if it’s more efficient.

#### Nested Inclusions

Code from files that are included in others with `require` and `load` has the same freedom as if the
code were pasted directly into the original file. This means files that you include can call `load`, `require`, or `require_relative` themselves.For example, assume `a.rb` contains the following:
```
require_relative 'b'
# and b.rb contains the following:
require_relative 'c'
# and c.rb contains the following:
def example
  puts "Hello!"
end
# and d.rb contains the following:
require_relative 'a'
example
#  When d.rb is then run,

# => Hello!
```
### Libraries

#### The Standard Libraries

> Collectively the “standard libraries” are often called “the Standard Library.” When you see this term, it’s important to remember it most likely refers to the collection rather than one library in particular—a “library of libraries,” if you will.

##### net/http
Ruby provides basic support for HTTP via the `net/http` library. For example, it’s trivial to write a Ruby script that can download and print out the contents of a particular web page:
```
require 'net/http'
Net::HTTP.get_print('www.rubyinside.com', '/')
```
If you ran this code, after a few seconds many pages of HTML code should fly past on your screen. The first line loads the `net/http` library into the current program, and the second line calls a class method on the `Net::HTTP` class (where `Net` is a module defining the `Net` namespace, and `HTTP` is a subclass) that gets and prints (hence `get_print`) the web page at [http://www.rubyinside.com/](http://www.rubyinside.com/).

- It’s just as easy to put the contents of any web page into a string, for further manipulation by your program:
```ruby
require 'net/http'
url = URI.parse('http://www.rubyinside.com/')
response = Net::HTTP.start(url.host, url.port) do |http|
  http.get(url.path)
end
content = response.body
```
In this example, you use the URI library (another standard library, and one that’s loaded automatically by net/http) to decipher a URL such as [http://www.rubyinside.com/](http://www.rubyinside.com/) into its constituent parts for the `net/http` library to use to make its request. Once the URL has been parsed, an HTTP connection is “started,” and within the scope of that connection, a `GET` request is made with the `get` method (if this doesn’t make sense, don’t worry; it’s part of how the HTTP protocol works). Finally, you retrieve the content from `response.body`, a string containing the contents of the web page at [http://www.rubyinside.com/](http://www.rubyinside.com/).

> The `net/http` library is only a basic library, and it requires its input to be sanitized in advance, as in the preceding examples. The URI library is ideally suited to this task.

##### OpenStruct

The `OpenStruct` class provided by the `ostruct` library allows you to create data objects without specifying the attributes, and allows you to create attributes on the fly:
```ruby
require 'ostruct'
person = OpenStruct.new
person.name = "Fred Bloggs"
person.age = 25
```
`person` is a variable pointing to an object of class `OpenStruct`, and `OpenStruct` allows you to call attributes whatever you like, on the fly. It’s similar to how a hash works, but using the object notation.

> As the name implies, `OpenStruct` is more flexible than `Struct`, but this comes at the cost of harder-to- read code. There’s no way to determine exactly, at a glance, which attributes have been used. However, with traditional `struct`s, you can see the attribute names at the same place the `struct` is created.

#### RubyGems

- RubyGems is a packaging system for Ruby programs and libraries. It enables developers to package their Ruby libraries in a form that’s easy for users to maintain and install. RubyGems makes it easy to manage different versions of the same libraries on your machine, and gives you the ability to install them with a single line at the command prompt.

- Each individually packaged Ruby library (or application) is known simply as a gem or RubyGem. Gems have names, version numbers, and descriptions. You can manage your computer’s local installations of gems using the `gem` command, available from the command line. RubyGems comes standard with Ruby nowadays, but it was not included with distributions of Ruby 1.8 (except in certain situations, such as with the default installation of Ruby on Mac OS X). You no longer need to be concerned with how it is installed as it’s available "out of the box"!

##### Finding Gems

It’s useful to get a list of the gems that are installed on your machine, as well as get a list of the gems available for download and installation. To do this, you use gem’s `list` command. If you run `gem list` from your command line, you’ll get a result similar to this:
```
***  LOCAL   GEMS  ***
bigdecimal (1.2.6)
json (1.8.1)
minitest (5.4.3)
```
Your list of gems may be significantly longer than this, but as long as it looks like a list and not an error message, you’re good to go.
- You can query the remote gem server (currently hosted by rubygems.org, but you can add other sources later) like so:

```
gem list --remote
abstract (1.0.0)
ackbar (0.1.1, 0.1.0)
action_profiler (1.0.0)

# [..1,000s of lines about other gems removed for brevity..]
```
Wading through such a list is impractical for most purposes, but generally you’ll be aware of which gem you want to install before you get to this stage.

> However, if you wish to “browse,” the best way to do so is to visit [http://rubygems.org/](http://rubygems.org/), the home for the RubyGems repository. The site features search tools and more information about each gem in the repository.

##### Installing a Simple Gem

Once you’ve found the name of a gem you wish to install, you can install it with a single command at the command line (where `chronic` would be replaced with the name of the gem you wish to install, although feedtools is a fine gem to test with):
```
gem install chronic
```
If all goes well, you’ll get output like this:
```
Fetching: chronic-0.10.2.gem (100%)
Successfully installed chronic-0.10.2
Parsing documentation for chronic-0.10.2
Installing ri documentation for chronic-0.10.2
Done installing documentation for chronic after 1 seconds
1 gem installed
```
First, RubyGems looks to see if the gem exists in the current directory (you can keep your own store of gems locally, if you like), and if not, it heads off to `rubygems.org` to download the gem and install it from afar. Last, it builds the documentation for the library using rdoc (covered in Chapter 8), and installation is complete. This process is the same for nearly all gems.

> In many cases, installing one gem requires other gems to be installed too. That is, the gem you’re trying to install might have other gems it needs to operate, also known as "dependencies".

- If you are aware that you need to install a specific version of a gem (such as version 0.10.2 of Chronic, as above), you can specify this like so:
```
gem install -v 0.10.2 chronic
```

##### Using Gems

As the RubyGems system isn’t an integrated part of Ruby, it’s necessary to tell your programs that you want to use and load gems.

To demonstrate how gems can be used, you’ll install the redcloth gem, a library that can convert specially formatted text into HTML, ready to be used on a webpage. Use `gem install chronic` (or `sudo gem install chronic`,depending on your setup),as demonstrated earlier, to install the gem.

Once the gem is installed, run irb or create a new Ruby source file, and use the `chronic` gem like so:
```
require 'chronic'
puts Chronic.parse('may 10th')

# 2016-05-10 12:00:00 +0100
```
In this example, we load the Chronic library with require and then we can use the `Chronic` class to do
various things—in this case, time manipulation. Congratulations, you’ve used your first gem.

##### Upgrading and Uninstalling Gems

You can update all of your currently installed gems with a single line:
```
gem update
```
This makes RubyGems go to the remote gem repository, look for new versions of all the gems you currently have installed, and if there are new versions, install them. If you want to upgrade only a specific gem, suffix the preceding command line with the name of the gem in question.

- To uninstall gems, use the `uninstall` command (where `feedtools` is replaced by the name of the gem you wish to uninstall):
```
gem uninstall feedtools
```
> Again, remember to use sudo when the situation demands it, as covered in previous sections.

- If there are multiple versions of the same gem on the machine, RubyGems will ask you which version you want to uninstall first (or you can tell it to uninstall all versions at once), as in this example:
```
$ gem uninstall rubyforge

Select RubyGem to uninstall:
1. rubyforge-0.3.0
2. rubyforge-0.3.1
3. All versions
```

#### Bundler

Bundler ([http://bundler.io/](http://bundler.io/)) is a tool that was developed to help you manage the dependencies of a project (essentially, the libraries upon which your project depends) in a more structured way. It comes by default on some Ruby installs, but you can always ensure it's installed with `gem install bundler`.

- Consider, for example, that you create a project that depends on several libraries or gems. To run this application locally, you'd need to make sure that you have the right versions of each gem installed on your system. But if you have numerous projects with wide varieties of dependencies, you'll start to find it hard to track which gems you have installed and what versions they are. Bundler lets you create a file (called `Gemfile`) within a project's directory that specifies what libraries the project depends on. Here's an example of a very simple `Gemfile`:
```
source 'https://rubygems.org'
gem 'nokogiri'
gem 'rack', '~>1.1'
```
This specifies where the gems are to be downloaded from by default, and then which two gems the current project depends upon. Nokogiri is specified without a version number, but in Rack's case, a version query is specified at the end of the line which says any version that's 1.1 or above (but not version 2 or above - so 1.2, 1.3, 1.4, etc.).
- If you run `bundle install` from the directory where a `Gemfile` is present, Bundler ensures that the right gems are installed or upgraded to the right versions:
```
Fetching gem metadata from https://rubygems.org/.........
Fetching version metadata from https://rubygems.org/..
Resolving dependencies...
Using mini_portile2 2.0.0
Installing rack 1.6.4
Using bundler 1.11.2
Using nokogiri 1.6.7.2
Bundle complete! 2 Gemfile dependencies, 4 gems now installed.
Use 'bundle show [gemname]` to see where a bundled gem is installed.
```
The correct gems, as specified in `Gemfile`, are now installed. You can use these from within your project, orifyouwanttoensurethattherightversionsareloaded,youcanspecifyrequire `'bundler/setup'` within your program, like so:
```
require 'bundler/setup'
require 'rack'
# Now Rack 1.1 or above is loaded properly
```
- One other thing to be aware of is that when you install or upgrade gems, another file is created or updated called `Gemfile.lock`. This is not a file you are meant to change yourself, but it simply reflects what the precise set of dependencies are, along with their version numbers, so that if you distribute the project anywhere else, the very same set of libraries and versions will be installed properly. Here's an example of the Gemfile.lock produced by the install above:
```
GEM
  remote: https://rubygems.org/
  specs:
    mini_portile2 (2.0.0)
    nokogiri (1.6.7.2-x86-mingw32)
      mini_portile2 (~> 2.0.0.rc2)
    rack (1.6.4)
PLATFORMS
  x86-mingw32
DEPENDENCIES
  nokogiri
rack (~> 1.1)
BUNDLED WITH
   1.11.2
```
Even though our main `Gemfile` specifies any version of Rack over 1.0 and under 2.0, we specifically have 1.6.4 installed as that's the latest matching version at the time of writing. If I transferred this project to you in the future, however, 1.7 may be the latest matching Rack, and this could break the code. The `Gemfile.lock`’s job, therefore, is to explicitly communicate which versions of which libraries are working with the project right now.

## CHAPTER 8: Documentation, Error Handling, Debugging, and Testing

### Documentation

Ruby makes it extremely easy to document your code as you create it, using a utility called *RDoc* (standing for “Ruby Documentation”).

#### Generating Documentation with RDoc

RDoc calls itself a “Document Generator for Ruby Source.” It’s a tool that reads through your Ruby source code files and creates structured HTML documentation. It comes with the standard Ruby distribution, so it’s easy to find and use.
- RDoc understands a lot of Ruby syntax and can create documentation for classes, methods, modules, and numerous other Ruby constructs without much prompting.
- The way you document your code in a way that RDoc can use is to leave comments prior to the definition of the class, method, or module you want to document. For example:

```
# This class stores information about people.
class Person
  attr_accessor :name, :age, :gender
# Create the person object and store their name
  def initialize(name)
    @name = name
  end
# Print this person's name to the screen
  def print_name
    puts "Person called #{@name}"
  end
end
```
This is a simple class that’s been documented using comments. It’s quite readable already, but RDoc can turn it into a pretty set of HTML documentation in seconds.
- To use RDoc, simply run it from the command line using `rdoc <name of source file>.rb`, like so:
```
rdoc person.rb
```
> On Linux and OS X this should simply work “out of the box” (as long as the directory containing RDoc—usually `/usr/bin` or `/usr/local/bin`—is in the path). On Windows it might be necessary to prefix `rdoc` with its full location.

This command tells RDoc to process `person.rb` and produce the HTML documentation. By default, it does this by creating a directory called doc from the current directory and placing its HTML and CSS files in there. Once RDoc has completed, you can open `index.html`, located within `doc`, and you should see some basic documentation

#### RDoc Techniques

> The following sections give only a basic overview of some of RDoc’s features. To read the full documentation for RDoc and learn about features that are beyond the scope of this book, visit the official RDoc [site](http://rdoc.sourceforge.net/doc/)

#### Producing Documentation for an Entire Project

Previously you used rdoc along with a filename to produce documentation for a single file. However, in the case of a large project, you could have many hundreds of files that you want processed. If you run RDoc with no filenames supplied, RDoc will process all the Ruby files found in the current directory and all other directories under that. The full documentation is placed into the `doc` directory, as before, and the entire set of documentation is available from `index.html`.

##### Basic Formatting

To learn more about RDoc’s general formatting features, the best method is to look at existing code that is extensively prepared for RDoc, such as the source code to the Ruby on Rails framework, or refer to the documentation at [http://docs.ruby-lang.org/en/2.2.0/RDoc/Markup.html](http://docs.ruby-lang.org/en/2.2.0/RDoc/Markup.html).

#### Modifiers and Options

RDoc supports a number of modifiers within comments, along with a plethora of command-line options.

##### :nodoc: Modifier

Sometimes, you’d rather RDoc ignore certain modules, classes, or methods, particularly if you haven’t documented them yet. To make RDoc ignore something in this way, simply follow the module, class, or method definition with a comment of `:nodoc:`, like so:
```
# This is a class that does nothing
class MyClass
  # This method is documented
  def some_method
  end
  def secret_method #:nodoc:
  end
end
```
In this instance, RDoc will ignore `secret_method`.
- If you want :nodoc: to apply to the current element and all those beneath it (all methods within a class, for example), do this:

```
# This is a class that does nothing
class MyClass #:nodoc: all
  # This method is documented (or is it?)
  def some_method
  end
  def secret_method
  end
end
```

##### Turning RDoc Processing On and Off

You can stop RDoc from processing comments temporarily using `#++` and `#--`, like so:
```
# This section is documented and read by RDoc.
#--
# This section is hidden from RDoc and could contain developer
# notes, private messages between developers, etc.
#++
# RDoc begins processing again here after the ++.
```
This feature is particularly ideal in sections where you want to leave comments to yourself that aren’t for general consumption.
> RDoc doesn’t process comments that are within methods, so your usual code comments are not used in the documentation produced. RDoc will also not process comments that are separated from other comments with blank lines.

##### Command-Line Options

- `--all`: Usually RDoc processes only public methods, but `--all` forces RDoc to document *all* methods within the source files.
- `--fmt <format name>`: Produce documentation in a certain format (which currently includes darkfish, pot, and ri).
- `--help`: Get help with using RDoc’s command-line options and find out which output formatters are available.
- `--inline-source`: Usually source code is shown using popups, but this option forces code to be shown inline with the documentation.
- `--main <name>`: Set the class, module, or file that appears as the main index page for thedocumentationto<name>(forexample, `rdoc --main MyClass`).

After any command-line options, `rdoc` is suffixed with the filename(s) of the files you want to have RDoc document. Alternatively, if you specify nothing, RDoc will traverse the current directory and all subdirectories and generate documentation for your entire project.

> RDoc supports many more command-line options than these, and they are all covered in RDoc’s official documentation. Alternatively, run RDoc with `rdoc --help` at the command line to get a list of its options.

### Debugging and Errors

#### Exceptions and Error Handling

##### Raising Exceptions

In Ruby, exceptions are packaged into objects of class `Exception` or one of `Exception`’s many subclasses. Ruby has about 30 main predefined exception classes that deal with different types of errors, such as `NoMemoryError`, `StandardError`, `RuntimeError`, `SecurityError`, `ZeroDivisionError`, and `NoMethodError`.

When an exception is *raised* (exceptions are said to be *raised* when they occur within the execution of a program), Ruby immediately looks back up the tree of routines that called the current one (known as the *stack*) and looks for a routine that can handle that particular exception. If it can’t find any error-handling routines, it quits the program with the raw error message. For example:
```
irb(main):001:0> puts 10 / 0

ZeroDivisionError: divided by 0
        from (irb):1:in `/'
        from (irb):1
```
This error message shows that an exception of type `ZeroDivisionError` has been raised, because you attempted to divide ten by zero.
- Ruby can raise exceptions automatically when you perform incorrect functions, and you can raise exceptions from your own code too. You do this with the `raise` method and by using an existing exception class, or by creating one of your own that inherits from the `Exception` class.
- One of the standard exception classes is `ArgumentError`, which is used when the arguments provided to a method are fatally flawed. You can use this class as an exception if bad data is supplied to a method of your own:
```
class Person
  def initialize(name)
    raise ArgumentError, "No name present" if name.empty?
  end
end
```
If you create a new object from Person and supply a blank name, an exception will be raised:

```
fred = Person.new('')

# ArgumentError: No name present
```

> You can call `raise` with no arguments at all, and a generic `RuntimeError` exception will be raised. This is not good practice, though, as the exception will have no message or meaning along with it. Always provide a message and a class with `raise`, if possible.

- However, you could create your own type of exception if you wanted to. For example:

```
class BadDataException < RuntimeError
end

class Person
  def initialize(name)
    raise BadDataException, "No name present" if name.empty?
  end
end
```
At this point, it might seem meaningless as to why raising different types of exceptions is useful. The reason is so that you can handle different exceptions in different ways with your error-handling code, as you’ll do next.

##### Handling Exceptions

In most situations, stopping a program because of a single error isn’t necessary. The error might only be minor, or there might be an alternative option to try. Therefore, it’s possible to *handle* exceptions. In Ruby, the `rescue` clause is used, along with `begin` and `end`, to define blocks of code to handle exceptions. For example:

```
begin
  puts 10 / 0
rescue
  puts "You caused an error!"
end

# You caused an error!
```
In this case, `begin` and `end` define a section of code to be run, where if an exception arises, it’s handled with the code inside the `rescue` block.

This can become important in programs that rely on external sources of data. Consider this pseudo-code:

```
data = ""
begin
  <..code to retrieve the contents of a Web page..>
  data = <..content of Web page..>
rescue
  puts "The Web page could not be loaded! Using default data instead."
  data = <..load data from local file..>
end
puts data
```
This code demonstrates why handling exceptions is extremely useful. If retrieving the contents of a web page fails (if you’re not connected to the Internet, for example), then the error-handling routine rescues the exception, alerts the user of an error, and then loads some data from a local file instead—certainly better than exiting the program immediately!

- In the previous section we looked at how to create your own exception classes, and the motivation
for doing this is that it’s possible to rescue different types of exceptions in a different way. For example, you might want to react differently if there’s a fatal flaw in the code, versus a simple error such as a lack of network connectivity. There might also be errors you want to ignore, and only specific exceptions you wish to handle.

- `rescue`’s syntax makes handling different exceptions in different ways easy:
```
begin
  ... code here ...
rescue ZeroDivisionError
  ... code to rescue the zero division exception here ...
rescue YourOwnException
  ... code to rescue a different type of exception here ...
rescue
  ... code that rescues all other types of exception here ...
end
```
If a `ZeroDivisionError` is raised within the code between `begin` and the `rescue` blocks, the rescue `ZeroDivisionError` code is executed to handle the exception.

##### Handling Passed Exceptions


As well as handling different types of exceptions using different code blocks, it’s possible to *receive* exceptions and use them. This is achieved with a little extra syntax on the `rescue` block:
```
begin
  puts 10 / 0
rescue => e
  puts e.class
end

ZeroDivisionError
```
Rather than merely performing some code when an exception is raised, the exception object itself is assigned to the variable e, whereupon you can use that variable however you wish. This is particularly useful if the exception class contains extra functionality or attributes that you want to access.

#### Catch and Throw

Sometimes you want to be able to break out of a thread of execution (say, a loop) during normal operation in a similar way to an exception, but without actually generating an error. Ruby provides two methods, `catch` and `throw`, for this purpose.

- `catch` and `throw` work in a way a little reminiscent of `raise` and `rescue`, but `catch` and `throw` work with symbols rather than exceptions. They’re designed to be used in situations where no error has occurred, but being able to escape quickly from a nested loop, method call, or similar, is necessary.

- The following example creates a block using `catch`. The catch block with the `:finish` symbol as an argument will immediately terminate (and move on to any code after that block) if `throw` is called with the `:finish` symbol.
```
catch(:finish) do
  1000.times do
    x = rand(1000)
    throw :finish if x == 123
  end
  puts "Generated 1000 random numbers without generating 123!"
end
```
Within the `catch` block you generate 1,000 random numbers, and if the random number is ever 123, you immediately escape out of the block using throw `:finish`. However, if you manage to generate 1,000 random numbers without generating the number 123, the loop and the block complete, and you see the message. `catch` and `throw` don’t have to be directly in the same scope. `throw` works from methods called from within a `catch` block:

```
def generate_random_number_except_123
  x = rand(1000)
  throw :finish if x == 123
end

catch(:finish) do
  1000.times { generate_random_number_except_123 }
  puts "Generated 1000 random numbers without generating 123!"
end
```
This code operates in an identical way to the first. When throw can’t find a code block using `:finish` in
its current scope, it jumps back up the stack until it can.

#### The Ruby Debugger

Constantly editing and re-running your program gives you no insight into what’s actually happening deep within your code. Sometimes you want to know what each variable contains at a certain point within your program’s execution, or you might want to force a variable to contain a certain value. You can use `puts` to show what variables contain at certain points in your program, but you can soon make your code messy by interspersing it with debugging tricks.

- Ruby provides a debugging tool you can use to *step* through your code line by line (if you wish), set *breakpoints* (places where execution will stop for you to check things out), and debug your code. It’s a little like irb, except you don’t need to type out a whole program. You can specify your program’s filename, and you’ll be acting as if you are within that program.
- For example, create a basic Ruby script called `debugtest.rb`:

```
i= 1
j= 0
until i > 1000000
i *= 2
j += 1 end
puts "i = #{i}, j = #{j}"

# If you run this code with ruby `debugtest.rb`, you’ll get the following result:
i = 1048576, j = 20
```
But say you run it with the Ruby debugger like this:
```
ruby –r debug debugtest.rb
```
You’ll see something like this appear:
```
Debug.rb
Emacs support available
debugtest.rb:1:i = 1 (rdb:1)
```
This means the debugger has loaded. The third line shows you the current line of code ready to be executed (the first line, in this case), and the fourth line is a prompt that you can type on.

- The function of the debugger is similar to irb, and you can type expressions and statements directly onto the prompt here. However, its main strength is that you can use special commands to run `debugtest.rb` line by line, or set breakpoints and “watches” (breakpoints that rely on a certain condition becoming true—for example, to stop execution when *x* is larger than 10).
- Here are the most useful commands to use at the debugger prompt:
  - `list`: Lists the lines of the program currently being worked upon. You can follow list by a range of line numbers to show. For example, `list 2-4` shows code lines 2 through 4. Without any arguments, `list` shows a local portion of the program to the current execution point.
  - `step`: Runs the next line of the program. `step` literally steps through the program line by line, executing a single line at a time. After each step, you can check variables, change values, and so on. This allows you to trace the exact point at which bugs occur. Follow `step` by the number of lines you wish to execute if it’s higher than one, such as `step 2` to execute two lines.
  - `cont`: Runs the program without stepping. Execution will continue until the program ends, reaches a breakpoint, or a `watch` condition becomes `true`.
  - `break`: Sets a breakpoint at a particular line number, such as with `break 3` to set a breakpoint at line 3. This means that if you continue execution with `cont`, execution will run until line 3 and then stop again. This is useful for stopping execution at a place where you want to see what’s going on.
  - `watch`: Sets a condition breakpoint. Rather than choosing a certain line upon which to stop, you specify a condition that causes execution to stop. For example, if you want the program to stop when x is larger than 10, use `watch x > 10`. This is perfect for discovering the exact point where a bug occurs if it results in a certain condition becoming `true`.
  - `quit`: Exits the debugger.

A simple debugging session with your debugtest.rb code might look like this:
```
# ruby -r debug debugtest.rb
Debug.rb

Emacs support available.
debugtest.rb:1:i = 1
(rdb:1) list
[-4, 5] in debugtest.rb
=> 1 i = 1
2j= 0
3 until i > 1000000
4 i *= 2
5 j += 1
(rdb:1) step
debugtest.rb:2:j = 0
(rdb:1) i
1
(rdb:1) i = 100
100
(rdb:1) step
debugtest.rb:3:until i > 1000000
(rdb:1) step
debugtest.rb:4: i *= 2
(rdb:1) step
debugtest.rb:5: j += 1
(rdb:1) i = 200
(rdb:1) watch i > 10000
Set watchpoint 1:i > 10000
(rdb:1) cont
Watchpoint 1, toplevel at debugtest.rb:5 debugtest.rb:5: j += 1
(rdb:1) i
12800
(rdb:1) j
6
(rdb:1) quit
Really quit? (y/n) y
```
However, many Ruby developers don’t use the debugger particularly often, as its style of debugging and its workflow can seem a little out of date compared to modern techniques such as `test-driven development` and `unit testing`.

### Benchmarking and Profiling

Benchmarking is the process in which you get your code or application to perform a function (often many hundreds of times in succession to average out discrepancies), and the time it takes to execute is measured. You can then refer to these times as you optimize your code. If future benchmarks run faster than previous ones, you’re heading in the right direction. Luckily, Ruby provides a number of tools to help you benchmark your code.

#### Simple Benchmarking

```
require 'benchmark'
puts Benchmark.measure { 10000.times { print "." } }
```
This code measures how long it takes to print 10,000 periods to the screen. Ignoring the periods produced, the output (on my machine; yours might vary) is as follows:
```
0.050000     0.040000      0.090000 (  0.455168)
```
The columns, in order, represent the amount of user CPU time, system CPU time, total CPU, and “real” time taken. In this case, although it took nine-hundredths of a second of CPU time to send 10,000 periods to the screen or terminal, it took almost half a second for them to finish being printed to the screen among all the other things the computer was doing.

Because `measure` accepts code blocks, you can make it as elaborate as you wish:
```
require 'benchmark'
iterations = 1000000

b = Benchmark.measure do
  for i in 1..iterations do
x= i end
end

c = Benchmark.measure do
  iterations.times do |i|
x= i end
end

puts b
puts c
```
In this example, you benchmark two different ways of counting from one to one million. The results might look like this:
```
0.800000   0.010000   0.810000 ( 0.949338)
0.890000   0.010000   0.900000 ( 1.033589)
```

- `Benchmark` also includes a way to make completing multiple tests more convenient. You can rewrite the
preceding benchmarking scenario like this:

```
require 'benchmark'
iterations = 1000000

Benchmark.bm do |bm|
  bm.report("for:") do
    for i in 1..iterations do x= i
    end
  end
  bm.report("times:") do
    iterations.times do |i|
      x= i
    end
  end
end
```
The primary difference with using the bm method is that it allows you to collect a group of benchmark tests together and display the results in a prettier way. Example output for the preceding code is as follows:

```
          User        system          total       real
for:   0.850000      0.000000        0.850000 (  0.967980)
times: 0.970000      0.010000        0.980000 (  1.301703)
```

- Another method, `bmbm`, repeats the benchmark set twice, using the first as a “rehearsal” and the second for the true results, as in some situations CPU caching, memory caching, and other factors can taint the results. Therefore, repeating the test can lead to more accurate figures. Replacing the `bm` method with `bmbm` in the preceding example (for the `Benchmark` method) gives results like these:

```
Rehearsal ----------------------------------------
for:  0.780000   0.000001   0.780001 ( 0.958378)
times: 0.100000   0.010000   0.110000 ( 1.342837)
------------------------------- total: 0.890001sec
         User     system     total     real
for:  0.850000   0.000000   0.850000 ( 0.967980)
times: 0.970000   0.010000   0.980000 ( 1.301703)
```

#### Profiling

Whereas benchmarking is the process of measuring the total time it takes to achieve something and comparing those results between different versions of code, *profiling* tells you *what code* is taking *what amount of time*. For example, you might have a single line in your code that’s causing the program to run slowly, so by profiling your code you can immediately see where you should focus your optimization efforts.

> Some people consider profiling to be the holy grail of optimization. Rather than thinking of efficient ways to write your application ahead of time, some developers suggest writing your application, profiling it,
and then fixing the slowest areas. This is to prevent premature optimization. After all, you might prematurely optimize something that didn’t actually warrant it, but miss out on an area of code that could do with significant optimization.

- Ruby comes with a code profiler but it is increasingly showing its age, and I would recommend instead installing [ruby-prof](https://github.com/ruby-prof/ruby-prof). This is available as a gem, so can be simply installed with:
```
gem install ruby-prof
```
> The installation process on Windows is a little more involved, so look at the [ruby-prof GitHub repository](https://github.com/ruby-prof/ruby-prof) for further guidance.

Let’s say we have the following Ruby program:
```
require 'profile'
class Calculator
  def self.count_to_large_number x= 0
    100000.times { x += 1 }
  end
  def self.count_to_small_number x= 0
    1000.times { x += 1 }
  end
end

Calculator.count_to_large_number
Calculator.count_to_small_number
```
This can then be run using ruby-prof:
```
ruby-prof calculator.rb
```

-The result contains a number of columns. The first is the percentage of time spent within the method named in the far right column. In the preceding example, the profiler shows that 65.46 percent of the total execution time was spent in the `times` method in the `Integer class`. The second column shows the amount of time in seconds rather than as a percentage.

- The `calls` column specifies how many times that method was called. In our case, times was called only twice. This is true, even though the code block passed to times was run 101,000 times. This is reflected in the number of calls for `Fixnum`’s addition `(+)` method, with 101,000 total calls shown there.

- You can use the profiler’s results to discover the “sticky” points in your program and help you work around using inefficient methods that suck up CPU time. It’s not worth spending time optimizing routines that barely consume any time, so use the profile to find those routines that are using the lion’s share of the CPU, and focus on optimizing those.

> The reason larger numbers, such as the 1,000,000 loops in the benchmarking tests, weren’t used is because profiling adds a severe overhead to the operating speed of a program, unlike benchmarking. Although the program will run slower, this slowdown is consistent, so the accuracy of the profiling results is ensured regardless.

> ruby-prof can also be used from within code, rather than via the ruby-prof program, in order to profile certain pieces of code rather than an entire script. See ruby-prof’s documentation for more information.

--------

## [Posts](http://www.eriktrautman.com/posts/ruby-explained-numbers-operators-and-expressions) from Erik Trautman

#### Numbers, Operators and Expressions

- `==` **vs** `===` : `===` typically asks whether the thing on the right is a member or a part or a type of the thing on the left. If the thing on the left is the range `(1..4)` and we want to know if 3 is inside there:

```ruby
(1..4) === 3
# => true

Integer === 3
# => true
```
This also works for checking whether some object is an instance of a class as in the second example.

#### Objects and Methods

-  Methods like `#is_a?`, which tell you something about the object itself, are called **Reflection Methods** (as in, "the object quietly reflected on its nature and told me that it is indeed an Integer").

- **Bang Methods** are finished with an exclamation point `!` like `#sort!`, and they actually modify the original object.

#### Strings

- **Double quotes vs Single quotes**

There's almost no difference and you're free to use either. Two cases make the distinction important:

A) When you want to show quotes inside a string:

```ruby
my_long_string = "And she said, 'Cool program!'"
=> "And she said, 'Cool program!'"
```
Note that you can accomplish the same type of thing by escaping the quote characters.

B) When you want to use string interpolation (`#{}`) and when you want to show quotes within a string.

> The key point here, though, is that interpolation *only works inside DOUBLE quotes*.

- `#chomp` will cut off a space or newline at the END of the string (and can take an optional input so you can specify what exactly to chomp off).  `#strip` will remove ALL spaces and newlines from both the beginning and end of the string:

```ruby
" dude \n".chomp
# => " dude "          still have the extra spaces
" dude \n".strip
# => "dude"            clean as a whistle.
```

```ruby
"hello".gsub("l","r")
# => "herro"
```

```ruby
"hi".ljust(4)
# => "hi  "

"hi".ljust(6,"*")
# => "hi****"

"hi".rjust(6)
# => "    hi"

"hi".center(6,"!")
# => "!!hi!!"
```

#### Arrays

```ruby
d = %w{ I am not a crook } # converts the string (no quotes) to an Array
# => [ "I", "am", "not", "a", "crook" ]
empty_a = Array.new(5)
# => [nil, nil, nil, nil, nil]
full_a = Array.new(3, "hi")
# => ["hi", "hi", "hi"]
```

```ruby
[1,2,3] - [2,3,4]
# => [1]                # the 4 did nothing
[2,2,2,2,2,3,4] - [2, 5, 7]
# => [3,4]              # it killed ALL the 2's
```

```ruby
[1,2,3]&[2,4,5]
# => [2]   # If you want to find values in Both arrays, check their union using the ampersand &
```

- add or remove stuff from the **END** of the array:

```ruby
my_arr = [1,2,3]
# => [1,2,3]
my_arr.push(747)
# => [1, 2, 3, 747]
my_arr
# => [1, 2, 3, 747]     # warning: we modified my_arr!!!
my_arr.pop
# => 747
my_arr.pop
# => 3
my_arr
# => [1, 2]          # warning: pop also modified my_arr
```

- take the item off the **FRONT** of the array:

```ruby
my_arr = [1,2,3]
# => [1,2,3]
my_arr.shift
# => 1
my_arr
# => [2,3]          # warning: shift also modified my_arr!
my_arr.unshift(999)
# => [999, 2, 3]
my_arr
# => [999, 2, 3]    # warning: unshift... yep, modified my_arr.
```

- **Shovel Operator** `<<`: is *almost* identical to push:

```ruby
my_arr = [1,2,3]
# => [1,2,3]
my_arr << 3
# => [1, 2, 3, 3]
```
> For now, just think of it as the cool way of pushing onto an array. But note that `<<` is often overridden (like in Rails), and so it pays to be mindful of exactly what flavor of `push`ing you're doing.

- **Deleting items** anywhere you want:

```ruby
my_arr = [1,2,3]
# => [1, 2, 3]
my_arr.delete_at(1)
# => 2
my_arr
# => [1,3]
```

- **Clear out** the whole array:
```ruby
my_arr = [1,3,5]
# => [1,3,5]
my_arr.clear
# => []
my_arr = [1,3,5]
# => [1,3,5]
my_arr = []           # better
# => []
```

- **Includes an item** AT ALL:

```ruby
my_arr.include?(3)
# => true
my_arr.include?(132)
# => false
```

- To find **WHERE** a specific item lives in the array, use `#index` but note that it only returns the FIRST instance of this (and then gives up. Lazy method.):

```ruby
my_arr.index(3)
# => 2
[1,2,3,4,5,6,7,3,3,3,3,3].index(3)
# => 2                  # Just the index of the FIRST match
```

**A few useful and commonly used methods:**

- `#max` to find the **biggest value**
- `#min` to find the **smallest value**
- `#uniq` to **remove all duplicates**
- `#size` to find out **how big the array is**
- `#shuffle` to put the **array in random order**
- `#sort` to put the **array in order** Though `#sort` is pretty self-explanatory in the simple case, it can actually take parameters to let you decide if you want to sort things using a different (or reverse) methodology.
- `#sample` picks out a **random value** from the array... good for gambling games!
- `#first` gives you the **first item** (but doesn't remove it, so it's same as [0]) but can be more descriptive of your code's intent.
- `#last` is same as [-1]

- **Convert an Array into a String**

```ruby
["he", "llo"].join
# => "hello"
colorful_bugs = ["caterpillar", "butterfly", "ladybug"]
# => ["caterpillar", "butterfly", "ladybug"]
"I found a #{colorful_bugs.join(' and a ')} in the yard!"
# => "I found a caterpillar and a butterfly and a ladybug in the yard!"
```

- **Range into an Array:**

```ruby
my_awesome_array = (1..6).to_a
# => [1,2,3,4,5,6]
```

#### Hashes

- **Delete** from a hash by just setting the value to `nil` or by calling the  `#delete` method:

```ruby
> favorite_smells[:flower] = nil
=> nil
> favorite_smells
=> {:cooking => "bacon" }             # one deleted...
> favorite_smells.delete(:cooking)
=> "bacon"
> favorite_smells
=> {}                                 # ...and the other.
```

- **Add two hashes together:** If there are any conflicts, the incoming hash (on the right) overrides the hash actually calling the method (`#merge`)

```ruby
> favorite_beers = { :pilsner => "Peroni" }
=> { :pilsner => "Peroni" }
> favorite_animals.merge(favorite_beers)
=> {"mammals"=>"dog", "birds"=>"parrot", :pilsner => "Peroni"}
```

- **All the keys** or **All the values**:

```ruby
> favorite_animals.keys
=> ["mammals", "birds" :pilsner]
> favorite_animals.values
=> ["dog", "parrot", "Peroni"]
```

- **Sets:** A simpler kind of hash is called a Set, and it's just a hash where all the values are either True or False. It's useful because your computer can search more quickly through this than an array trying to store the same information due to the way it's set up behind the scenes.

#### Dates and Times

```ruby
> nownow = Time.now
=> 2013-07-10 17:37:27 -0700
> nownow.ctime                  # a standard display type
=> "Wed Jul 10 17:38:10 2013"
> nownow.utc                    # Remove the time zone
=> 2013-07-11 00:38:10 UTC
> nownow.strftime("%Y-%m-%d %H:%M:%S")
=> "2013-07-11 00:38:10"
```

- **Extra Stuff: Time Zones and Local Time** What's that trailing `-0800` in  `2012-02-14 00:00:00 -0800`? It's because that time was created on my local system, which is many hours "earlier" in the day from the Coordinated Universal Time (called UTC... no, it doesn't match up but [here's why](http://geography.about.com/od/timeandtimezones/a/gmtutc.htm)) which is used by computers around the world as the standard benchmark time (so two computers communicating about times will always be talking about the same exact one and not have to worry about time zones).

I prefer to think of UTC as "Universal Time Code" because reasons. UTC is the new GMT... Greenwich Mean Time. You'll start thinking of things in terms of "how many hours away am I from England?" when you run into time zone bugs somewhere down the road.

#### Other Random Tidbits

- **Parallel Assignment**

```ruby
> a, b = 1, "hi"
=> [1, "hi"]      # ignore this output
> a
=> 1
> b
=> "hi"
> my_array = [1,2,3,4]
=> [1,2,3,4]
> my_array[1], my_array[3] = 100, 200
=> [100,200]      # ignore
> my_array
=> [1,100,3,200]
```

- **Swapping two variables**

```ruby
> a = 10
> b = 20
> a,b = b,a
> a
=> 20
> b
=> 10
```

- `blank?` **and** `empty?` are similar -- both basically check if the object has nothing in it -- but `#blank?` will also ignore any whitespace characters. *Note that `#blank?` is a method provided by Rails and is not available in Ruby*.

- We've seen lots of `#puts` so far but you've probably also run across `p` **What's the Difference?**  `p` will give you some more information because it runs the `#inspect` method on the object while `#puts` runs the `#to_s` method.  `#inspect` is meant to be informative where `#puts` is "pretty". The difference may not be readily apparent while you're only working with simple objects like strings and arrays, but you'll notice it when you start creating your own objects and you want to see what's inside (without typing out `puts my_object.inspect`).

#### Iteration

- `loop` is the most basic way to loop in Ruby and it's not used all that much because the other ways to loop are much sexier. `loop` takes a block of code, denoted by either `{ ... }` or `do ... end` (if it's over multiple lines). It will keep looping until you tell it to stop using a  `break` statement:

```ruby
i=0                   # Our index variable
loop do
  i+=1
  print "#{i} "
  break if i==10
end

# 1 2 3 4 5 6 7 8 9 10 => nil
```

> `while` performs a similar function but in a much more compact way, by allowing you to specify the condition that must be true to keep looping, and you'll find yourself using it much more in your own code.
> `until` is almost identical to `while` but, instead of running as long as the specified condition is `true`, it runs as long as the condition is  `false`.

- `for` is a looping mechanism present in lots of other languages but it gets de-emphasized in Ruby and you don't see it used much. A common use is to loop over every number in a range. You name the variable that holds the current number at the top and can then access it from inside the loop:

```ruby
for a_number in (1..3)
  print "#{a_number} "
end

# 1 2 3 => 1..3
```

- A couple other methods with similar purposes to `for` are `#times`, `#each`, `#upto`, `#downto`.

> Your best friends early on will be `while` for anything that needs to run until a certain condition is reached (like winning the game), `#each` for any time you want to do stuff with every item in an array or hash, and  `#times` for the simple cases when you just want to do something a fixed number of times.

- Use these statements to jump in and out of them for certain abnormal conditions:
  - `break` will **stop the current loop**. Often used with an `if` to specify under what conditions to do that.
  - `next` will **jump to the next iteration**. Also usually used with an if statement.
  - `redo` will let you restart the loop (without evaluating the condition on the first go-through), again usually with some condition
  - `retry` works on most loops (not `while` or `until`) similarly to `redo` but it *will* re-evaluate the condition before running through the loop again (hence *try* instead of *do*).
  > NOTE: Do NOT use `return` to exit a loop, since that will exit the whole method that contains it as well!

#### Blocks, Procs, and Lambdas, aka "Closures"

- How does `#each` take a block then? Through the magic of **the `yield` statement**, which basically says "run the block right here".

```ruby
class Array
  def my_each
    i = 0
    while i < self.size
        yield(self[i])
        i+=1
    end
    self
  end
end
```
What if you want to pass TWO blocks to your function? What if you want to save your block to a variable so you can use it again later? That's a job for **Procs**, aka Procedures! Actually, a block *is* a Proc (which is the class name for a block) and they rhyme just to confuse you. The block is sort of like a stripped-down and temporary version of a Proc that Ruby included just to make it really easy to use things like those  `#each` iterators.

```ruby
my_proc = Proc.new { |arg1| print "#{arg1}! " }
[1,2,3].each(&my_proc) # Use that block of code (now called a Proc) as an input to a function by prepending it with an apersand &:

# 1! 2! 3! =>[1,2,3]
```
- When you create your own function to accept procs, the guts need to change a little bit because you'll need to use `#call` instead of `yield` inside (because which proc would `yield` run if you had more than one?).  `#call` literally just runs the Proc that is called on. You can give it arguments as well to pass on to the Proc:

```ruby
my_proc.call("howdy ")
```
- If Procs are sort of a more-fleshed-out version of blocks, then lambdas are sort of a more-fleshed-out version of Procs. They are one step closer to being actual methods themselves, but still technically count as anonymous functions.
  - A lambda gives you more flexibility with what it returns (like if you want to return multiple values at once) because you can safely use the explicit `return` statement inside of one. With lambdas, `return` will only return from the lambda itself and not the enclosing method, which is what happens if you use `return` inside a block or Proc.
  - Lambdas are also much stricter than Procs about you passing them the correct number of arguments (you'll get an error if you pass the wrong number).

Here's a simple example to show you the syntax of a lambda (btw, there's nothing special to lambdas about placing the `#call` after the  `end`, if you hadn't seen that done before, it's just like method chaining):
```ruby
lambda do |word|
  puts word
  return word            # you can do this in lambdas not Procs
end.call("howdy ")

# howdy => "howdy "        not nil because we gave it a return
```
- To sum up
  - **Blocks** are unnamed little code chunks you can drop into other methods. Used all the time.
  - **Procs** are identical to blocks but you can store them in variables, which lets you pass them into functions as explicit arguments and save them for later. Used explicitly sometimes.
  - **Lambdas** are really full methods that just haven't been named. Used rarely.
  - **Methods** are a way of taking actual named methods and passing them around as arguments to or returns from other methods in your code. Used rarely.
  - **Closure** is just the umbrella term for all four of those things, which all somehow involve passing around chunks of code.

#### Map, Select, and Other Enumerable Methods

```ruby
my_array = [1,2,3,4,5,6,7,8,100]
my_array.select{|item| item%2==0 }
# => [2,4,6,8,100]      wow, that was easy.

my_array.collect{|num| num**2 }
# => [4,16,36,64,10000]
```
> `#map` vs `#collect` It's the EXACT same method as collect, just called something different. It's more conventional to use `#map` but both work the same way.

```ruby
u = User.all
@user_emails = u.map { |user| user.email }
```

```ruby
my_hash = {"Joe" => "male", "Jim" => "male", "Patty" => "female"}
my_hash.select{|name, gender| gender == "male" }
# => {"Joe" => "male", "Jim" => "male"}
```
- **Enumerable Iterators Cheat Sheet**
  - `#each` returns the original object it was called on because it's really used for its side effects and not what it returns
  - `#each_with_index` passes not just the current item but whatever position in the array it was located in.
  - `#select` returns a new object (e.g. array) filled with only those original items where the block you gave it returned `true`
  - `#map` returns a new array filled with whatever gets returned by the block each time it runs.

- **Some Other Handy Methods**
  - `#any?` returns true/false (see the question mark?) and answers the question, "do ANY of the elements in this object pass the test in my block?". If your block returns true on any time it runs, `any?` will return true.
  - `#all?` returns true/false and answers the question, "do ALL the elements of this object pass the test in my block?". Every time the block runs it must return true for this method to return true.
  - `#none?` returns true only if NONE of the elements in the object return true when the block is run.
  - `#find` returns the first item in your object for which the block returns true.

  ```ruby
  ages = [[:frank, 42], [:sue, 77], [:granny, 77]]
  ages.find do |name, age|
    age == 77
  end
  # => [:sue, 77] Get the first person from the ages array that is 77 years old.
  ```
  - `#find_all` or `#select` finds the all elements.
  ```ruby
  test_scores.select do |name, score|
    score > 80
  end
  # => [["jon", 99], ["bill", 85]] array of all students with test scores greater than 80.
  ```
- **Awesome but less common methods**
  - `#group_by` will run your block and return a hash that groups all the different types of returns from that block. For example:
  ```ruby
  names = ["James", "Bob", "Joe", "Mark", "Jim"]
  names.group_by{|name| name.length}
  # => {5=>["James"], 3=>["Bob", "Joe", "Jim"], 4=>["Mark"]}
  ```
  - `#grep` returns an array with those items that actualy match the specified criteria (RegEx) (using a `===` match)
  ```ruby
  names.grep(/J/)
  # => ["James", "Joe", "Jim"]
  ```

#### Classes

We've been over storing data in hashes, but what happens when you want to treat that data like a real object and make it move? Or if you want to handle 10,000 different instances of it? When you just store your `Viking`'s `name`, `age`, `health`, and `strength`, it just kind of sits there. What about when you want to make an army of `Viking`s who can do stuff like `#eat`, `#travel`, `#sleep` and, of course, `#attack`? For that, you need a slightly more complex structure to make your `Viking` out of, so you give it its own `Viking` class.

We've been dealing with classes since the very beginning, when it became clear that everything in Ruby is an object, whether strings, hashes, arrays or numbers, and these objects are instances of some type of class.

- To be able to amass a horde of 100 `Viking`s, you need a way to create new ones. Each time you do that, it's called **Instantiating** a new `Viking`. You use a special `::new` method to do that. You've done it many times for the `Array` class already:

```ruby
my_arr = Array.new
# => []
```
`::new` is a **Class Method**, which means that you call it on the class (`Array` here) and not the specific instance of that class (which would be `my_arr` here). It's also why we designate it with the two colons `::` when talking about it here.

- Classes share their methods, but what about variables? You don't want all your Vikings to have the same strength, so we use **instance variables** to take care of that. You designate an instance variable using the `@variable_name` notation.
- These instance variables are part of setting up your object's *state*.
- You'd usually set them up in your `#initialize` method:

```ruby
class Viking
    def initialize(name, age, health, strength)
        @name = name
        @age = age
        @health = health
        @strength = strength
    end
end

oleg = Viking.new("Oleg", 19, 100, 8)
# => #<Viking:0x007ffc0597bae0>     That's the position in the computer's memory that the viking object is stored.
```

- The class name is always capitalized and, for multiple words, uses **CamelCase** not the **snake_case** you've typically seen for variables.

- Since the methods get called on an individual instance of the Viking class, they're called **Instance Methods**, just the same as all your old friends like `#each` and `#sort` and `#max` etc. We just usually don't call them "instance" methods so maybe it wasn't obvious.

- So now you want to know what oleg's health is:

```ruby
oleg.health
NoMethodError: undefined method 'health' for #<Viking:0x007ffc0597bae0>
```
Woah! The instance variables are a part of oleg but you can't access them from outside him because it's really nobody's business but his. So you have to create a method specifically to get that variable, called a **getter** method, and just name it the same thing as the variable you want:

```ruby
def health
    @health
end

oleg.health
# => 87
```
That was easy! What if you decide that you want to set that variable yourself? You need to create a **setter** method, which is similar syntax to the getter but with an equals sign and taking an argument:

```ruby
def health=(new_health)
    @health = new_health
end
```

- Well, you can imagine that you'll probably be writing a whole lot of those methods, so Ruby gives you a helper method called  `attr_accessor`, which will create those getters and setters for you. Just pass it the symbols for whatever variables you want to make accessible and POOF! those methods will now exist for you to use:

```ruby
class Viking
    attr_accessor :name, :age, :health, :strength
    # codecodecode
end
```

- Because of your getters and setters, there are two different ways to access an instance variable from inside your class, either calling it normally using `@age` or calling the method on the instance using `self`. Since the original method (below it's `#take_damage`) is being called on an instance of the class, that instance becomes `self`. An example is clearer:

```ruby
class Viking
    ...
    def take_damage(damage)
        self.health -= damage
        # OR we could have said @health -= damage
        self.shout("OUCH!")
    end
    def shout(str)
        puts str
    end
    ...
end
```
You can also call methods from within other methods, as we saw with  `#shout` above. In that case, the `self` is actually optional because Ruby assumes if you just type `shout("OUCH!")` that you're trying to run the method `#shout` and Ruby will see if the method exists. That works 90% of the time, unless you've done something that overrides Ruby's assumption that you're trying to run a method, like using the `=` assignment operator:

```ruby
...
    def sleep
        health += 1 unless health >= 99   # ! FAIL !
    end
...
```
Here, Ruby assumes you're trying to set up a new `health` variable using `#health=` instead of accessing the one that currently exists as  `@health`. Just an edge case to watch out for if you start eliminating your `self`'s.

- Let's zoom away from the instance level and back to the class level for a second. Just like you've got instance variables and instance methods, you also get **class variables** and class methods. Class variables, denoted with TWO `@@`'s, are owned by the class itself so there is only one of them overall instead of one per instance.

In this example, we assume that all Vikings start with the same health, so we don't make it a parameter you can pass in:

```ruby
class Viking
    @@starting_health
    def initialize(name, age, strength)
        @health = @@starting_health
        # ...other stuff
    end
end
```
What about class methods? You define a class method by preceding its name with `self` (e.g. `def self.class_method`) or, identically, just the name of the class (e.g. `def Viking.class_method`). There's a less common method that puts the line `class << self` ahead of your method definitions (which won't use `self` anymore)

- There are two good times to use class methods: when you're building new instances of a class that have a bunch of known or "preset" features, and when you have some sort of utility method that should be identical across all instances and won't need to directly access instance variables.
- The first case is called a `factory method`, and is designed to save you from having to keep passing a bunch of parameters manually to your  `#initialize` method:

```ruby
class Viking
    def initialize(name, health, age, strength)
        #... set variables
    end
    def self.create_warrior(name)
        age = rand * 20 + 15   # remember, rand gives a random 0 to 1
        health = [age * 5, 120].min
        strength = [age / 2, 10].min
        Viking.new(name, health, age, strength)  # returned
    end
end

sten = Viking.create_warrior("Sten")
# => #<Viking:0x007ffc05a79848 @age=21.388120526202737, @name="Sten", @health=106.94060263101369, @strength=10>
```

- The second case above is more mundane. Often, there are things you need all Vikings to "know" or be able to do:

```ruby
class Viking
    ...
    def self.random_name      # useful for making new warriors!
        ["Erik","Lars","Leif"].sample
    end
    def self.silver_to_gold(silver_pieces)
        silver_pieces / 10
    end
    class << self           # The less common way
        def gold_to_silver(gold_pieces)
            gold_pieces * 10
        end
    end
end

warrior1 = Viking.create_warrior(Viking.random_name)
# => #<Viking:0x007ffc05a745c8 @age=22.369775138257097, @name="Lars", @health=111.84887569128549, @strength=10>
```
- **Quick Basics**
  - Classes are useful to use when you want to give methods to your data or have multiple instances of your data.
  - Class methods have access to other class methods and class variables but don't have access to instance methods or instance variables
  - Instance methods can call other instance methods, instance variables, class methods, or class variables

- **Class variables vs constants:** they are only similar in that all instances have access to them. If you've got something that will never, CAN never change, use a constant. If you might ever change it, stick with a class variable. At the very least, it makes your code much more legible.

- **Class vs Module:** *If you often create a class so it can use methods, what's the difference?* Basically, a class can be instantiated but a module *(it can be thought as the nice packages of methods that you can mix into classes)* cannot. A module will never be anything other than a library of methods. A class can be so much more -- it can hold its state (by keeping track of instance variables) and be duplicated as many times as you want. It's all about *objects*. If you need to instantiate something or otherwise have it exist over time, that's when you need to use a class instead of a module.

----------

In Ruby, a class **inherits** from another class using the `<` notation. Unlike some other languages, a class can only have ONE parent.

```ruby
class Viking < Person
```
Now `Viking` has access to all of `Person`'s methods. You say that  `Viking` **Extends** `Person`.

- *Overwriting* existing methods. It would cause all kinds of problems here, but we could do:

```ruby
class Array
    def each
        puts "HAHA no each here!"
    end
end

[1,2,3].each {|item| puts item }
# HAHA no each here!
# => nil
```
If `Viking` extends `Person`, you similarly have the option to overwrite any of `Person`'s methods. Maybe Vikings `#heal` twice as fast as normal people. You could write:

```ruby
class Person
    MAX_HEALTH = 120
    ...
    def heal
        self.health += 1 unless self.health + 1 > MAX_HEALTH
    end
end

class Viking < Person
    ...
    def heal
        self.health = [self.health + 2, MAX_HEALTH].min
        puts "Ready for battle!"
    end
end
```
That's one way... but we could also do it by calling the parent's `#heal` method directly a couple of times using the special `#super` method. `#super` lets you call the superclass's version of your current method.

```ruby
class Viking < Person
    ...
    def heal
        2.times { super }
        puts "Ready for battle!"
    end
end
```
You will often use that in your `#initialize` method when you want to use the parent's `#initialize` but just add a tweak or two of your own. You can pass in parameters as needed:

```ruby
class Viking < Person
    def initialize(name, health, age, strength, weapon)
        super(name, health, age, strength)
        @weapon = weapon
    end
end
```

#### Inheritance and Scope

By default, instance methods can be called by any instance of a class (e.g. `oleg.sleep`) and class methods can be called directly on the class itself (e.g. `Viking.new`).
- But what if we've got a really sensitive method like `#die` that we don't want anyone else to be able to call directly... it should ONLY be available to other methods from within THAT PARTICULAR instance of a Viking. So we don't want to be able to say > `oleg.die` from the command line, but we do want to be able to kill off oleg if he loses all his health. So we create a chunk of code marked `private`:

```ruby
class Viking < Person
    ...
    def take_damage(damage)
        @health -= damage
        die if @health <= 0
    end
    private
      def die
          puts "#{self.name} has been killed :("
          self.dead = true    # assume we've defined a `dead` instance variable
      end
end

oleg = Viking.create_warrior("Oleg")
oleg.die
NoMethodError: private method `die' called for #<Viking:0x007ffd4c041e50>
oleg.take_damage(200)
# Oleg has been killed :(
# => true
```
If you create methods that should only be accessible by other methods within your class, make them `private`. This is the default setting for instance variables unless you expose them using the afore-mentioned  `attr_accessor`.

> You should change the default thought in your head from "everything is accessible, what do I need to hide?" to "everything should be hidden, what do I absolutely need to make externally available?" That principle will take you far, especially when designing things like APIs that will be used by other programs. The more you make available to people, the harder it will be later on to hide it again.

- In our above example, there's really no reason for us to be able to directly call `#take_damage` on our Viking instance either... it's an implementation detail (why would a user ever need to say `oleg.take_damage(10)` directly? So we should probably rearrange things a bit to provide an even more high-level method to abstract `#take_damage` away from our user.

- If we create an `#attack` method for one instance to `#attack` another, then we can have that method deal with the damage stuff on its own so the user is none-the-wiser. But we can't make our `#take_damage` method `private` because otherwise we could only call it on the specific viking who is DOING the attacking. We want to call it on the RECIPIENT of the attack (remember, `private` methods can only be called from within the same instance).

- Since we don't want `#take_damage` to be visible to anyone on the command line but we DO want it to be visible to the methods inside other instances of `Viking`, we call that `protected`. `protected` provides most of the privacy of `private` but lets the methods inside other instances of the same class or its descendents also access it:

```ruby
class Viking < Person
    ...
    def attack(recipient)
        if recipient.dead
            puts "#{recipient.name} is already dead!"
            return false
        end
        damage = (rand * 10 + 10).round(0)
        recipient.take_damage(damage)  # `take_damage` called on `recipient`!
    end
    protected
        def take_damage(damage)
            self.health -= damage
            puts "Ouch! #{self.name} took #{damage} damage and has #{self.health} health left"
            die if @health <= 0
            # `die` called from within the same object as take_damage was (the `recipient` as well!)
        end
    private
        def die
            puts "#{self.name} has been killed :("
            self.dead = true  # assume we've defined a `dead` instance variable
        end
end

> oleg = Viking.create_warrior("Oleg")
 => #<Viking:0x007ffd4b8b5588 @age=24.58111251562904, @name="Oleg", @health=120, @strength=10, @dead=false>
> sten = Viking.create_warrior("Sten")
 => #<Viking:0x007ffd4b8e1700 @age=28.80998656037281, @name="Sten", @health=120, @strength=10, @dead=false>
> 10.times { oleg.attack(sten) }
Ouch! Sten took 19 damage and has 101 health left
Ouch! Sten took 10 damage and has 91 health left
Ouch! Sten took 13 damage and has 78 health left
Ouch! Sten took 17 damage and has 61 health left
Ouch! Sten took 15 damage and has 46 health left
Ouch! Sten took 11 damage and has 35 health left
Ouch! Sten took 14 damage and has 21 health left
Ouch! Sten took 14 damage and has 7 health left
Ouch! Sten took 18 damage and has -11 health left
Sten has been killed :(
Sten is already dead!
 => 10
> sten
=> #<Viking:0x007ffd4c048840 @age=25.601709008134428, @name="Sten", @health=-11, @strength=10, @dead=true>
```
--------
## Exception and Error Handling from [The Bastards Book of Ruby](http://ruby.bastardsbook.com/chapters/exception-handling/)

### Demonstarting Exceptions
Before the formal description of the `begin/rescue` block, let's walk through a couple examples of it in action. At a skin-deep level, it behaves nearly the same as the `if/else` construct.

#### Skipping past an error

The begin/rescue block is typically used on code in which you anticipate errors. There's only one line here for us to worry about:
```ruby
a = 10
b = "42"

begin
   a + b
rescue
   puts "Could not add variables a (#{a.class}) and b (#{b.class})"
else
   puts "a + b is #{a + b}"
end
```
The `puts` statement in the `rescue` clause executed. And more importantly, the Ruby program *did not crash*.

```ruby
while 1
   puts "Enter a number>>"
   begin
     num = Kernel.gets.match(/\d+/)[0]
   rescue
     puts "Erroneous input! Try again..."
   else
     puts "#{num} + 1 is: #{num.to_i+1}"
   end
end
```
The resulting output:

```ruby
Enter a number>>
8
8 + 1 is: 9
Enter a number>>
eight
Erroneous input! Try again...
Enter a number>>
8
8 + 1 is: 9
Enter a number>>
```
If a failure occurs, the program enters the rescue branch of code; else, the program goes on as normal. We now have a program that both:
  - Notifies the user of the existence of an error
  - Does not simply crash out because of the error


### The Begin...Rescue block

This is the most basic error handling technique. The main idea is to wrap any part of the program that could fail in this block. Commands that work with outside input, such as downloading a webpage or making calculation something based from user input, are points of failure.

```ruby
require 'open-uri'
require 'timeout'

remote_base_url = "http://en.wikipedia.org/wiki"

start_year = 1900
end_year = 2000

(start_year..end_year).each do |yr|
 begin
   rpage = open("#{remote_base_url}/#{yr}")
 rescue StandardError=>e
   puts "Error: #{e}"
 else
   rdata = rpage.read
 ensure
   puts "sleeping"
   sleep 5
 end
 if rdata
   File.open("copy-of-#{yr}.html", "w"){|f| f.write(rdata) }
 end
end
```
- `ensure` This branch will execute whether an error/exception was rescued or not. Here, we've decided to `sleep` for `3` seconds no matter the outcome of the `open` method.

### Flow of exception handling

#### Using `retry`

The `retry` statement redirects the program back to the `begin` statement. This is helpful if your begin/rescue block is inside a loop and you want to retry the same command and parameters that previously resulted in failure.

Here's a simple example; I use the `raise` statement to create my own `Exception` to be caught:
```
for i in 'A'..'C'
  retries = 2
  begin
    puts "Executing command #{i}"
    raise "Exception: #{i}"
  rescue Exception=>e
    puts "\tCaught: #{e}"
    if retries > 0
      puts "\tTrying #{retries} more times\n"
      retries -= 1
      sleep 2
      retry
    end
  end
end
```
The output:
```
Executing command A
   Caught: Exception: A
   Trying 2 more times
Executing command A
   Caught: Exception: A
   Trying 1 more times
Executing command A
   Caught: Exception: A
Executing command B
   Caught: Exception: B
   Trying 2 more times
Executing command B
   Caught: Exception: B
   Trying 1 more times
Executing command B
   Caught: Exception: B
Executing command C
   Caught: Exception: C
   Trying 2 more times
Executing command C
   Caught: Exception: C
   Trying 1 more times
Executing command C
   Caught: Exception: C
```

##### Using `retry` with `OpenURI`

To see an example please visit [this link](http://ruby.bastardsbook.com/chapters/exception-handling/) and find the subtitle as stated above.

### Exception and Error Classes

This section will make more sense if you have a little understanding of object-oriented programming. If you don't have time [to read the chapter on it](http://ruby.bastardsbook.com/chapters/oops/), the basic concept as it relates to exceptions and errors is this:
  - Every type of error and exception is derived from the `Exception` class
  - If your code rescues a `StandardError`, it will only rescue errors that are derived from StandardError.
  - If your code rescues an `Exception`, it will basically handle every possible error that could happen, including all errors of `StandardError` type and its children types.
You can see the [family tree of `Exception` here](http://ruby.bastardsbook.com/chapters/exception-handling/#exception-tree).

## Ruby Style Guide from [bbatsov/ruby-style-guide](https://github.com/bbatsov/ruby-style-guide)

### Source Code Layout

- Use two **spaces**

```
# bad - four spaces
def some_method
    do_something
end

# good
def some_method
  do_something
end
```

- Prefer a single-line format for **class definitions** with no body.

```
# bad
class FooError < StandardError
end

# okish
class FooError < StandardError; end

# good
FooError = Class.new(StandardError)
```

- Avoid single-line methods.

```
# bad
def too_much; something; something_else; end

# okish - notice that the first ; is required
def no_braces_method; body end

# okish - notice that the second ; is optional
def no_braces_method; body; end

# okish - valid syntax, but no ; makes it kind of hard to read
def some_method() body end

# good
def some_method
  body
end
```
One exception to the rule are empty-body methods.
```
# good
def no_op; end
```
- Use spaces around operators, after commas, colons and semicolons. Whitespace might be (mostly) irrelevant to the Ruby interpreter, but its proper use is the key to writing easily readable code.

```
sum = 1 + 2
a, b = 1, 2
class FooError < StandardError; end
```
There are a few exceptions. One is the exponent operator:
```
# bad
e = M * c ** 2

# good
e = M * c**2
```
Another exception is the slash in rational literals:
```
# bad
o_scale = 1 / 48r

# good
o_scale = 1/48r
```
- No spaces after `(`, `[` or before `]`, `)`. Use spaces around `{` and before `}`.

```
# bad
some( arg ).other
[ 1, 2, 3 ].each{|e| puts e}

# good
some(arg).other
[1, 2, 3].each { |e| puts e }
```
For hash literals two styles are considered acceptable. The first variant is slightly more readable (and arguably more popular in the Ruby community in general). The second variant has the advantage of adding visual difference between block and hash literals. Whichever one you pick—apply it consistently.
```
# good - space after { and before }
{ one: 1, two: 2 }

# good - no space after { and before }
{one: 1, two: 2}
```
- No space after `!`.

```
# bad
! something

# good
!something
```
- No space inside range literals.

```
# bad
1 .. 3
'a' ... 'z'

# good
1..3
'a'...'z'
```

- Indent `when` as deep as `case`. This is the style established in both "The Ruby Programming Language" and "Programming Ruby".

```
# bad
case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration > 120
    puts 'Too long!'
  when Time.now.hour > 21
    puts "It's too late"
  else
    song.play
end

# good
case
when song.name == 'Misty'
  puts 'Not again!'
when song.duration > 120
  puts 'Too long!'
when Time.now.hour > 21
  puts "It's too late"
else
  song.play
end
```
- When assigning the result of a conditional expression to a variable, preserve the usual alignment of its branches.

```
# bad - pretty convoluted
kind = case year
when 1850..1889 then 'Blues'
when 1890..1909 then 'Ragtime'
when 1910..1929 then 'New Orleans Jazz'
when 1930..1939 then 'Swing'
when 1940..1950 then 'Bebop'
else 'Jazz'
end

result = if some_cond
  calc_something
else
  calc_something_else
end

# good - it's apparent what's going on
kind = case year
       when 1850..1889 then 'Blues'
       when 1890..1909 then 'Ragtime'
       when 1910..1929 then 'New Orleans Jazz'
       when 1930..1939 then 'Swing'
       when 1940..1950 then 'Bebop'
       else 'Jazz'
       end

result = if some_cond
           calc_something
         else
           calc_something_else
         end

# good (and a bit more width efficient)
kind =
  case year
  when 1850..1889 then 'Blues'
  when 1890..1909 then 'Ragtime'
  when 1910..1929 then 'New Orleans Jazz'
  when 1930..1939 then 'Swing'
  when 1940..1950 then 'Bebop'
  else 'Jazz'
  end

result =
  if some_cond
    calc_something
  else
    calc_something_else
  end
```
- Use empty lines between method definitions and also to break up methods into logical paragraphs internally.

```
def some_method
  data = initialize(options)

  data.manipulate!

  data.result
end

def some_method
  result
end
```
- Don't use several empty lines in a row.

```
# bad - It has two empty lines.
some_method


some_method

# good
some_method

some_method
```
- Use empty lines around access modifiers.

```
# bad
class Foo
  attr_reader :foo
  def foo
    # do something...
  end
end

# good
class Foo
  attr_reader :foo

  def foo
    # do something...
  end
end
```
- Use spaces around the `=` operator when assigning default values to method parameters:

```
# bad
def some_method(arg1=:default, arg2=nil, arg3=[])
  # do something...
end

# good
def some_method(arg1 = :default, arg2 = nil, arg3 = [])
  # do something...
end
```
While several Ruby books suggest the first style, the second is much more prominent in practice (and arguably a bit more readable).
- Avoid line continuation `\` where not required. In practice, avoid using line continuations for anything but string concatenation.

```
# bad
result = 1 - \
         2

# good (but still ugly as hell)
result = 1 \
         - 2

long_string = 'First part of the long string' \
              ' and second part of the long string'
```
- Align the parameters of a method call if they span more than one line. When aligning parameters is not appropriate due to line-length constraints, single indent for the lines after the first is also acceptable.

```
# starting point (line is too long)
def send_mail(source)
  Mailer.deliver(to: 'bob@example.com', from: 'us@example.com', subject: 'Important message', body: source.text)
end

# bad (double indent)
def send_mail(source)
  Mailer.deliver(
      to: 'bob@example.com',
      from: 'us@example.com',
      subject: 'Important message',
      body: source.text)
end

# good
def send_mail(source)
  Mailer.deliver(to: 'bob@example.com',
                 from: 'us@example.com',
                 subject: 'Important message',
                 body: source.text)
end

# good (normal indent)
def send_mail(source)
  Mailer.deliver(
    to: 'bob@example.com',
    from: 'us@example.com',
    subject: 'Important message',
    body: source.text
  )
end
```
- Align the elements of array literals spanning multiple lines.

```
# bad - single indent
menu_item = ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
  'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']

# good
menu_item = [
  'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
  'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam'
]

# good
menu_item =
  ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
   'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']
```
- Add underscores to large numeric literals to improve their readability.

```
# bad - how many 0s are there?
num = 1000000

# good - much easier to parse for the human brain
num = 1_000_000
```
- Prefer smallcase letters for numeric literal prefixes. `0o` for octal, `0x` for hexadecimal and `0b` for binary. Do not use `0d` prefix for decimal literals.

```
# bad
num = 01234
num = 0O1234
num = 0X12AB
num = 0B10101
num = 0D1234
num = 0d1234

# good - easier to separate digits from the prefix
num = 0o1234
num = 0x12AB
num = 0b10101
num = 1234
```

- Use `Rdoc` and its conventions for API documentation. Don't put an empty line between the comment block and the `def`.

- Limit lines to 80 characters.
- Avoid trailing whitespace.
- End each file with a newline.
- Don't use block comments. They cannot be preceded by whitespace and are not as easy to spot as regular comments.

```
# bad
=begin
comment line
another comment line
=end

# good
# comment line
# another comment line
```

### Syntax

- Use `def` with parentheses when there are parameters. Omit the parentheses when the method doesn't accept any parameters.

```
# bad
def some_method()
  # body omitted
end

# good
def some_method
  # body omitted
end

# bad
def some_method_with_parameters param1, param2
  # body omitted
end

# good
def some_method_with_parameters(param1, param2)
  # body omitted
end
```
- Use parentheses around the arguments of method invocations, especially if the first argument begins with an open parenthesis `(`, as in `f((3 + 2) + 1)`.

```
# bad
x = Math.sin y
# good
x = Math.sin(y)

# bad
array.delete e
# good
array.delete(e)

# bad
temperance = Person.new 'Temperance', 30
# good
temperance = Person.new('Temperance', 30)
```

- Always omit parentheses for
  - Method calls with no arguments:

    ```
    # bad
    Kernel.exit!()
    2.even?()
    fork()
    'test'.upcase()

    # good
    Kernel.exit!
    2.even?
    fork
    'test'.upcase
    ```
  - Methods that are part of an internal DSL (e.g., Rake, Rails, RSpec):

    ```
    # bad
    validates(:name, presence: true)
    # good
    validates :name, presence: true
    ```
  - Methods that have "keyword" status in Ruby:

    ```
    class Person
      # bad
      attr_reader(:name, :age)
      # good
      attr_reader :name, :age

      # body omitted
    end
    ```
- Define optional arguments at the end of the list of arguments. Ruby has some unexpected results when calling methods that have optional arguments at the front of the list.

```
# bad
def some_method(a = 1, b = 2, c, d)
  puts "#{a}, #{b}, #{c}, #{d}"
end

some_method('w', 'x') # => '1, 2, w, x'
some_method('w', 'x', 'y') # => 'w, 2, x, y'
some_method('w', 'x', 'y', 'z') # => 'w, x, y, z'

# good
def some_method(c, d, a = 1, b = 2)
  puts "#{a}, #{b}, #{c}, #{d}"
end

some_method('w', 'x') # => '1, 2, w, x'
some_method('w', 'x', 'y') # => 'y, 2, w, x'
some_method('w', 'x', 'y', 'z') # => 'y, z, w, x'
```

- Avoid the use of parallel assignment for defining variables. Parallel assignment is allowed when it is the return of a method call, used with the splat operator, or when used to swap variable assignment. Parallel assignment is less readable than separate assignment.

```
# bad
a, b, c, d = 'foo', 'bar', 'baz', 'foobar'

# good
a = 'foo'
b = 'bar'
c = 'baz'
d = 'foobar'

# good - swapping variable assignment
# Swapping variable assignment is a special case because it will allow you to
# swap the values that are assigned to each variable.
a = 'foo'
b = 'bar'

a, b = b, a
puts a # => 'bar'
puts b # => 'foo'

# good - method return
def multi_return
  [1, 2]
end

first, second = multi_return

# good - use with splat
first, *list = [1, 2, 3, 4] # first => 1, list => [2, 3, 4]

hello_array = *'Hello' # => ["Hello"]

a = *(1..3) # => [1, 2, 3]
```

-Avoid the use of unnecessary trailing underscore variables during parallel assignment. Named underscore variables are to be preferred over underscore variables because of the context that they provide. Trailing underscore variables are necessary when there is a splat variable defined on the left side of the assignment, and the splat variable is not an underscore.

```
# bad
foo = 'one,two,three,four,five'
# Unnecessary assignment that does not provide useful information
first, second, _ = foo.split(',')
first, _, _ = foo.split(',')
first, *_ = foo.split(',')


# good
foo = 'one,two,three,four,five'
# The underscores are needed to show that you want all elements
# except for the last number of underscore elements
*beginning, _ = foo.split(',')
*beginning, something, _ = foo.split(',')

a, = foo.split(',')
a, b, = foo.split(',')
# Unnecessary assignment to an unused variable, but the assignment
# provides us with useful information.
first, _second = foo.split(',')
first, _second, = foo.split(',')
first, *_ending = foo.split(',')
```
- Do not use `for`, unless you know exactly why. Most of the time iterators should be used instead. `for` is implemented in terms of `each` (so you're adding a level of indirection), but with a twist—`for` doesn't introduce a new scope (unlike `each`) and variables defined in its block will be visible outside it.

```
arr = [1, 2, 3]

# bad
for elem in arr do
  puts elem
end

# note that elem is accessible outside of the for loop
elem # => 3

# good
arr.each { |elem| puts elem }

# elem is not accessible outside each's block
elem # => NameError: undefined local variable or method `elem`
```
- Favor the ternary operator(`?:`) over `if/then/else/end` constructs. It's more common and obviously more concise.

```
# bad
result = if some_condition then something else something_else end

# good
result = some_condition ? something : something_else
```
- Use one expression per branch in a ternary operator. This also means that ternary operators must not be nested. Prefer `if/else` constructs in these cases.

```
# bad
some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

# good
if some_condition
  nested_condition ? nested_something : nested_something_else
else
  something_else
end
```
- Leverage the fact that `if` and `case` are expressions which return a result.

```
# bad
if condition
  result = x
else
  result = y
end

# good
result =
  if condition
    x
  else
    y
  end
```
- Use `when x then ...` for one-line cases. The alternative syntax `when x: ...` has been removed as of Ruby 1.9.
- Do not use `when x; ....` See the previous rule.
- Use `!` instead of `not`.

```
# bad - parentheses are required because of op precedence
x = (not something)

# good
x = !something
```
- Avoid the use of `!!`. `!!` converts a value to boolean, but you don't need this explicit conversion in the condition of a control expression; using it only obscures your intention. If you want to do a `nil` check, use `nil?` instead.

```
# bad
x = 'test'
# obscure nil check
if !!x
  # body omitted
end

# good
x = 'test'
if x
  # body omitted
end
```
- The `and` and `or` keywords are banned. The minimal added readability is just not worth the high probability of introducing subtle bugs. For boolean expressions, always use `&&` and `||` instead. For flow control, use `if` and `unless`; `&&` and `||` are also acceptable but less clear.

```
# bad
# boolean expression
ok = got_needed_arguments and arguments_are_valid

# control flow
document.save or fail(RuntimeError, "Failed to save document!")

# good
# boolean expression
ok = got_needed_arguments && arguments_are_valid

# control flow
fail(RuntimeError, "Failed to save document!") unless document.save

# ok
# control flow
document.save || fail(RuntimeError, "Failed to save document!")
```
- Favor modifier `if/unless` usage when you have a single-line body. Another good alternative is the usage of control flow `&&/||`.

```
# bad
if some_condition
  do_something
end

# good
do_something if some_condition

# another good option
some_condition && do_something
```
- Do not use `unless` with `else`. Rewrite these with the positive case first.

```
# bad
unless success?
  puts 'failure'
else
  puts 'success'
end

# good
if success?
  puts 'success'
else
  puts 'failure'
end
```
-Omit the outer braces around an implicit options hash.

```
# bad
user.set({ name: 'John', age: 45, permissions: { read: true } })

# good
user.set(name: 'John', age: 45, permissions: { read: true })
```
- Omit the outer braces around an implicit options hash.

```
class Person < ActiveRecord::Base
  # bad
  validates(:name, { presence: true, length: { within: 1..10 } })

  # good
  validates :name, presence: true, length: { within: 1..10 }
end
```
- Use the proc invocation shorthand when the invoked method is the only operation of a block.

```
# bad
names.map { |name| name.upcase }

# good
names.map(&:upcase)
```
- Don't use the return value of `=` (an assignment) in conditional expressions unless the assignment is wrapped in parentheses. This is a fairly popular idiom among Rubyists that's sometimes referred to as safe assignment in condition.

```
# bad (+ a warning)
if v = array.grep(/foo/)
  do_something(v)
  # some code
end

# good (MRI would still complain, but RuboCop won't)
if (v = array.grep(/foo/))
  do_something(v)
  # some code
end

# good
v = array.grep(/foo/)
if v
  do_something(v)
  # some code
end
```
- Use shorthand self assignment operators whenever applicable.

```
# bad
x = x**y
x = x / y
x = x || y
x = x && y

# good
x **= y
x /= y
x ||= y
x &&= y
```
- Use `||=` to initialize variables only if they're not already initialized.

```
# bad
name = name ? name : 'Bozhidar'

# bad
name = 'Bozhidar' unless name

# good - set name to 'Bozhidar', only if it's nil or false
name ||= 'Bozhidar'
```
- Don't use `||=` to initialize boolean variables. (Consider what would happen if the current value happened to be `false`.

```
# bad - would set enabled to true even if it was false
enabled ||= true

# good
enabled = true if enabled.nil?
```
- Use `&&=` to preprocess variables that may or may not exist. Using `&&=` will change the value only if it exists, removing the need to check its existence with `if`.

```
# bad
if something
  something = something.downcase
end

# bad
something = something ? something.downcase : nil

# ok
something = something.downcase if something

# good
something = something && something.downcase

# better
something &&= something.downcase
```
- Avoid explicit use of the case equality operator `===`. As its name implies it is meant to be used implicitly by `case` expressions and outside of them it yields some pretty confusing code.

```
# bad
Array === something
(1..100) === 7
/something/ === some_string

# good
something.is_a?(Array)
(1..100).include?(7)
some_string =~ /something/
```
- Do not use `eql?` when using `==` will do. The stricter comparison semantics provided by `eql?` are rarely needed in practice.

```
# bad - eql? is the same as == for strings
'ruby'.eql? some_str

# good
'ruby' == some_str
1.0.eql? x # eql? makes sense here if want to differentiate between Integer and Float 1
```
- Do not put a space between a method name and the opening parenthesis.

```
# bad
f (3 + 2) + 1

# good
f(3 + 2) + 1
```
- Always run the Ruby interpreter with the `-w` option so it will warn you if you forget either of the rules above!

- Do not use nested method definitions, use lambda instead. Nested method definitions actually produce methods in the same scope (e.g. class) as the outer method. Furthermore, the "nested method" will be redefined every time the method containing its definition is invoked.

```
# bad
def foo(x)
  def bar(y)
    # body omitted
  end

  bar(x)
end

# good - the same as the previous, but no bar redefinition on every foo call
def bar(y)
  # body omitted
end

def foo(x)
  bar(x)
end

# also good
def foo(x)
  bar = ->(y) { ... }
  bar.call(x)
end
```
- Use the new lambda literal syntax for single line body blocks. Use the `lambda` method for multi-line blocks.

```
# bad
l = lambda { |a, b| a + b }
l.call(1, 2)

# correct, but looks extremely awkward
l = ->(a, b) do
  tmp = a * 7
  tmp * b / 50
end

# good
l = ->(a, b) { a + b }
l.call(1, 2)

l = lambda do |a, b|
  tmp = a * 7
  tmp * b / 50
end
```
-Don't omit the parameter parentheses when defining a stabby lambda with parameters.

```
# bad
l = ->x, y { something(x, y) }

# bad
l = ->() { something }

# good
l = ->(x, y) { something(x, y) }

# good
l = -> { something }
```

- Prefer `proc` over `Proc.new`.

```
# bad
p = Proc.new { |n| puts n }

# good
p = proc { |n| puts n }
```
- Prefer `proc.call()` over `proc[]` or `proc.()` for both lambdas and procs.

```
# bad - looks similar to Enumeration access
l = ->(v) { puts v }
l[1]

# also bad - uncommon syntax
l = ->(v) { puts v }
l.(1)

# good
l = ->(v) { puts v }
l.call(1)
```
- Use `Array()` instead of explicit `Array` check or `[*var]`, when dealing with a variable you want to treat as an Array, but you're not certain it's an array.

```
# bad
paths = [paths] unless paths.is_a? Array
paths.each { |path| do_something(path) }

# bad (always creates a new Array instance)
[*paths].each { |path| do_something(path) }

# good (and a bit more readable)
Array(paths).each { |path| do_something(path) }
```
- Use ranges or `Comparable#between?` instead of complex comparison logic when possible.

```
# bad
do_something if x >= 1000 && x <= 2000

# good
do_something if (1000..2000).include?(x)

# good
do_something if x.between?(1000, 2000)
```
- Favor the use of predicate methods to explicit comparisons with `==`. Numeric comparisons are OK.

```
# bad
if x % 2 == 0
end

if x % 2 == 1
end

if x == nil
end

# good
if x.even?
end

if x.odd?
end

if x.nil?
end

if x.zero?
end

if x == 0
end
```
- Don't do explicit non-`nil` checks unless you're dealing with boolean values.

```
# bad
do_something if !something.nil?
do_something if something != nil

# good
do_something if something

# good - dealing with a boolean
def value_set?
  !@some_boolean.nil?
end
```
- Prefer `next` in loops instead of conditional blocks.

```
# bad
[0, 1, 2, 3].each do |item|
  if item > 1
    puts item
  end
end

# good
[0, 1, 2, 3].each do |item|
  next unless item > 1
  puts item
end
```
- Prefer `map` over `collect`, `find` over `detect`, `select` over `find_all`, `reduce` over `inject` and `size` over `length`. This is not a hard requirement; if the use of the alias enhances readability, it's ok to use it. The rhyming methods are inherited from Smalltalk and are not common in other programming languages. The reason the use of `select` is encouraged over `find_all` is that it goes together nicely with `reject` and its name is pretty self-explanatory.
- Don't use `count` as a substitute for `size`. For `Enumerable` objects other than `Array` it will iterate the entire collection in order to determine its size.

```
# bad
some_hash.count

# good
some_hash.size
```
- Use `flat_map` instead of `map` + `flatten`. This does not apply for arrays with a depth greater than 2, i.e. if `users.first.songs == ['a', ['b','c']]`, then use `map` + `flatten` rather than `flat_map`. `flat_map` flattens the array by 1, whereas `flatten` flattens it all the way.

```
# bad
all_songs = users.map(&:songs).flatten.uniq

# good
all_songs = users.flat_map(&:songs).uniq
```
- Prefer `reverse_each` to `reverse.each` because some classes that `include Enumerable` will provide an efficient implementation. Even in the worst case where a class does not provide a specialized implementation, the general implementation inherited from `Enumerable` will be at least as efficient as using `reverse.each`.

```
# bad
array.reverse.each { ... }

# good
array.reverse_each { ... }
```

### Naming

- Use `snake_case` for symbols, methods and variables. Do not separate numbers from letters on symbols, methods and variables.

```
# bad
:'some symbol'
:SomeSymbol
:someSymbol

someVar = 5
var_10  = 10

def someMethod
  # some code
end

def SomeMethod
  # some code
end

# good
:some_symbol

some_var = 5
var10    = 10

def some_method
  # some code
end
```
- Use `CamelCase` for classes and modules. (Keep acronyms like HTTP, RFC, XML uppercase.)

```
# bad
class Someclass
  # some code
end

class Some_Class
  # some code
end

class SomeXml
  # some code
end

class XmlSomething
  # some code
end

# good
class SomeClass
  # some code
end

class SomeXML
  # some code
end

class XMLSomething
  # some code
end
```
- Use `snake_case` for naming files, e.g. `hello_world.rb`; and for naming directories, e.g. lib/hello_world/hello_world.rb
- Aim to have just a single class/module per source file. Name the file name as the class/module, but replacing CamelCase with snake_case.
- Use `SCREAMING_SNAKE_CASE` for other constants.

```
# bad
SomeConst = 5

# good
SOME_CONST = 5
```
- The names of predicate methods (methods that return a boolean value) should end in a question mark. (i.e. `Array#empty?`). Methods that don't return a boolean, shouldn't end in a question mark.
- Avoid prefixing predicate methods with the auxiliary verbs such as `is`, `does`, or `can`. These words are redundant and inconsistent with the style of boolean methods in the Ruby core library, such as `empty?` and `include?`.

```
# bad
class Person
  def is_tall?
    true
  end

  def can_play_basketball?
    false
  end

  def does_like_candy?
    true
  end
end

# good
class Person
  def tall?
    true
  end

  def basketball_player?
    false
  end

  def likes_candy?
    true
  end
end
```
- The names of potentially *dangerous* methods (i.e. methods that modify `self` or the arguments, `exit!` (doesn't run the finalizers like `exit` does), etc.) should end with an exclamation mark if there exists a safe version of that *dangerous* method.

```
# bad - there is no matching 'safe' method
class Person
  def update!
  end
end

# good
class Person
  def update
  end
end

# good
class Person
  def update!
  end

  def update
  end
end
```
- Define the non-bang (safe) method in terms of the bang (dangerous) one if possible.

```
class Array
  def flatten_once!
    res = []

    each do |e|
      [*e].each { |f| res << f }
    end

    replace(res)
  end

  def flatten_once
    dup.flatten_once!
  end
end
```

- When defining binary operators, name the parameter `other`(`<<` and `[]` are exceptions to the rule, since their semantics are different).

```
def +(other)
  # body omitted
end
```

### Comments

- Write self-documenting code and ignore the rest of this section. Seriously!

- Use `TODO` to note missing features or functionality that should be added at a later date.
- Use `FIXME` to note broken code that needs to be fixed.
- Use `OPTIMIZE` to note slow or inefficient code that may cause performance problems.
- Use `HACK` to note code smells where questionable coding practices were used and should be refactored away.
- Use `REVIEW` to note anything that should be looked at to confirm it is working as intended. For example: `REVIEW: Are we sure this is how the client does X currently?`
- Use other custom annotation keywords if it feels appropriate, but be sure to document them in your project's `README` or similar.

### Classes & Modules

- Use a consistent structure in your class definitions.

```
class Person
  # extend and include go first
  extend SomeModule
  include AnotherModule

  # inner classes
  CustomError = Class.new(StandardError)

  # constants are next
  SOME_CONSTANT = 20

  # afterwards we have attribute macros
  attr_reader :name

  # followed by other macros (if any)
  validates :name

  # public class methods are next in line
  def self.some_method
  end

  # initialization goes between class methods and other instance methods
  def initialize
  end

  # followed by other public instance methods
  def some_method
  end

  # protected and private methods are grouped near the end
  protected

  def some_protected_method
  end

  private

  def some_private_method
  end
end
```

- Split multiple mixins into separate statements.

```
# bad
class Person
  include Foo, Bar
end

# good
class Person
  # multiple mixins go in separate statements
  include Foo
  include Bar
end
```

- Don't nest multi-line classes within classes. Try to have such nested classes each in their own file in a folder named like the containing class.

```
# bad

# foo.rb
class Foo
  class Bar
    # 30 methods inside
  end

  class Car
    # 20 methods inside
  end

  # 30 methods inside
end

# good

# foo.rb
class Foo
  # 30 methods inside
end

# foo/bar.rb
class Foo
  class Bar
    # 30 methods inside
  end
end

# foo/car.rb
class Foo
  class Car
    # 20 methods inside
  end
end
```
- Prefer modules to classes with only class methods. Classes should be used only when it makes sense to create instances out of them.

```
# bad
class SomeClass
  def self.some_method
    # body omitted
  end

  def self.some_other_method
    # body omitted
  end
end

# good
module SomeModule
  module_function

  def some_method
    # body omitted
  end

  def some_other_method
    # body omitted
  end
end
```

- Favor the use of `module_function` over `extend self` when you want to turn a module's instance methods into class methods.

```
# bad
module Utilities
  extend self

  def parse_something(string)
    # do stuff here
  end

  def other_utility_method(number, string)
    # do some more stuff
  end
end

# good
module Utilities
  module_function

  def parse_something(string)
    # do stuff here
  end

  def other_utility_method(number, string)
    # do some more stuff
  end
end
```

- Use the attr family of functions to define trivial accessors or mutators.

```
# bad
class Person
  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end

  def first_name
    @first_name
  end

  def last_name
    @last_name
  end
end

# good
class Person
  attr_reader :first_name, :last_name

  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end
end
```

- [`Struct` Styling](https://github.com/bbatsov/ruby-style-guide#classes--modules)

- Prefer duck-typing over inheritance.

```
# bad
class Animal
  # abstract method
  def speak
  end
end

# extend superclass
class Duck < Animal
  def speak
    puts 'Quack! Quack'
  end
end

# extend superclass
class Dog < Animal
  def speak
    puts 'Bau! Bau!'
  end
end

# good
class Duck
  def speak
    puts 'Quack! Quack'
  end
end

class Dog
  def speak
    puts 'Bau! Bau!'
  end
end
```
- Avoid the usage of class (`@@`) variables due to their "nasty" behavior in inheritance.

```
class Parent
  @@class_var = 'parent'

  def self.print_class_var
    puts @@class_var
  end
end

class Child < Parent
  @@class_var = 'child'
end

Parent.print_class_var # => will print 'child'
```
As you can see all the classes in a class hierarchy actually share one class variable. Class instance variables should usually be preferred over class variables.

- Indent the `public`, `protected`, and `private` methods as much as the method definitions they apply to. Leave one blank line above the visibility modifier and one blank line below in order to emphasize that it applies to all methods below it.

```
class SomeClass
  def public_method
    # some code
  end

  private

  def private_method
    # some code
  end

  def another_private_method
    # some code
  end
end
```

- [`Alias` Method](https://github.com/bbatsov/ruby-style-guide#classes--modules)

### Exceptions

- Prefer `raise` over `fail` for exceptions.

```
# bad
fail SomeException, 'message'

# good
raise SomeException, 'message'
```
- Don't specify `RuntimeError` explicitly in the two argument version of `raise`.

```
# bad
raise RuntimeError, 'message'

# good - signals a RuntimeError by default
raise 'message'
```
- Prefer supplying an exception class and a message as two separate arguments to raise, instead of an exception instance.

```
# bad
raise SomeException.new('message')
# Note that there is no way to do `raise SomeException.new('message'), backtrace`.

# good
raise SomeException, 'message'
# Consistent with `raise SomeException, 'message', backtrace`.
```
- Do not return from an `ensure` block. If you explicitly return from a method inside an `ensure` block, the return will take precedence over any exception being raised, and the method will return as if no exception had been raised at all. In effect, the exception will be silently thrown away.

```
# bad
def foo
  raise
ensure
  return 'very bad idea'
end
```
- Use *implicit begin blocks* where possible.

```
# bad
def foo
  begin
    # main logic goes here
  rescue
    # failure handling goes here
  end
end

# good
def foo
  # main logic goes here
rescue
  # failure handling goes here
end
```
- Mitigate the proliferation of `begin` blocks by using *contingency methods* (a term coined by Avdi Grimm).

```
# bad
begin
  something_that_might_fail
rescue IOError
  # handle IOError
end

begin
  something_else_that_might_fail
rescue IOError
  # handle IOError
end

# good
def with_io_error_handling
   yield
rescue IOError
  # handle IOError
end

with_io_error_handling { something_that_might_fail }

with_io_error_handling { something_else_that_might_fail }
```

- Don't suppress exceptions.

```
# bad
begin
  # an exception occurs here
rescue SomeError
  # the rescue clause does absolutely nothing
end

# bad
do_something rescue nil
```
- Avoid using `rescue` in its modifier form.

```
# bad - this catches exceptions of StandardError class and its descendant classes
read_file rescue handle_error($!)

# good - this catches only the exceptions of Errno::ENOENT class and its descendant classes
def foo
  read_file
rescue Errno::ENOENT => ex
  handle_error(ex)
end
```
- Don't use exceptions for flow of control.

```
# bad
begin
  n / d
rescue ZeroDivisionError
  puts 'Cannot divide by 0!'
end

# good
if d.zero?
  puts 'Cannot divide by 0!'
else
  n / d
end
```
- Avoid rescuing the `Exception` class. This will trap signals and calls to `exit`, requiring you to `kill -9` the process.

```
`# bad
begin
  # calls to exit and kill signals will be caught (except kill -9)
  exit
rescue Exception
  puts "you didn't really want to exit, right?"
  # exception handling
end

# good
begin
  # a blind rescue rescues from StandardError, not Exception as many
  # programmers assume.
rescue => e
  # exception handling
end

# also good
begin
  # an exception occurs here
rescue StandardError => e
  # exception handling
end
```
- Put more specific exceptions higher up the rescue chain, otherwise they'll never be rescued from.

```
# bad
begin
  # some code
rescue StandardError => e
  # some handling
rescue IOError => e
  # some handling that will never be executed
end

# good
begin
  # some code
rescue IOError => e
  # some handling
rescue StandardError => e
  # some handling
end
```
- Release external resources obtained by your program in an `ensure` block.

```
f = File.open('testfile')
begin
  # .. process
rescue
  # .. handle error
ensure
  f.close if f
end
```
- Use versions of resource obtaining methods that do automatic resource cleanup when possible.

```
# bad - you need to close the file descriptor explicitly
f = File.open('testfile')
# some action on the file
f.close

# good - the file descriptor is closed automatically
File.open('testfile') do |f|
  # some action on the file
end
```
- Favor the use of exceptions from the standard library over introducing new exception classes.

### Collections

- Prefer literal array and hash creation notation (unless you need to pass parameters to their constructors, that is).

```
# bad
arr = Array.new
hash = Hash.new

# good
arr = []
arr = Array.new(10)
hash = {}
hash = Hash.new(0)
```
- Prefer `%w` to the literal array syntax when you need an array of words (non-empty strings without spaces and special characters in them). Apply this rule only to arrays with two or more elements.

```
# bad
STATES = ['draft', 'open', 'closed']

# good
STATES = %w[draft open closed]
```
- Prefer `%i` to the literal array syntax when you need an array of symbols (and you don't need to maintain Ruby 1.9 compatibility). Apply this rule only to arrays with two or more elements.

```
# bad
STATES = [:draft, :open, :closed]

# good
STATES = %i[draft open closed]
```
- When accessing the `first` or `last` element from an array, prefer first or last over `[0]` or `[-1]`.
- Use `Set` instead of `Array` when dealing with unique elements. `Set` implements a collection of unordered values with no duplicates. This is a hybrid of `Array`'s intuitive inter-operation facilities and `Hash`'s fast lookup.
- Prefer symbols instead of strings as hash keys.

```
# bad
hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

# good
hash = { one: 1, two: 2, three: 3 }
```
- Avoid the use of mutable objects as hash keys.
- Use the Ruby 1.9 hash literal syntax when your hash keys are symbols.

```
# bad
hash = { :one => 1, :two => 2, :three => 3 }

# good
hash = { one: 1, two: 2, three: 3 }
```
- Don't mix the Ruby 1.9 hash syntax with hash rockets in the same hash literal. When you've got keys that are not symbols stick to the hash rockets syntax.

```
# bad
{ a: 1, 'b' => 2 }

# good
{ :a => 1, 'b' => 2 }
```
- Use `Hash#key?` instead of `Hash#has_key?` and `Hash#value?` instead of `Hash#has_value?`.

```
# bad
hash.has_key?(:test)
hash.has_value?(value)

# good
hash.key?(:test)
hash.value?(value)
```
- Use `Hash#each_key` instead of `Hash#keys.each` and `Hash#each_value` instead of `Hash#values.each`.

```
# bad
hash.keys.each { |k| p k }
hash.values.each { |v| p v }
hash.each { |k, _v| p k }
hash.each { |_k, v| p v }

# good
hash.each_key { |k| p k }
hash.each_value { |v| p v }
```
- Use `Hash#fetch` when dealing with hash keys that should be present.

```
heroes = { batman: 'Bruce Wayne', superman: 'Clark Kent' }
# bad - if we make a mistake we might not spot it right away
heroes[:batman] # => 'Bruce Wayne'
heroes[:supermann] # => nil

# good - fetch raises a KeyError making the problem obvious
heroes.fetch(:supermann)
```
- Introduce default values for hash keys via `Hash#fetch` as opposed to using custom logic.

```
batman = { name: 'Bruce Wayne', is_evil: false }

# bad - if we just use || operator with falsy value we won't get the expected result
batman[:is_evil] || true # => true

# good - fetch work correctly with falsy values
batman.fetch(:is_evil, true) # => false
```
- Prefer the use of the block instead of the default value in `Hash#fetch` if the code that has to be evaluated may have side effects or be expensive

```
batman = { name: 'Bruce Wayne' }

# bad - if we use the default value, we eager evaluate it
# so it can slow the program down if done multiple times
batman.fetch(:powers, obtain_batman_powers) # obtain_batman_powers is an expensive call

# good - blocks are lazy evaluated, so only triggered in case of KeyError exception
batman.fetch(:powers) { obtain_batman_powers }
```
- Use `Hash#values_at` when you need to retrieve several values consecutively from a hash.

```
# bad
email = data['email']
username = data['nickname']

# good
email, username = data.values_at('email', 'nickname')
```
- Rely on the fact that as of Ruby 1.9 hashes are ordered.
- Do not modify a collection while traversing it.
- When accessing elements of a collection, avoid direct access via `[n]` by using an alternate form of the reader method if it is supplied. This guards you from calling `[]` on `nil`.

```
# bad
Regexp.last_match[1]

# good
Regexp.last_match(1)
```
- When providing an accessor for a collection, provide an alternate form to save users from checking for `nil` before accessing an element in the collection.

```
# bad
def awesome_things
  @awesome_things
end

# good
def awesome_things(index = nil)
  if index && @awesome_things
    @awesome_things[index]
  else
    @awesome_things
  end
end
```

### Numbers

- Use `Integer` check type of an integer number. Since `Fixnum` is platform-dependent, checking against it will return different results on 32-bit and 64-bit machines.

```
timestamp = Time.now.to_i

# bad
timestamp.is_a? Fixnum
timestamp.is_a? Bignum

# good
timestamp.is_a? Integer
```
  - Prefer to use ranges when generating random numbers instead of integers with offsets, since it clearly states your intentions. Imagine simulating a role of a dice:

  ```
  # bad
  rand(6) + 1

  # good
  rand(1..6)
  ```

### Strings

- Prefer string interpolation and string formatting instead of string concatenation:

```
# bad
email_with_name = user.name + ' <' + user.email + '>'

# good
email_with_name = "#{user.name} <#{user.email}>"

# good
email_with_name = format('%s <%s>', user.name, user.email)
```

- Adopt a consistent string literal quoting style. There are two popular styles in the Ruby community, both of which are considered good—single quotes by default (Option A) and double quotes by default (Option B).
  - **(Option A)** Prefer single-quoted strings when you don't need string interpolation or special symbols such as `\t`, `\n`, `'`, etc.

    ```
    # bad
    name = "Bozhidar"

    name = 'De\'Andre'

    # good
    name = 'Bozhidar'

    name = "De'Andre"
    ```
  - **(Option B)** Prefer double-quotes unless your string literal contains `"` or escape characters you want to suppress.

    ```
    # bad
    name = 'Bozhidar'

    sarcasm = "I \"like\" it."

    # good
    name = "Bozhidar"

    sarcasm = 'I "like" it.'
    ```
- Avoid using `String#+` when you need to construct large data chunks. Instead, use `String#<<`. Concatenation mutates the string instance in-place and is always faster than `String#+`, which creates a bunch of new string objects.

```
# bad
html = ''
html += '<h1>Page title</h1>'

paragraphs.each do |paragraph|
  html += "<p>#{paragraph}</p>"
end

# good and also fast
html = ''
html << '<h1>Page title</h1>'

paragraphs.each do |paragraph|
  html << "<p>#{paragraph}</p>"
end
```

- Don't use `String#gsub` in scenarios in which you can use a faster more specialized alternative.

```
url = 'http://example.com'
str = 'lisp-case-rules'

# bad
url.gsub('http://', 'https://')
str.gsub('-', '_')

# good
url.sub('http://', 'https://')
str.tr('-', '_')
```

> Please visit the [link of this guide](https://github.com/bbatsov/ruby-style-guide#strings) to have tips about `heredocs`.

### Date & Time

- Prefer `Time.now` over `Time.new` when retrieving the current system time.

- Don't use DateTime unless you need to account for historical calendar reform -- and if you do, explicitly specify the start argument to clearly state your intentions.

```
# bad - uses DateTime for current time
DateTime.now

# good - uses Time for current time
Time.now

# bad - uses DateTime for modern date
DateTime.iso8601('2016-06-29')

# good - uses Date for modern date
Date.iso8601('2016-06-29')

# good - uses DateTime with start argument for historical date
DateTime.iso8601('1751-04-23', Date::ENGLAND)
```

### Regular Expressions

- Don't use regular expressions if you just need plain text search in string: `string['text']`
- For complex replacements `sub/gsub` can be used with a block or a hash.

```
words = 'foo bar'
words.sub(/f/, 'f' => 'F') # => 'Foo bar'
words.gsub(/\w+/) { |word| word.capitalize } # => 'Foo Bar'
```

> Please visit [this link](https://github.com/bbatsov/ruby-style-guide/blob/master/README.md#percent-literals) for Percent Literals; [that link](https://github.com/bbatsov/ruby-style-guide/blob/master/README.md#metaprogramming) for Metaprogramming; and [this link](https://github.com/bbatsov/ruby-style-guide/blob/master/README.md#misc) for Misc.


---------------

### Why does explicit return make a difference in a Proc? from [stackoverflow](https://stackoverflow.com/questions/1435743/why-does-explicit-return-make-a-difference-in-a-proc)

Ruby has three constructs:

1. A *block* is not an object and is created by `{ ... }` or do `...` end.
2. A *proc* is a `Proc` object created by `Proc.new` or `proc`.
3. A *lambda* is a `Proc` created by `lambda` (or `proc` in Ruby 1.8).

Ruby has three keywords that return from something:

1. `return` terminates the method or lambda it is in.
2. `next` terminates the block, proc, or lambda it is in.
3. `break` terminates the method that yielded to the block or invoked the proc or lambda it is in.

In lambdas, `return` behaves like `next`, for whatever reason. `next` and `break` are named the way they are because they are most commonly used with methods like `each`, where terminating the block will cause the iteration to resume with the **next** element of the collection, and terminating `each` will cause you to **break** out of the loop.

If you use `return` inside the definition of `foo`, you will return from `foo`, even if it is inside a block or a proc. To return from a block, you can use the `next` keyword instead.

```
def foo
  f = Proc.new { next "return from foo from inside proc" }
  f.call # control leaves foo here
  return "return from foo"
end
puts foo # prints "return from foo"
```

- For more answers, please check the link above.

--------------

# From [Jumpstartlab](http://tutorials.jumpstartlab.com/projects/eventmanager.html)

## Ruby’s ERB

ERB defines several different escape sequence tags that we can use, the most common are:

```
<%= ruby code will execute and show output %>
<% ruby code will execute but not show output %>
```

We can define our ERB escape tags within any string. The ruby defined within the contents of the ERB tags will not be evaluated until we ask the template to give us the results.

```
require 'erb'

meaning_of_life = 42

question = "The Answer to the Ultimate Question of Life, the Universe, and Everything is <%= meaning_of_life %>"
template = ERB.new question

results = template.result(binding)
puts results
```

The code above loads the ERB library. Creates a new ERB template with the `question` string. The question string contains ERB tags that will show the results of the variable `meaning_of_life`. We send the `result` message to the template with `binding` and
  - What is `binding`?
  The method binding returns a special object. This object is an instance of Binding. An instance of binding knows all about the current state of variables and methods within the given scope. In this case, `binding` here knows about the variable `meaning_of_life`.

-------
#### Load vs Require

- The load method simply reads and parses another files into your code every time a script is executed. `load 'test_module.rb'`
- Require reads the file from the file system, parses it, saves to the memory and runs it in a given place. Simply, even if you change the required file when the script is running, those changes won't be applied - Ruby will use the file from memory, not from the file system.`require 'test_module'`

-  In most cases you’ll use `require`, but there are some cases when `load` is useful, for example, when your module changes frequently you may want to pick up those changes in classes that loads this module.

#### Include vs Extend

- When you `include` a module into your class it behaves as if you took the code defined in your `TestModule` and inserted it in your `TestClass`. For example, if we have many classes that would need same functionality we don’t have to write the same code in all of them. Instead, we can define the module and `include` it in any classes.

```
module TestModule
  def some_method
    "Some method of #{self.class}"
  end
end

class TestClass
  include TestModule
  # ...
end

test = TestClass.new.some_method
puts test
```

- Unlike `include`, which adds module’s methods as instance methods, `extend` allows you to add them as a class methods.

# From Michael Hartl's book, [Chp 4](https://www.railstutorial.org/book/rails_flavored_ruby)

### Single vs Double Quote

- Ruby won’t interpolate into single-quoted strings
- Single quotes are truly literal, containing exactly the characters you type. '\n' vs "\\n"


### CSS revisited

```
stylesheet_link_tag 'application', media: 'all',
                                   'data-turbolinks-track': 'reload'
```

- First, where are the parentheses? In Ruby, they are optional, so these two are equivalent:

  ```
  # Parentheses on function calls are optional.
  stylesheet_link_tag('application', media: 'all',
                                     'data-turbolinks-track': 'reload')
  stylesheet_link_tag 'application', media: 'all',
                                     'data-turbolinks-track': 'reload'
  ```

- Second, the `media` argument sure looks like a hash, but where are the curly braces? When hashes are the *last* argument in a function call, the curly braces are optional, so these two are equivalent:

  ```
  # Curly braces on final hash arguments are optional.
  stylesheet_link_tag 'application', { media: 'all',
                                       'data-turbolinks-track': 'reload' }
  stylesheet_link_tag 'application', media: 'all',
                                     'data-turbolinks-track': 'reload'
  ```

- Finally, why does Ruby correctly interpret the lines

  ```
  stylesheet_link_tag 'application', media: 'all',
                                     'data-turbolinks-track': 'reload'
  ```

  even with a line break between the final elements? The answer is that Ruby doesn’t distinguish between newlines and other whitespace in this context. The *reason* I chose to break the code into pieces is that I prefer to keep lines of source code under 80 characters for legibility.

So, we see now that the line

```
stylesheet_link_tag 'application', media: 'all',
                                   'data-turbolinks-track': 'reload'
```

calls the `stylesheet_link_tag` function with two arguments: a string, indicating the path to the stylesheet, and a hash with two elements, indicating the media type and telling Rails to use the [turbolinks](https://github.com/rails/turbolinks) feature added in Rails 4.0. Because of the `<%= %>` brackets, the results are inserted into the template by ERb, and if you view the source of the page in your browser you should see the HTML needed to include a stylesheet (see below). (You may see some extra things, like ?body=1, after the CSS filenames. These are inserted by Rails to ensure that browsers reload the CSS when it changes on the server.)

```
# The HTML source produced by the CSS includes.

<link data-turbolinks-track="true" href="/assets/application.css" media="all"
rel="stylesheet" />
```


























