# Chapter 6 - Arrays

- JavaScript does not have a real array. instead, **it provides an object that has some array-like characteristics**.

- It converts array subscripts into strings that are used to make properties. It is significantly slower than a real array.

- Arrays have their own literal format and their own set of methods (Chapter 8 - Methods).

- [Array Literals](#Array-Literals)

## Array Literals

- **Array literal** is a pair of square brackets surrounding zero or more values separated by commas. `["Helo", "World"]`
- it can appear anywhere an expression can appear. 
- The first value will get the property name '0', the second value will get the property name '1', and so on:

```js
var empty = [];
var numbers = [
 'zero', 'one', 'two', 'three', 'four',
 'five', 'six', 'seven', 'eight', 'nine'
];
empty[1] // undefined
numbers[1] // 'one'
empty.length // 0
numbers.length // 10

var numbers_object = {
 '0': 'zero', '1': 'one', '2': 'two',
 '3': 'three', '4': 'four', '5': 'five',
 '6': 'six', '7': 'seven', '8': 'eight',
 '9': 'nine'
};
```

- Both *numbers* and *numbers_object* are objects containing 10 properties, and **those properties have exactly the same names and values**. But there are also significant differences.
- numbers inherits from Array.prototype, whereas numbers_object inherits from Object.prototype, **so numbers inherits a larger set of useful methods**.
- numbers gets the mysterious length property, while numbers_object does not.
- JavaScript allows an array to **contain any mixture of values**.
