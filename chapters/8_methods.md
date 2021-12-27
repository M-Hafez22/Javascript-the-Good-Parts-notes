# Methods

## Table of Content

- [Arrays](#arrays)
- [Function](#function)
- [Number](#number)
- [Object](#object)
- [RegExp](#regexp)
- [String](#string)

## Arrays

- [Array-concat](#array-concat)
- [join](#join)
- [pop](#pop)
- [push](#push)
- [reverse](#reverse)
- [shift](#shift)
- [unshift](#unshift)
- [slice](#slice)
- [sort](#sort)
- [splice](#splice)

### Array-concat

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

## Number

- [toExponential](#toexponential)
- [toFixed](#tofixed)
- [toPrecision](#toprecision)
- [toString](#tostring)

### toExponential

> number.toExponential(fractionDigits)

- Converts number to a string in the exponential form.
- The optional **fractionDigits** parameter controls the number of *decimal* places. It should be between 0 and 20.

```js
console.log(Math.PI.toExponential(20))
// 3.14159265358979311600e+0
```

### toFixed

> number.toFixed(fractionDigits)

- Converts number to a string in the decimal form.
- The optional **fractionDigits** parameter controls the number of *decimal* places. It should be between 0 and 20.

```js
console.log(Math.PI.toFixed(0))
// 3
```

### toPrecision

> number.toPrecision(precision)

- Converts number to a string in the decimal form.
- The optional **precision** parameter controls the number of *decimal* places. It should be between 1 and 21.

```js
console.log(Math.PI.toPrecision(2))
// 3.1
```

### toString

> number.toString(radix)

- Converts number to a string.
- The optional **radix** parameter controls radix, or base. It should be between 2 and 36. The default radix is base 10.

```js
var num = 55.55
num.toString(2)
// "110111.1000110011001100110011001100110011001100110011"
```

---

## Object

### object.hasOwnProperty(name)

- The hasOwnProperty method returns true if the object contains a property having the name.
- The prototype chain is not examined. This method is useless if the name is hasOwnProperty:

```js
var a = {member: true};
var b = Object.create(a);
var t = a.hasOwnProperty('member'); // t is true
var u = b.hasOwnProperty('member'); // u is false 
var v = b.member; // v is true
```

---

## RegExp

- [exec](#exec)
- [test](#test)

### exec

> regexp.exec(string)

- If it successfully matches the regexp and the string, it returns an array.
  - The 0 element of the array will contain the substring that matched the regexp.
  - The 1 element is the *text captured by group* 1, the 2 element is the text captured by group 2, and so on.
  - *If the match fails, it returns null*.
- If the regexp has a `g` flag, things are a little more complicated. The searching begins not at position 0 of the string, but at position **regexp.lastIndex** (which is initially zero).
  - If the match is successful, then ***regexp.lastIndex** will be set to the position of the first character after the match*.
  - An unsuccessful match resets **regexp.lastIndex** to 0.
- There are a couple things to watch out for:
  1. If you exit the loop early, you must reset regexp.lastIndex to 0 yourself before entering the loop again.
  2. the `^` factor matches only when regexp.lastIndex is 0.

> The exec method is the most powerful and slowest of the methods that use regular expressions.

### test

> regexp.test(string)

- If the regexp matches the string, it returns true; otherwise, it returns false.
- Do not use the g flag with this method

> The test method is the simplest and fastest of the methods that use regular expressions.

---

## String

- [charAt](#charat)
- [charCodeAt](#charcodeAt)
- [String-concat](#string-concat)
- [indexOf](#indexof)
- [lastIndexOf](#lastIndexof)
- [Search](#search)
- [localeCompare](#localecompare)
- [String-slice](#string-slice)
- [Split](#split)
- [Substring](#substring)
- [toLocaleLowerCase](#tolocalelowercase)
- [toLocaleUpperCase](#tolocaleuppercase)
- [toLowerCase](#tolowercase)
- [toUpperCase](#touppercase)
- [fromCharCode](#fromcharcode)

### charAt

> string.charAt(pos)

- The charAt method returns the character at position *pos* in this string.
- If *pos* is less than zero or greater than or equal to string.length, it returns the empty string.
- The result of this method is a string.

```js
var name = 'Curly';
var initial = name.charAt(0);
// initial is 'C'
```

- charAt could be implemented as:

```js
String.method('charAt', function (pos) {
return this.slice(pos, pos + 1);
});
```

### charCodeAt

> string.charCodeAt(pos)

- just like it `charAt` except it returns an integer representation of the code point value of the character at position pos in that string.

```js
var name = 'Curly';
var initial = name.charCodeAt(0);
// initial is 67
```

### String-concat

> string.concat(string...)

- It makes a new string by concatenating other strings together.

```js
var a = 'C'.concat('a', 't');   // a is 'Cat'
// You can also use + operator
var b = 'D' + 'o' + 'g'  // b is 'Dog' 
```

### indexOf

> string.indexOf(searchString, position)

- It searches for a *string* within a *string*.
- If it is found, it returns the **position of the first matched character**; otherwise, it returns **–1**.
- The optional position parameter causes the search to begin at some specified position in the string.

```js
var text = 'Mississippi';
var p = text.indexOf('ss'); // p is 2
p = text.indexOf('ss', 3); // p is 5
p = text.indexOf('ss', 6); // p is -1
```

### lastIndexOf

> string.lastIndexOf(searchString, position)

- Just like the `indexOf` method, except that it searches from the **end of the string** instead of the front.

```js
var text = 'Mississippi';
var p = text.lastIndexOf('ss'); // p is 2
p = text.lastIndexOf('ss', 3); // p is 2
p = text.lastIndexOf('ss', 6); // p is 5
```

### Search

> string.search(regexp)

- Like the `indexOf` method, except that it takes a **regular expression**
object instead of a string.
- It returns the position of the *first character* of the first match
- if the search fails it returns *–1*
- The `g` flag is ignored. There is no position parameter:

```js
var text = 'and in it he says "Any damn fool could';
var pos = text.search(/["']/);
 // pos is 18
```

### localeCompare

> string.localeCompare(that)

- The rules for how the strings are compared are not specified.
- If this string is *less than* that string, the result is *negative*. If
they are *equal*, the result is *zero*.

```js
var m = ['AAA', 'A', 'aa', 'a', 'Aa', 'aaa'];
m.sort(function (a, b) {
    return a.localeCompare(b);
});
// m (in some locale) is
// ['a', 'A', 'aa', 'Aa', 'aaa', 'AAA']
```

### match

> string.match(regexp)

- matches a string and a regular expression.
- If there is no `g` flag, then the result of calling `string.match(regexp)` is the same as calling `regexp.exec(string)`.
- if the regexp has the `g` flag, then it produces an *array of all the matches* but excludes the capturing groups.

### replace

> string.replace(searchValue, replaceValue)

- The search method is like the indexOf method, except that it takes a regular expression object instead of a string.
- It returns the *position of the first character* of the first match, or *–1* if the search fails.
- The g flag is ignored. There is no position parameter:

```js
var text = 'and in it he says "Any damn fool could';
var pos = text.search(/["']/);
// pos is 18
```

### String-slice

> string.slice(start, end)

- Creates a *new string* by copying the characters *from the start position to the character before the end position* in string.
- If the *start* parameter is negative, it adds *string.length* to it.
- The end *parameter* is optional and the default is *string.length*. If either parameter is negative, string.length is added to it.

```js
var text = 'and in it he says "Any damn fool could';
var a = text.slice(18);
// a is '"Any damn fool could'
var b = text.slice(0, 3);
// b is 'and'
var c = text.slice(-5);
// c is 'could'
var d = text.slice(19, 32);
// d is 'Any damn fool'
```

### Split

> string.split(separator, limit)

- Creates an array of strings by splitting this string into pieces.
- The optional limit parameter can limit the number of pieces that will be split.
- The separator parameter can be a string or a regular expression.

```js
var digits = '0123456789';
var a = digits.split('', 5);
// a is ['0', '1', '2', '3', '4']
```

### Substring

> string.substring(start, end)

- like the slice method except that it **doesn’t handle the
adjustment for negative parameters**.

### toLocaleLowerCase

> string.toLocaleLowerCase()

- Produces a new string by converting this string to lowercase , using the rules for the locale.

### toLocaleUpperCase

> string.toLocaleUpperCase( )

- Produces a new string by converting this string to uppercase , using the rules for the locale.

### toLowerCase

> string.toLowerCase( )

- Produces a new string by converting this string to lowercase.

### toUpperCase

> string.toUpperCase( )

- Produces a new string by converting this string to uppercase.

### fromCharCode

> String.fromCharCode(char...)

- Produces a string from a series of numbers.

```js
var a = String.fromCharCode(67, 97, 116);
// a is 'Cat'
```
