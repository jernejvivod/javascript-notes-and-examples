# Inheritance and the Prototype Chain

JavaScript is dynamic and does not have static types.

When it comes to inheritance, JavaScript only has one construct: objects.

Each object has a private property which holds a link to another object
called its prototype. That prototype object has a prototype of its own, and
so onl until an object is reached with null as its prototype.

By definition, `null` has no prototype and acts as the final link in this
prototype chain.

It is possible to mutate any member of the prototype chain or even swap
out the prototype at runtime, so concepts like static dispatching do not
exist in JavaScript.


There are several ways to specify the `[[Prototype]]` of the object.

In an object literal like `{ a: 1, b: 2, __proto__: c }`, the value `c`
which has to be either null or another object, will become the `[[prototype]]` of the object represented by the literal, while the other keys like
`a` and `b` will become the own properties of the object.

## Inheriting "methods"

JavaScript does not have methods in the form that class-based languages
define them. In JavaScript, any function can be added to an object in the
form of a property. An inherited function acts just as any other property,
including property shadowing as shown above (in this case, a form of method
overriding).

When an inherited function is executed, the value of `this` points to the
inheriting object, not to the prototype object where the function
is an own property.

## Constructors

The power of prototypes is that we can reuse a set of properties if they
should be present on every instance, especially for methods.

Example:

```
// A constructor function
function Box(value) {
    this.value = value;
}

// Properties all boxes created from the Box() constructor
// will have
Box.prototype.getValue = function () {
    return this.value;
};

const boxes = [
    new Box(1),
    new Box(2),
    new Box(3),
];
```

We say that `new Box(1)` is an instance created from the `Box` constructor
function. `Box.prototype` is just a plain object. Every instance created
from a constructor function will automatically have the constructor's
prototype property as its `[[Prototype]]`.

`Constructor.prototype` by default has one own property `constructor` which
references the constructor function itself: `Box.prototype.constructor === Box`.

Note: if a non-primitive is returned from the constructor function, that
value will become the result of the `new` expression. In this case the
`[[Prototype]]` may not be correctly bound.


The above constructor function can be rewritten in classes as:

```
class Box {
    constructor(value) {
        this.value = value;
    }

    // methods are created on Box.prototype
    getValue() {
        return this.value;
    }
}
```


Classes are syntactic sugar over constructor fuctions, which means you can
still manipulate `Box.prototype` to change the behavior of all instances.

Because `Box.prototype` references the same object as the `[[Prototype]]`
of all instances, we can change the behavior of all instances by mutating
`Box.prototype`.

```
function Box(value) {
  this.value = value;
}
Box.prototype.getValue = function () {
  return this.value;
};
const box = new Box(1);

// Mutate Box.prototype after an instance has already been created
Box.prototype.getValue = function () {
  return this.value + 1;
};

box.getValue(); // 2
```

## Inspecting Protoypes: a Deepr Dive

In JavaScript, as mentioned ove, functions are able to hav poperties. All functios have a specal poperty named `prototype`. 

```
function doSomething() {}
console.log(doSomething.prototype);

const doSomethingFromArrowFunctio = () => {};
console.log(doSomehingFromArrowFunction.protoype);
```

A function in JavaScript will always have a default prototype property with one exception: an arrow function doesn't have
a default prototype property.


We can add properties to the prototype of `doSomething()` as shown below.

```
function doSomething() {}
doSomething.prototype.foo = 'bar';
console.log(doSomething.prototype);
```




we can now use the `new` operator to creat an instance of `doSomething()` based on this prototype. To use the new operator, call the function normally except prefix it with
`new`. Calling a function with the `new` operator returns an object that is an instance of the function. Properties can then be added onto this object.


## Different Ways of Creating and Mutating Prototype Chains

We have encountered many ways to create objects and change their prototype chains. We will systematically summarize the different ways, comparing each approach's pros and cons.

### Objects Created with Syntax Constructs

```
const o = { a: 1 };
// The newly created object o has Object.prototype as its [[Prototype]]
// Object.prototype has null as its prototype.
// o ---> Object.prototype ---> null

const b = ['yo', 'whadup', '?'];
// Arrays inherit from Array.prototype
// (which has methods indexOf, forEach, etc.)
// The prototype chain looks like:
// b ---> Array.prototype ---> Object.prototype ---> null

function f() {
  return 2;
}
// Functions inherit from Function.prototype
// (which has methods call, bind, etc.)
// f ---> Function.prototype ---> Object.prototype ---> null

const p = { b: 2, __proto__: o };
// It is possible to point the newly created object's [[Prototype]] to
// another object via the __proto__ literal property. (Not to be confused
// with Object.prototype.__proto__ accessors)
// p ---> o ---> Object.prototype ---> null
```

### Objects Created with Constructor Functions

```
function Graph() {
  this.vertices = [];
  this.edges = [];
}

Graph.prototype.addVertex = function (v) {
  this.vertices.push(v);
}

const g = new Graph();
// g is an object with own properties 'vertices' and 'edges'.
// g.[[Prototype]] is the value of Graph.prototype when new Graph() is executed.
```

### Objects Created with Object.create()

```
const a = { a: 1 };
// a ---> Object.prototype ---> null

const b = Object.create(a);
// b ---> a ---> Object.prototype ---> null
console.log(b.a); // 1 (inherited)

const c = Object.create(b);
// c ---> b ---> a ---> Object.prototype ---> null

const d = Object.create(null);
// d ---> null (d is an object that has null directly as its prototype)
console.log(d.hasOwnProperty);
// undefined, because d doesn't inherit from Object.prototype
```

### Objects created with Classes

```
class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

class Square extends Polygon {
  constructor(sideLength) {
    super(sideLength, sideLength);
  }

  get area() {
    return this.height * this.width;
  }

  set sideLength(newLength) {
    this.height = newLength;
    this.width = newLength;
  }
}

const square = new Square(2);
// square ---> Square.prototype ---> Polygon.prototype ---> Object.prototype ---> null
```

### Objects Created with Object.setPrototypeOf()

While all methods above will set the prototype chain at object creation time, `Object.setPrototypeOf()` allows mutating the `[[Prototype]]` internal property of an existing object.

```
const obj = { a: 1 };
const anotherObj = { b: 2 };
Object.setPrototypeOf(obj, anotherObj);
// obj --> anotherObj --> Object.prototype --> null
```

### Objects Created with the `__proto__` accessor

All objects inherit the `Object.prototype.__proto__` setter, which can be used to set the `[[Prototype]]` of an existing object (if the `__proto__` key is not overriden on the object).

`Object.prototype.__proto__` accessors are non-standard and deprecated. You should almost always use `Object.setPrototypeOf`.

```
const obj = {};
// DON'T USE THIS: for example only.
obj.__proto__ = { barProp: 'bar val' };
obj.__proto__.__proto__ = { fooProp: 'foo val' };
console.log(obj.fooProp);
console.log(obj.barProp);
```



