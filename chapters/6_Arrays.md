# Chapter 6 - Arrays

- JavaScript does not have a real array. instead, **it provides an object that has some array-like characteristics**.

- It converts array subscripts into strings that are used to make properties. It is significantly slower than a real array.

- Arrays have their own literal format and their own set of methods (Chapter 8 - Methods).

---

- [Array Literals](#Array-Literals)
- [Length](#Length)
- [Delete](#delete)
- [Enumeration](#enumeration)
- [Confusion](#confusion)
- [Methods](#methods)
- [Dimensions](#dimensions)
---

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

---

## Length

- **There is no array bounds error.**
  - JavaScript’s array length is not an upper bound. If you store an element with a subscript that is greater than or equal to the current length, the length will increase to contain the new element.
- The length property is the largest integer property name in the array plus one

  ```js
  var myArray = [];
  console.log(myArray.length) // 0
  myArray[1000000] = true;
  console.log(myArray.length) // 1000001
  // myArray contains one property.
  console.log(myArray[1000000]) // true
  // Other elements is undefined
  console.log(myArray[10]) // undefined
  ```

- **The length can be set explicitly**
  - Making the length larger **does not allocate more space** for the array.
  - Making the length smaller **will cause all properties with a subscript that is greater than or equal to the new length to be deleted**

  ```js
  var numbers = [ 'zero', 'one', 'two', 'three', 'four'];
  numbers.length = 3; // Making the length smaller
  console.log(numbers) // numbers is ['zero', 'one', 'two']
  ```

- A new element can be appended to the end of an array by:
  - **assigning to the array’s current length**

  ```js
  numbers[numbers.length] = 'shi';
  console.log(numbers) // numbers is ['zero', 'one', 'two', 'shi']
  ```

  - **using the push method**
  
  ```js
  numbers.push('go');
  console.log(numbers) // numbers is ['zero', 'one', 'two', 'shi', 'go']
  ```

---

## Delete

- Elements can be deleted from the array object using delete but **this leaves a hole in the array. (assign the deleted element to undefined)** This is because the elements to the right of the deleted element retain their original names.

  ```js
  var numbers = [ 'zero', 'one', 'two', 'three', 'four'];
  delete numbers[2]
  console.log(numbers); // ["zero", "one", undefined, "three", "four"]
  ```

- Use array.splice(keyInArray, howManyElementsToDelete) which changes the keys for the remaining values in the array so there is no hole left.

  ```js
  var numbers = [ 'zero', 'one', 'two', 'three', 'four'];
  numbers.splice(2, 1);
  console.log(numbers); // [ "zero", "one", "three", "four" ]
  ```

- Because every property after the deleted property must be removed and reinserted with a new key, this might be slow for large arrays.

---

## Enumeration

- the `for in` statement can be used to iterate over all of the properties of an array - Like Objects -.
- But Unfortunately, `for in` does not iterate through the properties in order and sometimes pulls in from further up the prototype chain
- To avoid these problems use `for statement`
  
  ```js
  var i;
  for (i = 0; i < myArray.length; i += 1) {
    console.log(myArray[i]);
  }
  ```

---

## Confusion

- **When to use Array**
To choose from Array or Object There is a simple rule: **when the property names are small sequential integers**, you should use an array. Otherwise, use an object.

- Javascript doesn't have a good way of telling an object from an array. `console.log(typeof([1, 2])) // object`.
- fortunately, we can make a function that detects arrays
  
  ```js
  var is_array = function (value) {
    // apply(value) binds `value` to `this` 
    // returns Array if `this` is an array
    // otherwise returns the type of the value
    return Object.prototype.toString.apply(value) === '[object Array]' ? "Array" : typeof(value) ;
  }
  console.log(is_array([1, 2])) // Array
  console.log(is_array("just a string")) // string
  ```

- The `Array.isArray()` method determines whether the passed value is an Array. `console.log(Array.isArray([1, 2, 3])) // true`
  [mozilla.org - Array.isArray()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)

---

## Methods

- The methods are functions stored in `Array.prototype`.
- Because an array is really an object, we can add methods directly to an individual array:

  ```js
  myArray.myMethod = function ( ) {
    //statements to execute; 
  };
  ```

- DO NOT USE: `Object.create()` because it will create *an object, not an array*. it will inherit the array’s values and methods, But lacking the `length` property.

---

## Dimensions

- The cells initial value is `undefined`.
- JavaScript does not have arrays of more than one dimension, but like most C languages, **it can have arrays of arrays**:

```js
var matrix = [
 [0, 1, 2],
 [3, 4, 5],
 [6, 7, 8]
];
matrix[2][1] // 7
```

---
