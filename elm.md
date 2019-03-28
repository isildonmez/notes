> From [elm documentation](https://guide.elm-lang.org/)

- `elm repl`
- `elm reactor` : This starts a server at http://localhost:8000
- `elm make Main.elm --output=main.html` : Say you want to compile `Main.elm` to an HTML file named `main.html`. You would run this command.
- `elm install elm/http` : This will add the dependencies into your `elm.json` file
- `elm --help` or `elm repl --help`
- `elm-package install evancz/elm-html` : Install a package

## Core Language

### Values

```
> "hello" ++ " world"
"hello world"

> 2 + 3 * 4
14

> (2 + 3) * 4
20

> 9 / 2
4.5

> 9 // 2
4
```

### Functions

```
> isNegative n = n < 0
<function>

> isNegative 4
False
```

- Instead of `(add(3,4))`, use `(add 3 4)`

- Anonymous function:

```
> \n -> n < 0
<function>

> (\n -> n < 0) 4
False
```

The parentheses in `(\n -> n < 0) 4` are important. After the arrow, Elm is just going to keep reading code as long as it can.

### If Expressions

```
> over9000 powerLevel = \
|   if powerLevel > 9000 then "It's over 9000!!!" else "meh"
<function>

> over9000 42
"meh"
```

>  Make sure that you add a whitespace before the second line of the function. Elm has a "syntactically significant whitespace" meaning that indentation is a part of its syntax.

### Lists

Values must all have the same type.

```
> names = [ "Alice", "Bob", "Chuck" ]
["Alice","Bob","Chuck"]

> List.isEmpty names
False

> numbers = [1,4,3,2]
[1,4,3,2]

> List.sort numbers
[1,2,3,4]

> double n = n * 2
<function>

> List.map double numbers
[2,8,6,4]
```

### Tuples

A tuple can hold a fixed number of values, and each value can have any type. A common use is if you need to return more than one value from a function. The following function gets a name and gives a message for the user:

```
> import String

> goodName name = \
|   if String.length name <= 20 then \
|     (True, "name accepted!") \
|   else \
|     (False, "name was too long; please limit it to 20 characters")

> goodName "Tom"
(True, "name accepted!")
```

> When things start becoming more complicated, it is often best to use records instead of tuples.

### Records

A record is a fixed set of key-value pairs.

```
> bill = { name = "Gates", age = 62 }
{ age = 62, name = "Gates" }

> bill.name
"Gates"
```

Elm also has a version of record access that works like a function. By starting the variable with a dot, you are saying *please access the field with the following name*. This means that `.name` is a function that gets the `name` field of the record.

```
> .name bill
"Gates"

> List.map .name [bill,bill,bill]
["Gates","Gates","Gates"]
```

Doing pattern matching:

```
> under70 {age} = age < 70
<function>

> under70 bill
True

> under70 { species = "Triceratops", age = 68000000 }
False
```

So we can pass any record in as long as it has an `age` field that holds a number.

Useful to update the values in a record:

```
bill = { name = "Gates", age = 62 }

> { bill | name = "Nye" }
{ age = 62, name = "Nye" }
```

> we do not make destructive updates. When we update some fields of bill we actually create a new record rather than overwriting the existing one.

> Records vs Objects
>> You cannot ask for a field that does not exist
>> No field will ever be `undefined` or `null`
>> You cannot create recursive records with a this or self keyword.
> data vs logic: Elm encourages a strict separation of data and logic, and the ability to say `this` is primarily used to break this separation. This is a systemic problem in Object Oriented languages that Elm is purposely avoiding.

## The Elm Architecture

### The Basic Pattern

- **Model** — the state of your application
- **Update** — a way to update your state
- **View** — a way to view your state as HTML
















----------

> From Elm Training at carwow

- ##Strings##: only `""`
- "a" ++ (String.fromInt 1): notice parentesis around function not around parameters

```
y = "I love carwow.co.uk"
String.slice 7 13 y
String.contains "carwow" y
```

```
(2 == 3) 
(2 /= 3)
(2 <= 3)
```

All types should be the same on branches

```
if (1 < 2) then "it's true" else False
```

```
sumTwoNumbers a b = a + b
sumTwoNumbers 1 3
```







------

> From [Elm Cheat Sheet](https://github.com/izdi/elm-cheat-sheet)

## Primitives

```
> 'a'
'a' : Char
> "Hello"
"Hello" : String

> 'ab'
-- SYNTAX PROBLEM --
> "ab"
"ab" : String
```

## Collections

Ways to create a list:

```
> List.range 1 4
> [1,2,3,4]
> 1 :: [2,3,4]
> 1 :: 2 :: 3 :: 4 :: []
```

Tuples have a minumum of two elements and maximum of nine. Possible to use commas as a tuple function, like a [prefix operation](https://github.com/izdi/elm-cheat-sheet#prefix).

```
> (,,,) 1 True 'a' []
(1,True,'a',[]) : ( number, Bool, Char, List a )
```

Destructuring:

```
(x, y) = (1, 2)
> x
1 : number
```

```
myRecord =
 { style = "Blue",
   number = 1,
   isCool = True
 }

 > myRecord.style
"Blue" : String
> .style myRecord
"Blue" : String
```

Updating records returns a new record.
Destructuring:

```
{ style, number, isCool } = myRecord
> style
"Blue" : String
```

Extensible records:

```
type alias Mammal r = {
   r | legs : Int
}

cat : Mammal
    { name : String
    , ageInHumanYears = 13
    }

cat =
  { name = "Mittens"
  , ageInHumanYears = 13
  , legs = 4
  }
```

```
-- mutate is a function that can work on any Mammal

mutate : Mammal r -> Mammal r
mutate mammal =
    { mammal | legs = mammal.legs + 1 }

mutatedCat = mutate cat
mutatedCat.legs == 5
```

## Functions

```
sum a b = a + b

-- combine arguments in a tuple
sum (a, b) = a + b
```

```
-- Both are equal
myFunction arg1 arg2
((myFunction arg1) arg2)

-- Partial application
> minus x y = (-) x y
<function> : number -> number -> number
> minus1 = minus 1
<function> : number -> number
> minus1 11
-10 : number
```

Anonymous:

```
-- (\function arguments -> function body)
-- parenthesized, content starts with backslash
(\n -> n < 0)
(\x y -> x * y)
```

```
-- Normally you would do this
> "abcde" ++ "fghij"
"abcdefghij" : String

-- Prefix
> (++) "abcde" "fghij"
"abcdefghij" : String
```

## Types

Union types can have one of the values (or tags):

```
type Person a
  = Name String
  | Surname String
  | Age Int
  | About a
```

A `Maybe` can help you with optional arguments, error handling, and records with optional fields. Think of it as a kind of `null`.

```
-- Maybe resides in a module
import Maybe exposing ( Maybe(..) )

-- Takes an argument that can be filled with any value
type Maybe a = Just a | Nothing

getId : Int -> Maybe Int
getId id =
  if id >= 0 then
    Just id
  else
    Nothing
```

## Type Aliases

Give existing types a custom name with `type alias`:

```
type alias Name = String
type alias Dob = String

type alias Record = { name: Name, dob: Dob }

record : Record
record =
    { name = "Dave", dob = "27/08/1999" }
```

`type alias` equals to it's parent `type`

```
type alias Name = String

name : Name
name =
  "Dave"

secondName : String
secondName =
  "Dave"

-- True
name == secondName
```

## Control Statements

If: no matter which one we take, we get back the same type of value overall.

```
if y > 0 then
    "Greater"
else if x /= 0 then
    "Not equals"
else
    "silence"
```

Elm does not have the notion of “truthiness”.
The condition must evaluate to True or False, and nothing else.

```
> if 1 then "nope" else "nope again"
- TYPE MISMATCH --
```

```
type User
    = Activated Int
    | Deleted (Int, String)

update state =
  case state of
    Activated value ->
      -- do something with value
    Deleted values ->
      -- do something with values

update ( Activated 1 )
update ( Deleted (0, "gone") )
```

```
let
  activeUsers = List.filter (\u -> u.state /= 1) model.users
in
  { model | user = activeUsers}
```






















