# JavaScript

JavaScript s stanardied at Ecma International — the European association
for standardizing information and communication systems (ECMA was formerly
an acronym for the European Computer Manufacturers Association) to deliver
a standardzed, international programming language based on JavaScript.
This standardized version of JavaScript, called ECMAScript, behaves the
same way in all applications tha support the standard. Companies can use
the open standard language to develop their implementation of JavaScript.

the ECMAScript standard is documented in the ECMA-262 specification.

The ECMA-262 is also approved by the ISO as ISO-16262.

The ECMAScript specification does not describe the Document Object Model
(DOM), which is standardized by the World Wide Web Consortium (W3C) and/or
WHATWG (Web Hypertext Application Technology Working Group). The DOM
defines the way in which HTL document objects are exposed to your script.

To get a better idea about the different technologies that are used when
programming with JavaScript, consult the article 
`JavaScript technologies overview`.

## Declarations

`var` declares a variable, optionally initializing it to a value.

`let` declares a block-scoped, local variable, optionally initializing it to a value

`const` declares a block-scoped, read-only named constant


## Variables

A JavaScript identifier usually starts with a letter, underscore, or dollar sign. Subsequent characters can be
digits.

You can use most of ISO 8859-1 or Unicode letters in identifiers.

You can also assign a value to a variable, for example `x = 42` creates an undeclared global variable. It also generates
a strict JavaScript warning. Undeclared global variables can often lead to unexpected behavior. Thus, it is discouraged to use
undeclared global variables.


## Evaluating Variables

A variable declared using the `var` or `let` statemenet with no assigned value specified has the value of `undefined`.
An attempt to access an undeclared variable results in a `ReferenceError` exception being thrown.

Variables created with `var` are not block-scoped, but only local to the function (or global scope) that the block resides within.


## Variable Hoisting

Another unusual thing about variables in JavaScript is that you can refer to a variable declared later, without getting an exception.
However, variables that are hoisted return a value of `undefined`. So even if you declare and initialize after you use or refer to this variable,
it still returns undefined.

Because of hoisting, all `var` statements in a function should be placed as near to the top of the function as possible.
This best practice increases the clarity of the code.

`let` and `const` are hoisted but not initialized. Referencing the variable in the block before the variable declaration results in a `ReferenceError` because the variable is in a
"temporal dead zone" from the start of the block until the declaration is processed.


## Function Hoisting

Functions are hoisted if they're defined using function declarations. They are not hoisted if they are defined
using function expressions.

## Global Variables

Global variables are in fact properties of the global object.

In web pages, the global object is window, so you can set and access global variables using the `window.variable` syntax.

Consequently, you can access global variables declared in one window or frame from another window or frame by specifying the `window` of `Frame` name.

For example, if a variable called `phoneNumber` is declared in a document, you can refer to this variable from an iframe as `parent.phoneNumber`.


## Data Structures and Types

The latest ECMAScript standard defines eight data types:
1. `Boolean` (true and false)
2. `null` (denoting a null value)
3. `undefined` (top-level property whose value is not defined)
4. `Number` (an integer or floating point number)
5. `BigInt` (an integer with arbitrary precision)
6. `String` (a sequence of characters that represent a text value)
7. `Symbol` (a data type whose instances are unique and immutable)

and Object (non-primitive)


## Literals

If you put two commas in a row in an array literal, the array leaves an empty slot for the unspecified
element: `const myList = ['home', /* empty */, 'school', /* empty */, ];`

When using array-traversing methods like `Array.prototype.map`, empty slots are skipped. However, index-accessing
`fish[1]` still returns `undefined`.

The syntax of floating-point literals is:
`[digits].[digits][(E|e)[(+|-)]digits]`

## Object Literals

Enhanced object literals support a range of shorthand syntaxes that include setting the prototype
at construction, shorthand for `foo: foo` assignments, defining methods, making `super` calls, and
computing property names with expressions.

## RegExp Literals

A regex literal is a pattern enclosed between slashes:

```
const re = /ab+c/
```

## String Literals

template literals are also available. Template literals are enclosed by the back-tick and provide syntactic sugar for constructing
strings. Template strings can run over multiple lines, but double and single quoted strings cannot.

## Number Object

The built-in Number object has properties for numerical constants, such as maximum value, not-a-number, and infinity.


## Math Object

The built-in `Math` object has properties and methods for mathematical constants and functions.

## Date Object

JavaScript does not have a date data type. However, you can use the `Date` object and its methods to work with dates and times in your applications.

The `Date` object methods for handling dates and times fall into these broad categories:
- "set" methods, for setting date and time values in `Date` objects.
- "get" methods, for getting date and time values from `Date` objects,
- "to" methods, for returning string values from `Date` objects.
- parse and UTC methods, for parsing `Date` strings.



