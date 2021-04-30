# Chapter 5 - Inheritance

## Table of Content

- [Pseudoclassical](#pseudoclassical)
- [Object Specifiers](#object-specifiers)
- [Prototypal](#prototypal)
- [Functional](#functional)

--- 

- The benefits of classical inheritance (or extends).
  - it is a form of code reuse.
  - it includes the specification of a system of types.

- JavaScript provides a much richer set of code reuse patterns.It can ape the classical pattern, but it also supports other patterns that are more expressive

> JavaScript is a prototypal language, which means that objects inherit directly from other objects.

## Pseudoclassical

- Instead of having objects inherit directly from other objects, objects are produced by constructor functions.
- the Pseudoclassical pattern tries to mimic the classes languages by using **constructor functions**, which is against the prototypal nature of JavaScript.
- using Pseudoclassical means:
  - all properties are public.
  - If you forget to include the new prefix when calling a constructor function, then this willnot be bound to a new object. Sadly, this will be bound to the global object.

> There is no need to use it, there are better code reuse patterns in JavaScript

## Object Specifiers

- When a constructor is given a very large number of parameters. It's better to give the constructor a single object specifier instead.
  - instead of:
  
  ```js
  var myObject = maker(f, l, m, c, s);
  ```

  - we can write:
  
  ```js
  var myObject = maker({
  first: f,
  last: l,
  middle: m,
  state: s,
  city: c
  });
  ```
  
- This is useful when working with JSON, we can simply pass the JSON object to the constructor and it will return a fully constituted object.

## Prototypal

- In a purely prototypal pattern, a **new object can inherit the properties of an old object**.
- Now you can customize the new object (adding properties or methods through the dot notation for example). this is called **Differential Inheritance**

  ```js
  // the original Object
  var myMammal = {
    name: 'Herb the Mammal',
    get_name: function () {
      return this.name;
    },
    says: function () {
      return this.saying || '';
    }
  };

  // Create an instance of original object
  var myCat = Object.create(myMammal);

  // Customizing the new object
  myCat.name = 'Henrietta';
  myCat.saying = 'meow';
  myCat.purr = function (n) {
    var i, s = '';
    for (i = 0; i < n; i += 1) {
      if (s) {
        s += '-';
      }
      s += 'r';
    }
    return s;
  };
  myCat.get_name = function () {
    return this.says() + ' ' + this.name + ' ' + this.says();
  };
  ```

## Functional

- All properties of an object are visible. there is no such thing as a 'private variable'. this pattern manage us to make private variables.

- The function contains four steps:
  1. It creates a new object.
  2. It optionally defines private instance variables and methods.
  3. It augments that new object with methods.
  4. It returns that new object.

  ```js
  var constructor = function (spec, my) {
    var that, other // private instance variables;
    my = my || {};
    // Add shared variables and functions to my
    that = a new object;
    // Add privileged methods to that
    return that;
  };

  ```

- example

```js
var mammal = function (spec) {
  var that = {};
  that.get_name = function () {
    return spec.name;
  };
  that.says = function () {
    return spec.saying || '';
  };
  return that;
};
var myMammal = mammal({ name: 'Herb' });

console.log(myMammal.get_name()); // Herb
```

- The name and saying properties are now completely private. They are accessible only via the privileged get_name and says methods

- Create the Cat constructor

```js

var mammal = function (spec) {
  var that = {};
  that.get_name = function () {
    return spec.name;
  };
  that.says = function () {
    return spec.saying || '';
  };
  return that;
};
var myMammal = mammal({ name: 'Herb' });


var cat = function (spec) {

  spec.saying = spec.saying || 'meow'; //if spec.saying doesn't already exists, make it 'meow'


  var that = mammal(spec);  //here the object 'container of secrets' is set up inheriting from mammal already

  that.purr = function (n) {
    var i, s = '';
    for (i = 0; i < n; i += 1) {
      if (s) {
        s += '-';
      }
      s += 'r';
    }
    return s;
  };

  that.get_name = function () {
    return `${that.says()} ${spec.name} ${that.says()}`;
  };

  return that;
};

var myCat = cat({ name: 'Henrietta' });

console.log(myCat.get_name())
console.log(myCat.says())
```

- If we create an object in the functional style, and if all of the methods of the object make no use of this or that, then the object is durable.
- **A durable object** is simply a collection of functions that act as capabilities. that cannot be compromised by attackers.

