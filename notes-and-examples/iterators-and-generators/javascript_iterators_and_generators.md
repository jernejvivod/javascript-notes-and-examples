# Iterators and Generators

## Iterators

In JavaScript an iterator is an object which defines a sequence and potentially a return value
upon its termination.

Specifically, an iterator is any object which implements the iterator protocol by having
a `next()` method that returns an object with two properties — `value` and `done`.

After a terminating value has been yielded additional calls to `next()` should continue to
return `{done: true}`.

An example of an iterator:

```
function makeRangeIterator(start = 0, end = Infinity, step = 1) {
    let nextIndex = start;
    let iterationCount = 0;

    const rangeIterator = {
        next() {
            let result;
            if (nextIndex < end) {
                result = { value: nextIndex, done: false };
                nextIndex += step;
                iterationCount++;
                return result;
            }
            return { value: iterationCount, done: true };
        }
    }
    return rangeIterator;
}
```

Note: it is not possible to know reflectively whether a particular object is an iterator. If you
need to do this, use Iterables.


## Generator Functions

Generator functions are written using the `function*` syntax.

When called, generator functions do not initially execute their code. Instead, they return a
special type of iterator, called a Generator.

Calling the function returns a generator. Each generator may only be iterated once.

Example of a generator function:

```
function* makeRangeIterator(start = 0, end = Infinity, step = 1) {
    let iterationCount = 0;
    for (let i = start; i < end, i += step) {
        iterationCount++;
        yield i;
    }
    return iterationCount;
}
```

## Iterables

An object is iterable if it defines its iteration behavior, such as what values are looped over
in a `for...of` construct.

In order to be iterable, an object must implement the `@@iterator` method. This means that the
object (or one of the objects up its prototype chain) must have a property with a `Symbol.iterator` key.

It may be possible to iterate over an iterable more than once, or only once.

Iterables which can iterate only once (such as Generators) customarily return `this` from their
`@@iterator` method, whereas iterables which can be iterated many times must return a new
iterator on each invocation of `@@iterator`.


## User-Defined Iterables

You can make your own iterables like this:

```
const myIterable = {
    *[Symbol.iterator]() {
        yield 1;
        yield 2;
        yield 3;
    }
}
```

User-defined iterables can be used in `for...of` loops or the spread syntax as usual.

## The yield\* Keyword

The `yield*` expression is used to delegate to another generator or iterable object.

Examples:
```
function* func1() {
  yield 42;
}

function* func2() {
  yield* func1();
}

const iterator = func2();

console.log(iterator.next().value);
// expected output: 42
```

## Advanced Generators

Generators compute their `yield` values on demand, which allows them to efficiently represent
sequences that are expensive to compute (or are infinite).

The `next()` method also accepts a value, which can be used to modify the internal state of the
generator. A value passed to `next()` will be received by `yield`.


Here is a fibonacci generator using `next(x)` to restart the sequence:

```
function* fibonacci() {
    let current = 0;
    let next = 1;
    while (true) {
        const reset = yield current;
        [current, next] = [next, next + current];
        if (reset) {
            current = 0;
            next = 1;
        }
    }
}

const sequence = fibonacci();
console.log(sequence.next().value);     // 0
console.log(sequence.next().value);     // 1
console.log(sequence.next().value);     // 1
console.log(sequence.next().value);     // 2
console.log(sequence.next().value);     // 3
console.log(sequence.next().value);     // 5
console.log(sequence.next().value);     // 8
console.log(sequence.next(true).value); // 0
console.log(sequence.next().value);     // 1
console.log(sequence.next().value);     // 1
console.log(sequence.next().value);     // 2
```

You can force a generator to throw an exception by calling its `throw()` method and passing the
exception value it should throw.

This exception will be thrown from the current suspended context of the generator, as if the `yield`
that is currently suspended were instead a `throw value` statement.

If the exception is not caught from within the generator, it will propagate up through the call
to `throw()`, and subsequent calls to `next()` will result in the `done` property being `true`.

Generators have a `return(value)` method that returns the given value and finishes the generator
itself.

