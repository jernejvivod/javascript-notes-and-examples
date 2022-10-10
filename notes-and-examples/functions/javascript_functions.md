# Functions

## Function Declarations

A functio definition (also called a function declaration, or function statement) consists of the function keyword followed by:
- The name of the function,
- A list of parameters to the function, enclosed in parenheses and separated by commas,
- The JavaScript statements that efine the function, eclosed in curly brackets, `{ /* ... */ }`.

For example, the following code defines simple function named `square`:

```
function square(number) {
    return number * number;
}
```

## Function Expressions

While the function declaration above  is syntactically a statement, functions can also be created by a function expression.

Such a function can be anonymous; it does not have to have a name. For example, the function `square` could have been defined as:

```
const square = function (number) {
    return number * number;
}
```

or 

```
const square = number => number * number
```


However, a name can be provided with a function expression. Providing a name allows the function to refer to itself, and also makes it easier to identify the function in a debugger's stack traces:

```
const factorial = function fac(n) {
    return n < 2 ? 1 : n * fac(n - 1);
}
```

Note that function hoisting only works with function declarations, not with function expressions.

Functions are themselves objects and in turn have methods. The `call()` and `apply()` methods can be used to call the function.


## Recursion

A function can refer to and call itself. There are three ways for a function to refer to itself:

1. the function's name
2. `arguments.callee`
3. An in-scope variable that refers to the function

For example, consider the following function definition:

```
const foo = function bar() {
  // statements go here
}
```

Within the function body, the following are all equivalent:
1. `bar()`
2. `arguments.callee()`
3. `foo()`


## Using the Arguments Object

The arguments of a function are maintained in an array-like object. Within a function, you can address the arguments passed to it as follows:
```
arguments[i]
```

Using the `arguments` object, you can call a function with more arguments than it is formally declared to accept. This is often useful if you don't know in advance how many arguments will be passed to the function. You can use `arguments.length` to determine
the number of arguments actually passed to the function, and then access each argument using the `arguments` object.

For example, consider a function that concatenates several strings. The only formal argument for the function is a string that specifies the characters that separate the items to concatenate. The function is defined as follows:

```
function myConcat(separator) {
  let result = '';
  for (let i = 1; i < arguments.length; i++) {
    result += arguments[i] + separator;
  }
  return result;
}

// returns "red, orange, blue, "
myConcat(', ', 'red', 'orange', 'blue');

// returns "elephant; giraffe; lion; cheetah; "
myConcat('; ', 'elephant', 'giraffe', 'lion', 'cheetah');

// returns "sage. basil. oregano. pepper. parsley. "
myConcat('. ', 'sage', 'basil', 'oregano', 'pepper', 'parsley');
```

Note, the `arguments` variable does not possess all of the array-manipulation methods.

## Function Parameters

There are two special kinds of parameter syntax: default parameters and rest parameters.

### Default parameters

In JavaScript, parameters of functions default to undefined. However, in some situations, it might be useful to set a different default value.

In the past, the general strategy for setting defaults was to test parameter values in the body of the function and assign a value if they are undefined.

```
function multiply(a, b) {
  b = typeof b !== 'undefined' ?  b : 1;
  return a * b;
}

multiply(5); // 5
```

With default parameters, a manual check in the function body is no longer necessary:

```
function multiply(a, b = 1) {
  return a * b;
}

multiply(5);  // 5
```

### Rest Parameters

The rest parameters syntax allows us to represent an indefinite number of arguments as an array.

```
function multiply(multiplier, ...theArgs) {
  return theArgs.map(x => multiplier * x);
}

const arr = multiply(2, 1, 2, 3);
console.log(arr); // [2, 4, 6]
```

### Arrow Functions

Arrow functions do not have its own `this`, `arguments`, `super` or `new.target`.


