From [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)

# A re-introduction to JavaScript(JS tutroial)

## Numbers

```
parseInt('123', 10); // 123
parseInt('010', 10); // 10
```
If you want to convert a binary number to an integer, just change the base:

```
parseInt('11', 2); // 3
```

Similarly, you can parse floating point numbers using the built-in `parseFloat()` function. Unlike its `parseInt()` cousin, `parseFloat()` always uses base 10.
You can also use the unary `+` operator to convert values to numbers:

```
+ '42';   // 42
+ '010';  // 10
+ '0x10'; // 16
```

A special value called NaN (short for "Not a Number") is returned if the string is non-numeric:

```
parseInt('hello', 10); // NaN
NaN + 5; // NaN (if you pass it as an operand to any mathematical operation)
isNaN(NaN); // true
```

JavaScript also has the special values `Infinity` and `-Infinity`:

```
1 / 0; //  Infinity
-1 / 0; // -
isFinite(1 / 0); // false
isFinite(-Infinity); // false
isFinite(NaN); // false
```

> The `parseInt()` and `parseFloat()` functions parse a string until they reach a character that isn't valid for the specified number format, then return the number parsed up to that point. However the "+" operator simply converts the string to `NaN` if there is an invalid character contained within it.

	```
	> parseFloat("10.2abc", 10)
	10.2
	> parseInt("10.2abc", 10)
	10
	> + "10.2abc"
	NaN
	```

## Strings

```
'hello'.length; // 5
'hello'.charAt(0); // "h"
'hello, world'.replace('hello', 'goodbye'); // "goodbye, world"
'hello'.toUpperCase(); // "HELLO"
```

## Other Types

`false`, `0`, empty strings (`""`), `NaN`, `null`, and `undefined` all become `false`.

```
Boolean('');  // false
Boolean(234); // true
```

## Variables

New variables in JavaScript are declared using one of three keywords: `let`, `const`, or `var`.

`let` allows you to declare block-level variables. The declared variable is available from the *block* it is enclosed in.

```
// myLetVariable is *not* visible out here

for (let myLetVariable = 0; myLetVariable < 5; myLetVariable++) {
  // myLetVariable is only visible in here
}

// myLetVariable is *not* visible out here
```

`const` allows you to declare variables whose values are never intended to change. The variable is available from the *block* it is declared in.

```
const Pi = 3.14; // variable Pi is set 
Pi = 1; // will throw an error because you cannot change a constant variable.
```

`var` is the most common declarative keyword. It does not have the restrictions that the other two keywords have. This is because it was traditionally the only way to declare a variable in JavaScript. A variable declared with the `var` keyword is available from the *function* it is declared in.

```
// myVarVariable *is* visible out here 

for (var myVarVariable = 0; myVarVariable < 5; myVarVariable++) { 
  // myVarVariable is visible to the whole function 
} 

// myVarVariable *is* visible out here
```

An important difference between JavaScript and other languages like Java is that in JavaScript, blocks do not have scope; only functions have a scope. So if a variable is defined using `var` in a compound statement (for example inside an `if` control structure), it will be visible to the entire function. However, starting with ECMAScript 2015, `let` and `const` declarations allow you to create block-scoped variables.

## Operators

If you add a string to a number (or other value) everything is converted in to a string first. This might catch you out:

```
'3' + 4 + 5;  // "345"
 3 + 4 + '5'; // "75"
```
Adding an empty string to something is a useful way of converting it to a string itself.

The double-equals operator performs type coercion if you give it different types, with sometimes interesting results:

```
123 == '123'; // true
1 == true; // true
123 === '123'; // false
1 === true;    // false
```

Check the [link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) for bitwise operators

## Control Structures

JavaScript has `while` loops and `do-while` loops. The first is good for basic looping; the second for loops where you wish to ensure that the body of the loop is executed at least once:

```
var name = 'kittens';
if (name == 'puppies') {
  name += ' woof';
} else if (name == 'kittens') {
  name += ' meow';
} else {
  name += '!';
}
name == 'kittens meow';
```

```
while (true) {
  // an infinite loop!
}

var input;
do {
  input = get_input();
} while (inputIsNotValid(input));
```

```
for (var i = 0; i < 5; i++) {
  // Will execute 5 times
}
```
ECMAScript introduced the more concise `for...of` loop for iterable objects such as arrays.

```
let iterable = [10, 20, 30];

for (let value of iterable) {
  value += 1;
  console.log(value);
}
// 11
// 21
// 31
```
You could also iterate over an array using a `for...in` loop, however this does not iterate over the array elements, but the array indices. Furthermore, if someone added new properties to `Array.prototype`, they would also be iterated over by such a loop. Therefore this loop type is not recommended for arrays.

```
for (let property in object) {
  // do something with object property
}

var obj = {a: 1, b: 2, c: 3};
    
for (const prop in obj) {
  console.log(`obj.${prop} = ${obj[prop]}`);
}

// "obj.a = 1"
// "obj.b = 2"
// "obj.c = 3"
```

Another way of iterating over an array that was added with ECMAScript 5 is `forEach()`:

```
var array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});

// "a"
// "b"
// "c"
```

This is useful for checking for null objects before accessing their attributes:

```
var name = o && o.getName();
```

Or for caching values (when falsy values are invalid):

```
var name = cachedName || (cachedName = getName());
```

JavaScript has a ternary operator for conditional expressions:

```
var allowed = (age > 18) ? 'yes' : 'no';
```

The `switch` statement can be used for multiple branches based on a number or string:

```
switch (action) {
  case 'draw':
    drawIt();
    break;
  case 'eat':
    eatIt();
    break;
  default:
    doNothing();
}
```

If you don't add a `break` statement, execution will "fall through" to the next level. The default clause is optional.

## Objects

JavaScript objects can be thought of as simple collections of name-value pairs. The "name" part is a JavaScript string, while the value can be any JavaScript value — including more objects.

```
var obj = new Object();
// or
var obj = {}; // this is called object literal syntax and is more convenient. 
```

```
var obj = {
  name: 'Carrot',
  for: 'Max', // 'for' is a reserved word, use '_for' instead.
  details: {
    color: 'orange',
    size: 12
  }
};
```

The following example creates an object prototype, `Person` and an instance of that prototype, `you`.

```
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Define an object
var you = new Person('You', 24); 
// We are creating a new person named "You" aged 24.
```

```
// dot notation
obj.name = 'Simon';
var name = obj.name;
// bracket notation
obj['name'] = 'Simon';
var name = obj['name'];
```

#### dot vs bracket notation

- bracket notation has the advantage that the name of the property is provided as a string, which means it can be calculated at run-time.
-  It can also be used to set and get properties with names that are reserved words.
-  However, using this method prevents some JavaScript engine and minifier optimizations being applied.

> Starting in ECMAScript 5, reserved words may be used as object property names "in the buff". This means that they don't need to be "clothed" in quotes when defining object literals. See the ES5 [Spec](http://es5.github.io/#x7.6.1).

## Arrays

Note that `array.length` isn't necessarily the number of items in the array. Consider the following:

```
var a = ['dog', 'cat', 'hen'];
a[100] = 'fox';
a.length; // 101 — the length of the array is one more than the highest index.
```

Arrays come with a number of methods. See also the [full documentation for array methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

## Functions

If no return statement is used (or an empty return with no value), JavaScript returns `undefined`. You can call a function without passing the parameters it expects, in which case they will be set to `undefined`.

```
function add(x, y) {
  var total = x + y;
  return total;
}

add(); // NaN
// You can't perform addition on undefined

add(2, 3, 4); // 5
// added the first two; 4 was ignored
```

That may seem a little silly, but functions have access to an additional variable inside their body called `arguments`, which is an array-like object holding all of the values passed to the function. Let's re-write the add function to take as many values as we want:

```
function add() {
  var sum = 0;
  for (var i = 0, j = arguments.length; i < j; i++) {
    sum += arguments[i];
  }
  return sum;
}

add(2, 3, 4, 5); // 14
```

To reduce this code a bit more we can look at substituting the use of the arguments array through [Rest parameter syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters). The **rest parameter operator** is used in function parameter lists with the format: **...variable** and it will include within that variable the entire list of uncaptured arguments that the function was called with. We will also replace the `for` loop with a `for...of` loop to return the values within our variable. Also, that's really not any more useful than writing 2 + 3 + 4 + 5 though. Let's create an averaging function:

```
function avg(...args) {
  var sum = 0;
  for (let value of args) {
    sum += value;
  }
  return sum / args.length;
}

avg(2, 3, 4, 5); // 3.5
```

> It is important to note that wherever the rest parameter operator is placed in a function declaration it will store all arguments *after* its declaration, but not before. *i.e. function avg(**firstValue,** ...args)* will store the first value passed into the function in the **firstValue** variable and the remaining arguments in **args**. That's another useful language feature but it does lead us to a new problem. The `avg()` function takes a comma-separated list of arguments — but what if you want to find the average of an array? You could just rewrite the function as follows:

```
function avgArray(arr) {
  var sum = 0;
  for (var i = 0, j = arr.length; i < j; i++) {
    sum += arr[i];
  }
  return sum / arr.length;
}

avgArray([2, 3, 4, 5]); // 3.5
```

But it would be nice to be able to reuse the function that we've already created. Luckily, JavaScript lets you call a function with an arbitrary array of arguments, using the `apply()` method of any function object.

```
avg.apply(null, [2, 3, 4, 5]); // 3.5
```
This emphasizes the fact that functions are objects too.

> You can achieve the same result using the [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator) in the function call:

```
const numbers = [2, 3, 4, 5];
avg(...numbers);
```

JavaScript lets you create anonymous functions.

```
var avg = function() {
  var sum = 0;
  for (var i = 0, j = arguments.length; i < j; i++) {
    sum += arguments[i];
  }
  return sum / arguments.length;
};
```
This enables all sorts of clever tricks. Here's a way of "hiding" some local variables:

```
var a = 1;
var b = 2;

(function() {
  var b = 3;
  a += b;
})();

a; // 4
b; // 2
```

JavaScript allows you to call functions recursively. This is particularly useful for dealing with tree structures, such as those found in the browser DOM.

```
function countChars(elm) {
  if (elm.nodeType == 3) { // TEXT_NODE
    return elm.nodeValue.length;
  }
  var count = 0;
  for (var i = 0, child; child = elm.childNodes[i]; i++) {
    count += countChars(child);
  }
  return count;
}
```

How do you call them recursively if they don't have a name? You can use named [IIFEs (Immediately Invoked Function Expressions)](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) as shown below:

```
var charsInBody = (function counter(elm) {
  if (elm.nodeType == 3) { // TEXT_NODE
    return elm.nodeValue.length;
  }
  var count = 0;
  for (var i = 0, child; child = elm.childNodes[i]; i++) {
    count += counter(child);
  }
  return count;
})(document.body);
```

The name provided to a function expression as above is only available to the function's own scope. This allows more optimizations to be done by the engine and results in more readable code. The name also shows up in the debugger and some stack traces, which can save you time when debugging.

Note that JavaScript functions are themselves objects — like everything else in JavaScript — and you can add or change properties on them just like we've seen earlier in the Objects section.

## Custom Objects

For a more detailed discussion of object-oriented programming in JavaScript, see [Introduction to Object-Oriented JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript).

JavaScript is a prototype-based language that contains no class statement, as you'd find in C++ or Java (this is sometimes confusing for programmers accustomed to languages with a class statement). Instead, JavaScript uses functions as classes. Let's consider a person object with first and last name fields.

```
function makePerson(first, last) {
  return {
    first: first,
    last: last,
    fullName: function() {
      return this.first + ' ' + this.last;
    },
    fullNameReversed: function() {
      return this.last + ', ' + this.first;
    }
  };
}

s = makePerson('Simon', 'Willison');
s.fullName(); // "Simon Willison"
s.fullNameReversed(); // "Willison, Simon"
```
Used inside a function, `this` refers to the current object. If you called it using [dot notation or bracket notation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Accessing_properties) on an object, that object becomes `this`. If dot notation wasn't used for the call, `this` refers to the global object.

```
s = makePerson('Simon', 'Willison');
var fullName = s.fullName;
fullName(); // undefined undefined
```

When we call `fullName()` alone, without using `s.fullName()`, `this` is bound to the global object. Since there are no global variables called `first` or `last` we get `undefined` for each one.

```
function Person(first, last) {
  this.first = first;
  this.last = last;
  this.fullName = function() {
    return this.first + ' ' + this.last;
  };
  this.fullNameReversed = function() {
    return this.last + ', ' + this.first;
  };
}
var s = new Person('Simon', 'Willison');
```

It creates a brand new empty object, and then calls the function specified, with `this` set to that new object. Notice though that the function specified with `this` does not return a value but merely modifies the `this` object. It's `new` that returns the `this` object to the calling site. Functions that are designed to be called by `new` are called *constructor functions*. Common practice is to capitalize these functions as a reminder to call them with `new`.

The improved function still has the same pitfall with calling `fullName()` alone.

Every time we create a person object we are creating two brand new function objects within it — wouldn't it be better if this code was shared?

```
function personFullName() {
  return this.first + ' ' + this.last;
}
function personFullNameReversed() {
  return this.last + ', ' + this.first;
}
function Person(first, last) {
  this.first = first;
  this.last = last;
  this.fullName = personFullName;
  this.fullNameReversed = personFullNameReversed;
}
```
Or even better:

```
function Person(first, last) {
  this.first = first;
  this.last = last;
}
Person.prototype.fullName = function() {
  return this.first + ' ' + this.last;
};
Person.prototype.fullNameReversed = function() {
  return this.last + ', ' + this.first;
};
```

`Person.prototype` is an object shared by all instances of `Person`. It forms part of a lookup chain (that has a special name, "prototype chain"): any time you attempt to access a property of `Person` that isn't set, JavaScript will check `Person.prototype` to see if that property exists there instead. As a result, anything assigned to `Person.prototype` becomes available to all instances of that constructor via the `this` object.

This is an incredibly powerful tool. JavaScript lets you modify something's prototype at any time in your program, which means you can add extra methods to existing objects at runtime:

```
s = new Person('Simon', 'Willison');
s.firstNameCaps(); // TypeError on line 1: s.firstNameCaps is not a function

Person.prototype.firstNameCaps = function() {
  return this.first.toUpperCase();
};
s.firstNameCaps(); // "SIMON"
```

Interestingly, you can also add things to the prototype of built-in JavaScript objects. Let's add a method to `String` that returns that string in reverse:

```
var s = 'Simon';
s.reversed(); // TypeError on line 1: s.reversed is not a function

String.prototype.reversed = function() {
  var r = '';
  for (var i = this.length - 1; i >= 0; i--) {
    r += this[i];
  }
  return r;
};

s.reversed(); // nomiS
```

As mentioned before, the prototype forms part of a chain. The root of that chain is `Object.prototype`, whose methods include `toString()` — it is this method that is called when you try to represent an object as a string. This is useful for debugging our `Person` objects:

```
var s = new Person('Simon', 'Willison');
s.toString(); // [object Object]

Person.prototype.toString = function() {
  return '<Person: ' + this.fullName() + '>';
}

s.toString(); // "<Person: Simon Willison>"
```

Remember how `avg.apply()` had a null first argument? We can revisit that now. The first argument to `apply()` is the object that should be treated as `'this'`. For example, here's a trivial implementation of `new`:

```
function trivialNew(constructor, ...args) {
  var o = {}; // Create an object
  constructor.apply(o, args);
  return o;
}
```

This isn't an exact replica of `new` as it doesn't set up the prototype chain (it would be difficult to illustrate). This is not something you use very often, but it's useful to know about. In this snippet, `...args` (including the ellipsis) is called the "[rest arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)" — as the name implies, this contains the rest of the arguments.

Calling:

```
var bill = trivialNew(Person, 'William', 'Orange');
// is therefore almost equivalent to
var bill = new Person('William', 'Orange');
```

`apply()` has a sister function named [`call`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call), which again lets you set this but takes an expanded argument list as opposed to an array.

```
function lastNameCaps() {
  return this.last.toUpperCase();
}
var s = new Person('Simon', 'Willison');
lastNameCaps.call(s);
// Is the same as:
s.lastNameCaps = lastNameCaps;
s.lastNameCaps(); // WILLISON
```

### Inner Functions

An important detail of nested functions in JavaScript is that they can access variables in their parent function's scope:

```
function parentFunc() {
  var a = 1;

  function nestedFunc() {
    var b = 4; // parentFunc can't use this
    return a + b; 
  }
  return nestedFunc(); // 5
}
```

- If a function relies on one or two other functions that are not useful to any other part of your code, you can nest those utility functions inside the function that will be called from elsewhere. This keeps the number of functions that are in the global scope down, which is always a good thing.

- When writing complex code it is often tempting to use global variables to share values between multiple functions — which leads to code that is hard to maintain. Nested functions can share variables in their parent, so you can use that mechanism to couple functions together when it makes sense without polluting your global namespace — "local globals" if you like. This technique should be used with caution, but it's a useful ability to have.

## Closures

A **closure** is the combination of a function and the scope object in which it was created. Closures let you save state — as such, they can often be used in place of objects. You can find [several excellent introductions to closures](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work).

```
function makeAdder(a) {
  return function(b) {
    return a + b;
  };
}
var x = makeAdder(5);
var y = makeAdder(20);
x(6); // 11
y(7); // 27
```

The name of the `makeAdder()` function should give it away: it creates new 'adder' functions, each of which, when called with one argument, adds it to the argument that it was created with.

The only difference here is that the outer function has returned, and hence common sense would seem to dictate that its local variables no longer exist. But they *do* still exist — otherwise, the adder functions would be unable to work. What's more, there are two different "copies" of `makeAdder()`'s local variables — one in which a is 5 and the other one where a is 20.

Here's what's actually happening. Whenever JavaScript executes a function, a 'scope' object is created to hold the local variables created within that function. It is initialized with any variables passed in as function parameters. This is similar to the global object that all global variables and functions live in, but with a couple of important differences:

- firstly, a brand new scope object is created every time a function starts executing, and
- secondly, unlike the global object (which is accessible as this and in browsers as window) these scope objects cannot be directly accessed from your JavaScript code.

There is no mechanism for iterating over the properties of the current scope object, for example.

So when `makeAdder()` is called, a scope object is created with one property: `a`, which is the argument passed to the `makeAdder()` function. `makeAdder()` then returns a newly created function. Normally JavaScript's garbage collector would clean up the scope object created for `makeAdder()` at this point, but the returned function maintains a reference back to that scope object. As a result, the scope object will not be garbage-collected until there are no more references to the function object that `makeAdder()` returned.

Scope objects form a chain called the scope chain, similar to the prototype chain used by JavaScript's object system.


























