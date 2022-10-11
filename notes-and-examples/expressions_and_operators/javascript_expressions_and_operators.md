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

Most operators that can be used between numbers can be used between BigInt values
as well.

BigInts and numbers are not mutually replaceable — you cannot mix them in calculations.
You can compare BigInts with numbers.

This is because BigInt is neither a subset nor a superset of numbers.

## String Operators

The concatenation operator (+) concatenates two string values together, returning another
string that is the union of the two operand strings.

## Comma Operator

The comma operator evaluates both of its operands and returns the value of the last operand.
This operator is primarily used inside a for loop, to allow multiple variables to be updated
each time through the loop. It is regarded bad style to use it elsewhere when it is not
necessary.

```
const x = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
const a = [x, x, x, x, x];

for (let i = 0, j = 9; i <= j; i++, j--) {
    console.log(`a[${i}][${j}]= ${a[i][j]}`);
}
```

## Delete Operator

The `delete` operator deletes an object's property.

The syntax is:
```
delete object.property;
delete object[propertyKey];
delete objectName[index];
```

where `object` is the name of an object, `property` is an existing property, and `propertyKey` is a
string or symbol referring to an existing property.

The `delete` operator returns `true` is the operation is possible; it returns `false` if the
operation is not possible.

## Typeof Operator

The `typeof` operator returns a string indicating the type of the unevaluated operand.

## Void Operator

The `void` operator is used in either of the following ways:
```
void (expression)
void expression
```

The `void` operator specifies an expression to be evaluated without returning a value. It is good
style to use the optional parentheses.

## In Operator

The `in` operator returns `true` if the specified property is in the specified object.
The syntax is:

```
propNameOrNumber in objectName
```

where `propNameOrNumber` is a string, numeric, or symbol expression representing a property name
or array index, and `objectName` is the name of an object.

## Instanceof Operator

The `instanceof` operator returns `true` if the specified object is of the specified object type.
The syntax is:

```
objectName instanceof objectType
```

