## 1. Primitive Datatypes and Operators

Integer division rounds down for both positive and negative numbers.
```
5 // 3       # => 1
-5 // 3      # => -2
5.0 // 3.0   # => 1.0 # works on floats too
-5.0 // 3.0  # => -2.0
```

The result of division is always a float
```
10.0 / 3  # => 3.3333333333333335
```

Modulo operation
```
7 % 3   # => 1
# i % j have the same sign as j, unlike C
-7 % 3  # => 2
```

True and False are actually 1 and 0 but with different keywords
```
True + True # => 2
True * 8    # => 8
False - 5   # => -5
```

Comparison operators look at the numerical value of True and False
```
0 == False  # => True
2 > True    # => True
2 == True   # => False
-5 != False # => True
```

None, 0, and empty strings/lists/dicts/tuples/sets all evaluate to False.
All other values are True
```
bool(0)     # => False
bool("")    # => False
bool([])    # => False
bool({})    # => False
bool(())    # => False
bool(set()) # => False
bool(4)     # => True
bool(-6)    # => True
```

Using boolean logical operators on ints casts them to booleans for evaluation,but their non-cast value is returned. Don't mix up with bool(ints) and bitwise and/or (&,|)
```
bool(0)     # => False
bool(2)     # => True
0 and 2     # => 0
bool(-5)    # => True
bool(2)     # => True
-5 or 0     # => -5
```

(is vs. ==) is checks if two variables refer to the same object, but == checks if the objects pointed to have the same values.
```
a = [1, 2, 3, 4]  # Point a at a new list, [1, 2, 3, 4]
b = a             # Point b at what a is pointing to
b is a            # => True, a and b refer to the same object
b == a            # => True, a's and b's objects are equal
b = [1, 2, 3, 4]  # Point b at a new list, [1, 2, 3, 4]
b is a            # => False, a and b do not refer to the same object
b == a            # => True, a's and b's objects are equal
```

Strings can be added too
```
"Hello " + "world!"  # => "Hello world!"
```

String literals (but not variables) can be concatenated without using '+'
```
"Hello " "world!"    # => "Hello world!"
```

Don't use the equality "==" symbol to compare objects to None. Use "is" instead. This checks for equality of object identity.
```
"etc" is None  # => False
None is None   # => True
```

## 2. Variables and Collections

By default the print function also prints out a newline at the end. Use the optional argument end to change the end string.
```
print("Hello, World", end="!")  # => Hello, World!
```

Accessing a previously unassigned variable is an exception. See Control Flow to learn more about exception handling.
```
some_unknown_var  # Raises a NameError
```

if can be used as an expression. Equivalent of C's '?:' ternary operator
```
"yay!" if 0 > 1 else "nay!"  # => "nay!"
```

Looking out of bounds is an IndexError
```
li[4]  # Raises an IndexError
li[::2]   # Return list selecting every second entry => [1, 4]
li[::-1]  # Return list in reverse order => [3, 4, 2, 1]
```
Use any combination of these to make advanced slices
```
li[start:end:step]
```

Make a one layer deep copy using slices
```
li2 = li[:]  # => li2 = [1, 2, 4, 3] but (li2 is li) will result in false.
```

Remove arbitrary elements from a list with "del"
```
li = [1,2,3,4]
del li[2]  # li is now [1, 2, 3]
```

Remove first occurrence of a value
```
li.remove(2)  # li is now [1, 3]
li.remove(2)  # Raises a ValueError as 2 is not in the list
```

Insert an element at a specific index
```
li.insert(1, 2)  # li is now [1, 2, 3] again
```

Concatenate lists
```
li + other_li  # => [1, 2, 3, 4, 5, 6] # values for li and for other_li are not modified.
li.extend(other_li)  # Now li is [1, 2, 3, 4, 5, 6]
```

Note that a tuple of length one has to have a comma after the last element but tuples of other lengths, even zero, do not.
```
type((1))   # => <class 'int'>
type((1,))  # => <class 'tuple'>
type(())    # => <class 'tuple'>
```

You can unpack tuples (or lists) into variables
```
a, b, c = (1, 2, 3)  # a is now 1, b is now 2 and c is now 3
```
You can also do extended unpacking
```
a, *b, c = (1, 2, 3, 4)  # a is now 1, b is now [2, 3] and c is now 4
```
Tuples are created by default if you leave out the parentheses
```
d, e, f = 4, 5, 6  # tuple 4, 5, 6 is unpacked into variables d, e and f respectively such that d = 4, e = 5 and f = 6
e, d = d, e  # d is now 5 and e is now 4
```
keys for dictionaries have to be immutable types. This is to ensure that the key can be converted to a constant hash value for quick look-ups. Immutable types include ints, floats, strings, tuples.
```
invalid_dict = {[1,2,3]: "123"}  # => Yield a TypeError: unhashable type: 'list'
valid_dict = {(1,2,3):[1,2,3]}   # Values can be of any type, however.
```

Get all keys as an iterable with "keys()"
```
filled_dict = {"one": 1, "two": 2, "three": 3}
list(filled_dict.keys())  # => ["three", "two", "one"] in Python <3.7
list(filled_dict.keys())  # => ["one", "two", "three"] in Python 3.7+, dictionary items maintain the order at which they are inserted into the dictionary.
# Same applies to values()
```

Looking up a non-existing key is a KeyError
```
filled_dict["four"]  # KeyError
# Use "get()" method to avoid the KeyError
filled_dict.get("four")     # => None
filled_dict.get("four", 4)  # => 4
```

"setdefault()" inserts into a dictionary only if the given key isn't present
```
filled_dict.setdefault("five", 5)  # filled_dict["five"] is set to 5
filled_dict.setdefault("five", 6)  # filled_dict["five"] is still 5
```

From Python 3.5 you can also use the additional unpacking options
```
{'a': 1, **{'b': 2}}  # => {'a': 1, 'b': 2}
{'a': 1, **{'a': 2}}  # => {'a': 2}
```

Sets
```
some_set = {1, 1, 2, 2, 3, 4}  # some_set is now {1, 2, 3, 4}
```
Similar to keys of a dictionary, elements of a set have to be immutable.
```
invalid_set = {[1], 1}  # => Raises a TypeError: unhashable type: 'list'
valid_set = {(1,), 1}
```

Do set intersection with &
```
filled_set = {1, 2, 3, 4, 5}
other_set = {3, 4, 5, 6}
filled_set & other_set  # => {3, 4, 5}
```

Do set union with |
```
filled_set | other_set  # => {1, 2, 3, 4, 5, 6}
```

Do set difference with -
```
{1, 2, 3, 4} - {2, 3, 5}  # => {1, 4}
```

Do set symmetric difference with ^
```
{1, 2, 3, 4} ^ {2, 3, 5}  # => {1, 4, 5}
```

Check if set on the left is a superset of set on the right
```
{1, 2} >= {1, 2, 3} # => False
```

Check if set on the left is a subset of set on the right
```
{1, 2} <= {1, 2, 3} # => True
```

## 3. Control Flow and Iterables

`range(lower, upper, step)` returns an iterable of numbers. prints:
4
6
```
for i in range(4, 8, 2):
    print(i)
```

Loop over a list to retrieve both the index and the value of each list item:
    0 dog
    1 cat
    2 mouse
```
animals = ["dog", "cat", "mouse"]
for i, value in enumerate(animals):
    print(i, value)
```

Handle exceptions with a try/except block
```
try:
    # Use "raise" to raise an error
    raise IndexError("This is an index error")
except IndexError as e:
    pass                 # Refrain from this, provide a recovery (next example).
except (TypeError, NameError):
    pass                 # Multiple exceptions can be processed jointly.
else:                    # Optional clause to the try/except block. Must follow
                         # all except blocks.
    print("All good!")   # Runs only if the code in try raises no exceptions
finally:                 # Execute under all circumstances
    print("We can clean up resources here")
```

Instead of try/finally to cleanup resources you can use a with statement
```
with open("myfile.txt") as f:
    for line in f:
        print(line)
```

Python offers a fundamental abstraction called the Iterable.
An iterable is an object that can be treated as a sequence.
The object returned by the range function, is an iterable.
```
filled_dict = {"one": 1, "two": 2, "three": 3}
our_iterable = filled_dict.keys()
```
An iterable is an object that knows how to create an iterator.
```
our_iterator = iter(our_iterable)
```
Our iterator is an object that can remember the state as we traverse through it. We get the next object with "next()".
```
next(our_iterator)  # => "one"
```
It maintains state as we iterate.
```
next(our_iterator)  # => "two"
next(our_iterator)  # => "three"
```
After the iterator has returned all of its data, it raises a StopIteration exception
```
next(our_iterator)  # Raises StopIteration
```
We can also loop over it, in fact, "for" does this implicitly!
```
our_iterator = iter(our_iterable)
for i in our_iterator:
    print(i)  # Prints one, two, three
```
You can grab all the elements of an iterable or iterator by call of list().
```
list(our_iterable)  # => Returns ["one", "two", "three"]
list(our_iterator)  # => Returns [] because state is saved
```

## 4. Functions

```
(lambda x: x > 2)(3)                  # => True
(lambda x, y: x ** 2 + y ** 2)(2, 1)  # => 5
```

There are built-in higher order functions
```
list(map(add_10, [1, 2, 3]))          # => [11, 12, 13]
list(map(max, [1, 2, 3], [4, 2, 1]))  # => [4, 2, 3]
list(filter(lambda x: x > 5, [3, 4, 5, 6, 7]))  # => [6, 7]
```

List comprehension stores the output as a list (which itself may be nested)
```
[x for x in [3, 4, 5, 6, 7] if x > 5]  # => [6, 7]
```

You can construct set and dict comprehensions as well.
```
{x for x in 'abcddeef' if x not in 'abc'}  # => {'d', 'e', 'f'}
{x: x**2 for x in range(5)}  # => {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## 5. Modules

```
import math
```
If you have a Python script named math.py in the same folder as your current script, the file math.py will be loaded instead of the built-in Python module. This happens because the local folder has priority over Python's built-in libraries.

## 6. Classes

```
class Human
    species = "H.sapiens"

    @classmethod
    def get_species(cls):
        return cls.species

    @staticmethod
    def grunt():
        return "*grunt*"
```

Static methods can be called by instances too
```
h = Human()
print(Human.grunt())            # => "*grunt*"
print(h.grunt())            # => "*grunt*"
```

A property is just like a getter. It turns the method age() into a read-only attribute of the same name. There's no need to write trivial getters and setters in Python, though.
```
@property
def age(self):
    return self._age

# This allows the property to be set
@age.setter
def age(self, age):
    self._age = age

# This allows the property to be deleted
@age.deleter
def age(self):
    del self._age
```

This __name__ check makes sure this code block is only executed when this module is the main program.
```
if __name__ == '__main__':
```

## 6. Inheritance

```
class Superhero(Human):
    species = "Superhuman"

    def __init__(self, name, movie=False,
                 superpowers=["super strength", "bulletproofing"]):

        # add additional class attributes:
        self.fictional = True
        self.movie = movie
        # be aware of mutable default values, since defaults are shared
        self.superpowers = superpowers
        # This calls the parent class constructor:
        super().__init__(name)
```

isinstance vs type
```
h = Human()
sh = Superhero()

isinstance(sh, Human)       # => True
isinstance(sh, Superhero)   # => True
type(sh) is Human           # => False
type(sh) is Superhero       # => True

```

## 6.2 Multiple Inheritance

```
class Batman(Superhero, Bat):
    def __init__(self, *args, **kwargs):
        # super(Batman, self).__init__(*args, **kwargs)
        # However we are dealing with multiple inheritance here, and super()
        # only works with the next base class in the MRO list.
        # So instead we explicitly call __init__ for all ancestors.
        Superhero.__init__(self, 'anonymous', movie=True,
                           superpowers=['Wealthy'], *args, **kwargs)
        Bat.__init__(self, *args, can_fly=False, **kwargs)
        # override the value for the name attribute
        self.name = 'Sad Affleck'

if __name__ == '__main__':
    sup = Batman()

    # Get the Method Resolution search Order used by both getattr() and super().
    # This attribute is dynamic and can be updated
    print(Batman.__mro__)       # => (<class '__main__.Batman'>,
                                # => <class 'superhero.Superhero'>,
                                # => <class 'human.Human'>,
                                # => <class 'bat.Bat'>, <class 'object'>)

```

## 7. Advanced

#### Generators

Generators are memory-efficient because they only load the data needed to process the next value in the iterable. This allows them to perform operations on otherwise prohibitively large value ranges.
NOTE: `range` replaces `xrange` in Python 3.

```
for i in double_numbers(range(1, 900000000)):  # `range` is a generator.
    print(i)
    if i >= 30:
        break
```

Just as you can create a list comprehension, you can create generator comprehensions as well.
```
values = (-x for x in [1,2,3,4,5])
for x in values:
    print(x)  # prints -1 -2 -3 -4 -5 to console/terminal
list(values) # => [-1, -2, -3, -4, -5]
```

#### Decorators

```
from functools import wraps


def beg(target_function):
    @wraps(target_function)
    def wrapper(*args, **kwargs):
        msg, say_please = target_function(*args, **kwargs)
        if say_please:
            return "{} {}".format(msg, "Please! I am poor :(")
        return msg

    return wrapper


@beg
def say(say_please=False):
    msg = "Can you buy me a beer?"
    return msg, say_please


print(say())                 # Can you buy me a beer?
print(say(say_please=True))  # Can you buy me a beer? Please! I am poor :(
```
