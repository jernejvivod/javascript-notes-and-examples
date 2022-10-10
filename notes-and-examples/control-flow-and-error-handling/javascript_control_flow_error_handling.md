# Control Flow and Error Handling

The semicolon character is used to separate statements in JavaScript code.

Any JavaScript expression is also a statement.

## Block Statement

The most basic statement is a block statement, which is used to group
statements. The block is delimited by a pair of curly brackets.

```
{
  statement1;
  statement2;
  // ...
  statementN;
}
```


Note that `var`-declared variables are not block-scoped, but are scoped to
the containing function or script, and the effect of setting them
persist beyond the block itself.


## Falsy Values

The following values evaluate to false:
- false
- undefined
- null
- 0
- NaN
- ""

Note: Do not confuse the primitive boolean values `true` and `false` with
the true and false values of the `Boolean` object.

```
const b = new Boolean(false);
if (b) {
  // this condition evaluates to true
}
if (b == true) {
  // this condition evaluates to false
}
```

## Exception Handling Statements

You can throw exceptions using the `throw` statement and handle
them using the `try...catch` statements.

### Exception Types

Just about any object can be thrown in JavaScript. Nevertheless, not all
objects are created equal. While it is common to throw numbers or strings
as errors, it is frequently more effective to use one of the exception
types specifically created for this purpose:

- ECMAScript exceptions
- DOMException and DOMError

### Throw Statement

A `throw` statement specifies the value to be thrown:

### try...catch Statement

The `try...catch` statement marks a block of statements to try, and
specifies one or more responses should an exception be thrown.

You can use a `catch` block to handle all exceptions that may be generated
in the `try` block.

### The Finally Block

The finally block contains statements to be executed after the `try` and
`catch` block execute.

If the `finally` block returns a value, this value becomes the return
value of the entire `try...catch...finally` production, regardless of
any `return` statements in the `try` and `catch` blocks.

Overwriting of return values by the `finally` block also applies to
exceptions thrown or re-thrown inside of the `catch` block.

If you are throwing your own exceptions, in order to take advantage of
these properties (such as if your `catch` block doesn't discriminate
between your own exceptions and system ones), you can use the `Error`
constructor.

