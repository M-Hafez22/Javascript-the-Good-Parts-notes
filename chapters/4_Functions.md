
# Chapter 4 - Functions

## Table of Content

- [Function Objects](#function-objects)
- [Function Literal](#function-literal)
- [Invocation](#invocation)
- [Arguments](#arguments)
- [Return](#return)
- [Exceptions](#exceptions)
- [Augmenting Types](#augmenting-types)
- [Recursion](#recursion)

---

> **Functions are the fundamental modular unit of JavaScript**. It encloses a set of statements. Functions are used for *code reuse*, *information hiding*, *composition*, and specify the behavior of objects. Generally.

---

## Function Objects

- **Functions in JavaScript are objects**.
- Function objects are linked to Function.prototype (which is itself linked to Object.prototype).
- Every function is also created with two additional hidden properties:
  - The function’s *context*
  - The *code* that implements the function’s behavior.

- Since functions are objects, they can be used like any other value:
  - **Functions can be stored in variables, objects, and arrays.**
  - **Functions can be passed as arguments to functions.**
  - **Functions can be returned from functions.**
  - **Functions can have methods.**
  - **Functions can be defined inside of other functions.**
- The thing that is special about functions is that they can be **invoked**.

---

## Function Literal

- Function objects are created with function literals:

```js
    // Create a variable called add and store a function in it that adds two numbers.
    var add = function (a, b) {
        return a + b;
    };
```

- A function literal has four parts:
  1. The reserved word **function**.
  2. The **function’s name** which is  *optional*.
      - If a function is not given a *name*, it is said to be **anonymous**.
      - The function can use its name to **call itself recursively**.
      - The name can be used by debuggers and development tools to **identify the function**.
  3. The **Parameters**:
      - They are wrapped in parentheses separated by commas **(.. , ..)**.
      - These names will be defined as variables in the function. and will be initialized to the arguments supplied when the function is invoked.
  4. The **statements**:
      - The set of statements wrapped in curly braces **{ }** .
      - These statements are *the body of the function*. and They are *executed when the function is invoked*.

> A function literal can appear anywhere that an expression can appear

- **closure**
  - As functions can be defined inside of other functions. the inner function has access to its parameters and variables. and also enjoys **access to the parameters and variables of the functions it is nested within**. The function object created by a function literal contains a link to that outer context. *This is called closure*.

---

## Invocation

> **Invoking a function suspends the execution of the current function, passing control and parameters to the new function**.

```js
    add(5, 7)
```

- In addition to the declared parameters, *the function receives two additional parameters*:
    1. **this**
        - The this parameter is very important in object oriented programming, and **its value is determined by the invocation pattern**.The patterns differ in how the bonus parameter ***this*** is initialized.
    2. **arguments**
        - the arguments passed in the invocation parentheses separated by commas.
        - Each expression produces one argument value. Each of the argument values will be assigned to the function’s parameter names.
        - there is no run time error if the number of arguments don't match the number of the parameters  

            ```js
                if (argument > parameters) {
                    // the extra argument values will be ignored.
                }else if (argument < parameters) {
                    // the missing parameters will be assigned to undefined
                }
            ```

        - There is no type checking on the argument values: any type of value can be passed to any parameter.

- **The Invocation patterns** in JavaScript are:
    1. The **method** invocation pattern
    2. The **function** invocation pattern
    3. The **constructor** invocation pattern
    4. The **apply** invocation pattern.

1. **The Method Invocation Pattern**
    When a function is stored as a property of an object, we call it a method. 
    When a method is invoked, ***this*** is bound to that object. If an invocation expression contains a refinement (that is, a . dot expression or [subscript] expression), it is invoked as a method:

    ```js
        // Create myObject. It has a value and an increment
        // method. The increment method takes an optional
        // parameter. If the argument is not a number, then 1
        // is used as the default.

        var myObject = {
            value: 0,
            increment: function (inc) {
                this.value += typeof inc === 'number' ? inc : 1;
            }
        };

        myObject.increment( );
        console.log(myObject.value); // 1

        myObject.increment(2);
        console.log(myObject.value); // 3
    ```

    - A method can use **this** to access the object so that it can retrieve values from the object or modify the object. The binding of **this** to the object happens at invocation time. This very late binding makes functions that use **this** highly reusable. Methods that get their object context from **this** are called *public methods*.

2. **The Function Invocation Pattern**

    - When a function is not the property of an object, then it is invoked as a function:

    ```js
    var sum = add(3, 4);  // sum is 7
    ```

    - When a function is invoked with this pattern, ***this*** is bound to the **global object**.
    - When the inner function is invoked, ***this*** would still be bound to the this variable of the outer function.
    - A consequence of this bound way is that a method cannot employ an inner function to help it do its work because **the inner function does not share the method’s access to the object as its *this* is bound to the wrong value**.
    - An easy workaround. If the method defines a variable and assigns it the value of ***this***, the inner function will have access to ***this*** through that variable. By convention, the name of that variable is ***that***:

        ```js
        // Augment myObject with a double method.
        myObject.double = function ( ) {
            var that = this; // Workaround.

            var helper = function ( ) {
                that.value = add(that.value, that.value);
            };

            helper( ); // Invoke helper as a function.
        };
        // Invoke double as a method.
        myObject.double( );
        document.writeln(myObject.value); //6
        ```

3. **The Constructor Invocation Pattern**

    - JavaScript is a **prototypal inheritance language**. That means that *objects can inherit properties directly from other objects*. The language is class-free.
    - JavaScript itself is not confident in its prototypal nature, so it offers an *object-making syntax that is reminiscent of the classical languages*.

    > The classically inspired syntax obscures the language’s true prototypal nature. It is the worst of both worlds.

    - If a function is invoked with the ***new*** prefix:
      - a new object will be created with a hidden link to the value of the function’s prototype member, and ***this*** will be bound to that new object.
      - The ***new*** prefix also changes the behavior of the return statement.

    ```js
    // Create a constructor function called Quo.
    // It makes an object with a status property.

    var Quo = function (string) {
        this.status = string;
    };

    // Give all instances of Quo a public method called get_status.
    Quo.prototype.get_status = function ( ) {
        return this.status;
    };

    // Make an instance of Quo.

    var myQuo = new Quo("confused");
    console.log(myQuo.get_status( ));   // confused
    ```

    - Functions that are intended to be used with the new prefix are called constructors. By convention, they are kept in variables with a capitalized name. If a constructor is called without the new prefix, very bad things can happen without a compile-time or runtime warning, so the capitalization convention is really important.

    >Use of this style of constructor functions is not recommended. We will see better alternatives in the next chapter.

4. **The Apply Invocation Pattern**

    - Because JavaScript is a functional object-oriented language, functions can have methods.
    - The ***apply*** method lets us construct an array of arguments to use to invoke a function.
    - It also lets us choose the value of ***this***.
    - The ***apply*** method takes two parameters.
      - The first is the value that should be bound to ***this***.
      - The second is an *array of parameters*.

    ```js
    // Make an array of 2 numbers and add them.
    var array = [3, 4];
    var sum = add.apply(null, array); // sum is 7

    // Make an object with a status member.
    var statusObject = {
    status: 'A-OK'
    };
    // statusObject does not inherit from Quo.prototype,
    // but we can invoke the get_status method on
    // statusObject even though statusObject does not have
    // a get_status method.
    var status = Quo.prototype.get_status.apply(statusObject); // status is 'A-OK'
    ```

---

## Arguments

- A bonus parameter that is available to functions when they are invoked is the arguments array.
- It gives the function access to all of the arguments that were supplied with the invocation, including excess *arguments that were not assigned to parameters*. This makes *it possible to write functions that take an unspecified number of parameters*:

```js
// Make a function that adds a lot of stuff.
// Note that defining the variable sum inside of the function does not interfere with the sum defined outside of the function. 
// The function only sees the inner one.
var sum = function ( ) {
    var i, sum = 0;

    for (i = 0; i < arguments.length; i += 1) {
        sum += arguments[i];
    }
    return sum;
};
console.log(sum(4, 8, 15, 16, 23, 42)); // 108

```

```js
/**
 * Sorted Union
 * 
 * Write a function that takes two or more arrays and returns a new array of unique values in the order of the original provided arrays.
 * 
 * In other words, all values present from all arrays should be included in their original order, but with no duplicates in the final array.
 * 
 * The unique numbers should be sorted by their original order, but the final array should not be sorted in numerical order.
 */


function uniteUnique(arr) {
    let unionArrays = [];
    for (let i = 0; i <  arguments.length; i++){
        unionArrays = unionArrays.concat(arguments[i])
    }
    unionArrays = new Set(unionArrays)
    const arrayWithNoDuplicates = [...unionArrays]
    return arrayWithNoDuplicates;
}

console.log(uniteUnique([1, 3, 2], [5, 2, 1, 4], [2, 1]));
```

- Because of a design error, arguments is not really an array. It is an array-like object. arguments has a length property, but it lacks all of the array methods.

---

## Return

- When a function is invoked, it begins execution with the first statement, and ends when it hits the **}** that closes the function body. That causes the function to return control to the part of the program that invoked the function.

- The **return** statement can be used to cause the function to return early. When **return** is executed, the function returns immediately without executing the remaining statements.

- A function always returns a value. If the return value is not specified, then *undefined* is returned.
- If the function was invoked with the ***new*** prefix and the return value is not an object, then ***this*** (the new object) is returned instead.

---

## Exceptions

- JavaScript provides an exception handling mechanism. Exceptions are unusual (but not completely unexpected) mishaps that interfere with the normal flow of a program. When such a mishap is detected, your program should throw an exception:

    ```js
    var add = function (a, b) {
        if (typeof a !== 'number' || typeof b !== 'number') {
            throw {
                name: 'TypeError',
                message: 'add needs numbers'
            };
        }
        return a + b;
    }
    ```

  - The throw statement interrupts execution of the function. It should be given an exception object containing a name property that identifies the type of the exception, and a descriptive message property. You can also add other properties.

- The exception object will be delivered to the catch clause of a try statement:

    ```js
    // Make a try_it function that calls the new add
    // function incorrectly.
    var try_it = function ( ) {
        try {
            add("seven");
        } catch (e) {
            console.log(e.name + ': ' + e.message);
        }
    }
    try_it( );
    ```

  - If an exception is thrown within a try block, control will go to its catch clause.
  - A try statement has a single catch block that will catch all exceptions. If your handling depends on the type of the exception, then the exception handler will have to inspect the name to determine the type of the exception.

---

## Augmenting Types

JavaScript allows the basic types of the language to be augmented. In Chapter 3, we saw that adding a method to Object.prototype makes that method available to all objects. This also works for functions, arrays, strings, numbers, regular expressions, and booleans.

- For example, by augmenting Function.prototype, we can make a method available to
all functions:

  ```js
  Function.prototype.method = function (name, func) {
  this.prototype[name] = func;
  return this;
  };
  ```

  - Now we no longer have to type the name of the prototype property. That bit of ugliness can now be hidden.

  - Return the closest integers

  ```js
  Number.method('integer', function ( ) {
  return Math[this < 0 ? 'ceil' : 'floor'](this);
  });
  console.log((-10 / 3).integer( )); // -3
  ```

  - Removes spaces from the ends of a string

  ```js
  String.method('trim', function ( ) {
  return this.replace(/^\s+|\s+$/g, '');
  });
  console.log('"' + " neat ".trim( ) + '"');
  ```

- By augmenting the basic types, we can make significant improvements to the expressiveness of the language. Because of the dynamic nature of JavaScript’s prototypal inheritance, all values are immediately endowed with the new methods, even values that were created before the methods were created.

> The prototypes of the basic types are public structures, so care must be taken when mixing libraries. One defensive technique is to add a method only if the method is known to be missing:
  
  ```js
  // Add a method conditionally.
  Function.prototype.method = function (name, func) {
    if (!this.prototype[name]) {
      this.prototype[name] = func;
      return this;
  }
  };
  ```

> Another concern is that the for in statement interacts badly with prototypes. We saw a couple of ways to mitigate that in Chapter 3: we can use the hasOwnProperty method to screen out inherited properties, and we can look for specific types.

## Recursion

- A recursive function is a function that calls itself, either directly or indirectly. Recursion is a powerful programming technique in which a problem is divided into a set of similar subproblems, each solved with a trivial solution. Generally, a recursive function calls itself to solve its subproblems.

```js
var hanoi = function hanoi(disc, src, aux, dst) {
 if (disc > 0) {
    hanoi(disc - 1, src, dst, aux);
    console.log('Move disc ' + disc +
    ' from ' + src + ' to ' + dst);
    hanoi(disc - 1, aux, src, dst);
 }
};
hanoi(3, 'Src', 'Aux', 'Dst');
```

[Recursion in software development](https://www.youtube.com/watch?v=vPEJSJMg4jY)

- Some languages offer the tail recursion optimization. This means that if a function returns the result of invoking itself recursively, then the invocation is replaced with a loop, which can significantly speed things up. Unfortunately, JavaScript does not currently provide tail recursion optimization. Functions that recurse very deeply can fail by exhausting the return stack:

  ```js
  // Make a factorial function with tail
  // recursion. It is tail recursive because
  // it returns the result of calling itself.
  // JavaScript does not currently optimize this form.
  var factorial = function factorial(i, a) {
  a = a || 1;
  if (i < 2) {
    return a;
  }
  return factorial(i - 1, a * i);
  };
  console.log(factorial(4)); // 24
  ```
