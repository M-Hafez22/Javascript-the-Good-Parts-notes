# Methods

## Table of Content

- [Arrays](#arrays)
- [Function](#Function)

## Arrays

- [concat](#concat)
- [join](#join)
- [pop](#pop)
- [push](#push)
- [reverse](#reverse)
- [shift](#shift)
- [unshift](#unshift)
- [slice](#slice)
- [sort](#sort)
- [splice](#splice)

### concat

- The concat method produces a *new array* containing a shallow copy of this array with the items appended to it (does not modify the original array ).

```js
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];
var c = a.concat(b, true);
// c is ['a', 'b', 'c', 'x', 'y', 'z', true]
```

### join

- Creates a string of all the array's elements, separated by the *separator*.
- The default separator is `,`.
- To join without separation use empty string as separator.

```js
var a = ['a', 'b', 'c'];
var first = a.join('')
// first is "abc"

var b = ['x', 'y', 'z'];
var second = b.join()
// second is "x,y,z"
```

### pop

- Removes and returns the last element of the array. If the array is empty, it returns undefined.

```js
var a = ['a', 'b', 'c'];
var c = a.pop( );
// a is ['a', 'b']
// c is 'c'
```

- pop can be implemented like this:

```js
Array.method('pop', function ( ) {
    return this.splice(this.length - 1, 1)[0];
});
```

### push

- The push method appends items to the end of an array.
- It modifies the array and returns the new length of the array

```js
var a =  ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];
var c =a.push(b, true);
// a is ['a', 'b', 'c', ['x', 'y', 'z'], true]  the Array
// c is 5; the new lenght
```

- push can be implemented like this:

```js
Array.method('push', function ( ) {
    this.splice.apply(
        this,
        [this.length, 0].concat(Array.prototype.slice.apply(arguments)));
    return this.length;
});
```

### reverse

- Modifies the array by reversing the order of the elements.

```js
var a = ['a', 'b', 'c'];
var b = a.reverse( );
// both a and b are ['c', 'b', 'a']
```

### shift

- Removes the first element from an array and returns it.

> shift is usually much slower than pop

```js
var a = ['a', 'b', 'c'];
var c = a.shift( );
// a is ['b', 'c'] & c is 'a'
```

- shift can be implemented like this:

```js
Array.method('shift', function ( ) {
    return this.splice(0, 1)[0];
});
```

### unshift

- The **unshift** shoves items onto the front of this array.
- It returns the array’s new length:

```js
var a = ['a', 'b', 'c'];
var r = a.unshift('?', '@');
// a is ['?', '@', 'a', 'b', 'c']
// r is 5
```

- unshift can be implemented like this:

```js
Array.method('unshift', function ( ) {
    this.splice.apply(this,
        [0, 0].concat(Array.prototype.slice.apply(arguments)));
    return this.length;
});
```

### slice

- creates a new array, copying from the *start* element and stopping at the element before the *end* value given.
- If no *end* is given, default is *array.length*.
- if negative values *array.length* will be added to them in an attempt to make them nonnegative.
- If *start* is greater than or equal to *array.length*, the result will be a new empty array.

### sort

- The sort method sorts the contents of an array in place. It **assumes that the elements are strings**. So **it sorts arrays of numbers incorrectly**. It converts the numbers to strings as it compares them.

> expected argument of Function Which compare the element and return (true or false) (+ or -)

```js
var n = [4, 8, 15, 16, 23, 42];
n.sort( );
// n is [15, 16, 23, 4, 42, 8]
```

- To fix this you can make your own:

```js
// That function will sort numbers, but it doesn’t sort strings.

n.sort((a, b) => a - b);
// n is [4, 8, 15, 16, 23, 42];
```

```js
// sort any array of simple values

var m = ['aa', 'bb', 'a', 4, 8, 15, 16, 23, 42];

m.sort(function (a, b) {
    if (a === b) {
        return 0;
    }
    if (typeof a === typeof b) {
        return a < b ? -1 : 1;
    }
    return typeof a < typeof b ? -1 : 1; // Strings > Numbers
});
// m is [4, 8, 15, 16, 23, 42, 'a', 'aa', 'bb']
```

- If case is not significant, you can lowercase before comparing them.

### splice

- The splice method removes elements from an array, replacing them with new items.
- The start parameter is the number of a **position** within the array.
- The **deleteCount** parameter is the number of elements to delete starting from that position.
- Additional parameters will be inserted at the position.
- It returns an array containing the deleted elements.

```js
// splice(position, number of Elements to be removed, addedElements...)
var a = ['a', 'b', 'c'];
var r = a.splice(1, 1, 'ache', 'bug');
// a is ['a', 'ache', 'bug', 'c']
// r is ['b']
```

---

## Function

### apply

> function.apply(thisArg, argArray)

- The apply method invokes a function, passing in *the object that will be bound to **this*** and an optional *array of arguments*.
- The apply method is used in the apply invocation pattern

---
