# Tagged Templates

Tags allow you to parse template literals with a function. The first
argument of a tag function contains an array of string values. The
remaining arguments are related to the expressions.

The tag function can then perform whatever operations on these arguments
you wish, and return the manipulated string. (Alternatively, it can
return something completely different.

```
const person = "Mike";
const age = 28;

function myTag(strings, personExp, ageExp) {
    const str0 = strings[0];  // "That"
    const str1 = strings[1];  // " is a "
    const str2 = strings[2];  // "."
    
    const ageStr = ageExp > 99 ? "centenarian" : "youngster";

    return `${str0}${personExp}${str1}${ageStr}${str2}`;
}

const output = myTag`That ${person} is a ${age}.`

console.log(output);
```

The special `raw` property, available on the first argument to the tag
function, allows you to access the raw strings as they were entered,
without processing escape sequences.

In addition, the `String.raw()` method exists to create raw strings just
like the default template function and string concatenation would create.






