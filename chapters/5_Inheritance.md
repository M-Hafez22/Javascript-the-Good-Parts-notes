# Chapter 5 - Inheritance

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

