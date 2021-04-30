# Chapter 6 - Arrays

- JavaScript does not have a real array. instead, **it provides an object that has some array-like characteristics**.

- It converts array subscripts into strings that are used to make properties. It is significantly slower than a real array.

- Arrays have their own literal format and their own set of methods (Chapter 8 - Methods).

- [Array Literals](#Array-Literals)
- [Length](#Length)
- [Delete](#delete)

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
