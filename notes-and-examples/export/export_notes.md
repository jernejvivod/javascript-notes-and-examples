# Export and Import

Export and import directives have several syntax variants.


## Export

### Export Before Declarations

We can label any declaration as exported by placing export before it,
be it a variable, function, or a class:

```
export let months = ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
export const MODULES_BECAME_STANDARD_YEAR = 2015;

export class User {
    constructor(name) {
        this.name = name;
    }
}

export class User {
    constructor(name) {
        this.name = name;
    }
}

```

Export before a class or a function does not make it a function expression which means that semicolons are not recommended.

### Separate Export

We can also put export separately:

```
function sayHi(user) {
    alert(`Hello, ${user}!`);
}

function sayBye(user) {
    alert(`Bye, ${user}!`);
}

export {sayHi, sayBye}
```

Technically, we could put export above functions as well.


## Import

Usually, we put a list of what to import in curly braces `import {...}`, like this:

```
import {sayHi, sayBye} from './say.js'

sayHi('John');   // Hello, John!
sayBye('John');  // Bye, John!
```

But if there's a lot to import, we can import everything as an object using `import * as <obj>`, for instance:

```
import * as say from '.say.js';

say.sayHi('John');
say.sayBye('John');
```

Why is it useful to explicitly list what we need to import?

1. Modern build tools (webpack and others) bundle modules together and optimize them to speedup loading and remove unused stuff.

Let's say, we added a 3rd-party library `say.js` to our project with many functions:

```
// say.js
export function sayHi() { ... }
export function sayBye() { ... }
export function becomeSilent() { ... }
```

Now if we only use one of `say.js` functions in our project:

```
// main.js
import {sayHi} from './say.js';
```

Then the optimizer will see that and remove the other functions from the bundled code, thus making the build smaller. That is called "tree-shaking".


2. Explicitly listing what to import gives us shorter names: `sayHi()` instead of `say.sayHi()`.

3. Explicit list of imports gives better overview of the code structure: what is used and where. It makes code support and refactoring easier.

3. Explicit list of imports gives bette roverview of the code structure: what is used and where. It makes code support and refactoring easier.


### Import "as"


### Export "as"


### Export default


### Re-export


continue https://javascript.info/import-export

