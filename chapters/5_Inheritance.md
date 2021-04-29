# Chapter 5 - Inheritance

## Table of Content

- [Pseudoclassical](#pseudoclassical)
- [Object Specifiers](#object-specifiers)
- [Prototypal](#prototypal)

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
