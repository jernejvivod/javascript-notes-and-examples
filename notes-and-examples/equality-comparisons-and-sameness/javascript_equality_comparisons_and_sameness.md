# Equality Comparisons and Sameness

JavaScript provides three different value-comparison operations:

- `===` (strict equality)
- `===` (loose equality)
- `Object.is()`

`==` will perform a type conversion when comparing two things, and will handle `NaN`, `-0`, and
`+0` specially to conform to IEEE 754 (so `NaN != NaN`, and `-0 == +0`)

`===` will do the same comparison as double equals but without type conversion; if the types
differ, `false` is returned.

`Object.is()` does no type conversion and no special handling for `NaN`, `-0`, and `+0`.


`===` is almost always the correct comparison operation to use.

Strict equality is also used by array index-finding methods.

## Same-value Equality Using Object.is()


Same-value equality determines whether two values are functionally identical in all contexts. One
instance occurs when an attempt is made to mutate an immutable property:

```
// Add an immutable NEGATIVE_ZERO property to the Number constructor.
Object.defineProperty(Number, "NEGATIVE_ZERO", {
  value: -0,
  writable: false,
  configurable: false,
  enumerable: false,
});

function attemptMutation(v) {
  Object.defineProperty(Number, "NEGATIVE_ZERO", { value: v });
}
```


`Object.defineProperty` will throw an exception when attempting to change an immutable property,
but it does nothing if no actual change is requested. If `v` is `-0`, no change has been requested,
and no error will be thrown. Internally, when an immutable property is redefined, the newly
specified value is compared against the current value using same-value equality.

Same-value equality is provided by the `Object.is` method. It's used almost everywhere in the
language where a value of equivalent identity is expected.

