# Expressions and Operators

## Assigning to Properties

If an expression evaluates to an object, then the left-hand side
of an assignment expression may make assignments to properties of
that expression.

If an expression does not evaluate to an object, then assignments to
properties of that expression do not assign:

```
const val = 0;
val.x = 3;

console.log(val.x);  // prints undefined
console.log(val);    // prints 0
```

In strict mode, the code above throws, because one cannot assign properties
to primitives.


### Destructuring

A kind of pattern matching:

```
const foo = ['one', 'two', 'three'];

// without destructuring
const one   = foo[0];
const two   = foo[1];
const three = foo[2];

// with destructuring
const [one, two, three] = foo;
```

### Evaluation and Nesting

By chaining or nesting an assignment expression, its result can itself be
assigned to another variable. It can be logged, it can be put inside an
array literal or function call, and so on.

```
let x;
const y = (x = f()); // Or equivalently: const y = x = f();
console.log(y); // Logs the return value of the assignment x = f().

console.log(x = f()); // Logs the return value directly.

// An assignment expression can be nested in any place
// where expressions are generally allowed,
// such as array literals' elements or as function calls' arguments.
console.log([ 0, x = f(), 0 ]);
console.log(f(0, x = f(), 0));
```

Note that for all assignment operators other that `=` itself, the resulting
values are always based on the operand's values before the operation.

For example, assume that the following functions `f` and `g` and the
variables `x` and `y` have been declared:

```
function f () {
  console.log('F!');
  return 2;
}

function g () {
  console.log('G!');
  return 3;
}

let x, y;
```

Consider these three examples:

```
y = x = f();
y = [f(), x = g()];
x[f()] = g();
```

### Avoid Assignment Chains

Chaining assignments or nesting assignments in other expressions can result
in surprising behavior. For this reason, chaining assignments in the same
statement is discouraged.

In particular, putting a variable chain in a `const`, `let`, or `var`
statement often does not work. Only the outermost/leftmost variable would
get declared; other variables within the assignment chain are not declared
by the `const`/`let`/`var` statement. For example:

```
const z = y = x = f();
```

This statement seemingly declares the variables `x`, `y`, and `z`.
However, it only actually declares the variable `z`.

`y` and `x` are either invalid references to nonexistent variables
(in strict mode) or, worse, would implicitly create global variables for
`x` and `y` in sloppy mode.

## BigInt Operators

TODO

## String Operators

TODO

## Comma Operator

TODO

## Delete Operator

TODO

## Typeof Operator

TODO

## Void Operator

TODO

## In Operator

TODO

## Instanceof Operator

TODO


