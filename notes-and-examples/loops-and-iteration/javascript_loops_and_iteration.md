# Loops and Iteration

## Labeled Statement

A `label` provides a statement with an identifier that lets you refer
to it elsewhere in your program.

For example, you can use a label to identify a loop, and then use the
`break` or `continue` statements to indicate whether a program should
interrupt the loop or continue its execution.

The syntax of the labeled statement looks like the following:

```
label:
    statement
```

The value of `label` may be any JavaScript identifier that is not a
reserved word. The `statement` that you identify with a label may be any
statement.

Example:

```
markLoop:
while (theMark) {
    doSomething();
}
```


Using `break markLoop` can be used to break the corresponding loop.


## for...in Statement

The `for...in` statement iterates a specified variable over all the
enumerable properties of an object. For each distinct property, JavaScript
executes the specified statements.

## for...of Statement

The `for...of` statement creates a loop iterating over iterable objects
(including `Array`, `Map`, `Set`, `arguments` object and so on), invoking
a custom iteration hook with statements to be executed for the value of
each distinct property.

The following example demonstrates the difference between a `for...of` loop
and a `for...in` loop.

While `for...in` iterates over property names, `for...of` iterates over
property values:

```
const arr = [3, 5, 7];
arr.foo = 'hello';

for (const i in arr) {
  console.log(i); // logs "0", "1", "2", "foo"
}

for (const i of arr) {
  console.log(i); // logs 3, 5, 7
}
```

