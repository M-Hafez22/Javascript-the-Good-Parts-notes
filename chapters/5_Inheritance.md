# Chapter 5 - Inheritance

## Table of Content

- [Pseudoclassical](#pseudoclassical)
- [Object Specifiers](#object-specifiers)

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
