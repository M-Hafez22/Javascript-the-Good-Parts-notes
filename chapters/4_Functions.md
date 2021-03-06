
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
- [Scope](#scope)
- [Closure](#closure)
- [Callbacks](#callbacks)
- [Cascade](#cascade)
- [Curry](#curry)

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

## Scope

- Scope in a programming language controls the visibility and lifetimes of variables and parameters.
- This is an important service to the programmer because it reduces naming collisions and provides automatic memory management:

```js
var foo = function ( ) {
 var a = 3, b = 5;
 console.log({a, b})
 var bar = function ( ) {
 var b = 7, c = 11;
 console.log({b, c})
// At this point, a is 3, b is 7, and c is 11
 a += b + c;
// At this point, a is 21, b is 7, and c is 11
 console.log({a, b, c})
 };
// At this point, a is 3, b is 5, and c is not defined
 console.log({a, b})
 console.log({c})
 bar( );
// At this point, a is 21, b is 5
 console.log({a, b})
 console.log({c})
};
foo();
```

> Most languages with **C** syntax have block scope. All variables defined in a block (a list of statements wrapped with curly braces) are not visible from outside of the block. The variables defined in a block can be released when execution of the block is finished. This is a good thing

- Unfortunately, JavaScript does not have block scope even though its block syntax suggests that it does. This confusion can be a source of errors.

- JavaScript does have **function scope*: 
That means that the **parameters and variables defined in a function are not visible outside of the function**, and that a **variable defined anywhere within a function is visible everywhere within the function**.

- because of the lack of block scope. it is best to **declare all of the variables used in a function at the top of the function body**.

## Closure

- The good news about scope is that **inner functions get access to the parameters and variables of the functions they are defined within (with the exception of this and arguments)**.

- we will initialize myObject by calling a function that returns an object literal. That function defines a value variable. That variable is always available to the increment and getValue methods, but the function’s scope keeps it hidden from the rest of the program (the outer functions):

  ```js
  var myObject = (function ( ) {
    var value = 0;
    return {
      increment: function (inc) {
        value += typeof inc === 'number' ? inc : 1;
      },
      getValue: function ( ) {
        return value;
      }
    };
  }( ));
  ```

> We are not assigning a function to myObject. **We are assigning the result of invoking that function**.

- The function returns an object containing two methods, and those methods continue to enjoy the privilege of access to the value variable.

- Other Example

```js
  // Create a maker function called quo. It makes an
  // object with a get_status method and a private
  // status property.
  var quo = function (status) {
    return {
      get_status: function ( ) {
        return status;
      }
    };
  };
  // Make an instance of quo.
  var myQuo = quo("amazed");
  console.log(myQuo.get_status( ));
```

- This *quo* function is designed to be used without the new prefix, so the name is not capitalized.
- When we call quo, it returns a new object containing a *get_status* method.
- A reference to that object is stored in myQuo.
- The *get_status* method still has privileged access to quo’s status property even though quo has already returned.
- *get_status* **does not have access to a copy of the parameter; it has access to the parameter itself**. This is possible because the function has access to the context in which it was created. This is called closure.

```js
// Define a function that sets a DOM node's color
// to yellow and then fades it to white.
var fade = function (node) {
  var level = 1;
  var step = function () {
    var hex = level.toString(16);
    node.style.backgroundColor = '#FFFF' + hex + hex;
    if (level < 15) {
      level += 1;
      setTimeout(step, 100);
    }
  };
  setTimeout(step, 100);
};
fade(document.body);
```

- We call fade, passing it document.body (the node created by the HTML \<body> tag).
- fade sets level to 1. It defines a step function. It calls setTimeout, passing it the step function and a time (100 milliseconds).
- It then returns—fade has finished.
- Suddenly, about a 10th of a second later, the step function gets invoked. It makes a base 16 character from fade’s level.
- It then modifies the background color of fade’s node.
- It then looks at fade’s level. If it hasn’t gotten to white yet, it then increments fade’s level and uses setTimeout to schedule itself to run again.
- Suddenly, the step function gets invoked again. But this time, fade’s level is 2.
- fade returned a while ago, but its variables continue to live as long as they are needed by one or more of fade’s inner functions.

> It is important to understand that the inner function has access to the actual variables of the outer functions and not copies in order to avoid the following problem.

```js
// BAD EXAMPLE
// Make a function that assigns event handler functions to an array of nodes the wrong way.
// When you click on a node, an alert box is supposed to display the ordinal of the node.
// But it always displays the number of nodes instead.
var add_the_handlers = function (nodes) {
  var i;
  for (i = 0; i < nodes.length; i += 1) {
    nodes[i].onclick = function (e) {
      alert(i);
    };
  }
};
// END BAD EXAMPLE

```

- The add_the_handlers function was intended to give each handler a unique number i. It fails because the handler functions are bound to the variable i, not the value of the variable i at the time the function was made.

## Callbacks

- When dealing with server requests it's better to make an asynchronous request, providing a callback function that will be invoked when the server’s response is received. An asynchronous function returns immediately, so the client isn’t blocked:

  ```js
  request = prepare_the_request( );
    send_request_asynchronously(request, function (response) {
    display(response);
  });
  ```

  - We pass a function parameter to the send_request_asynchronously function that will be called when the response is available.

## Module

- A module is a function or object that presents an interface but that hides its state and implementation.
- By using functions to produce modules, we can almost completely eliminate our use of global variables, thereby mitigating one of JavaScript’s worst features.

- For example, suppose we want to augment String with a deentityify method. Its job is to look for HTML entities in a string and replace them with their equivalents. It makes sense to keep the names of the entities and their equivalents in an object. But where should we keep the object? We could put it in a global variable, but global variables are evil. We could define it in the function itself, but that has a runtime cost because the literal must be evaluated every time the function is invoked. The ideal approach is to put it in a closure, and perhaps provide an extra method that can add additional entities:

```js
Function.prototype.method = function (name, func) {
  this.prototype[name] = func;
  return this;
};

String.method('deentityify', function () {
  // The entity table. It maps entity names to
  // characters.
  var entity = {
    quot: '"',
    lt: '<',
    gt: '>'
  };
  // Return the deentityify method.
  return function () {
    // This is the deentityify method. It calls the string
    // replace method, looking for substrings that start
    // with '&' and end with ';'. If the characters in
    // between are in the entity table, then replace the
    // entity with the character from the table. It uses
    // a regular expression (Chapter 7).
    return this.replace(/&([^&;]+);/g,
      function (a, b) {
        var r = entity[b];
        return typeof r === 'string' ? r : a;
      }
    );
  };
}());

console.log('&lt;&quot;&gt;'.deentityify()); // <">
```

- It can also be used to produce objects that are secure. Let’s suppose we want to make an object that produces a serial number:

  ```js
  var serial_maker = function () {
    // Produce an object that produces unique strings. A
    // unique string is made up of two parts: a prefix
    // and a sequence number. The object comes with
    // methods for setting the prefix and sequence
    // number, and a gensym method that produces unique
    // strings.
    var prefix = '';
    var seq = 0;
    return {
      set_prefix: function (p) {
        prefix = String(p);
      },
      set_seq: function (s) {
        seq = s;
      },
      gensym: function () {
        var result = prefix + seq;
        seq += 1;
        return result;
      }
    };
  };
  var seqer = serial_maker();
  seqer.set_prefix('Q');
  seqer.set_seq(1000);
  var unique = seqer.gensym(); // unique is "Q1000"
  console.log(unique)
  ```

  - The methods do not make use of this or that. As a result, there is no way to compromise the seqer. It isn’t possible to get or change the prefix or seq except as permitted by the methods. The seqer object is mutable, so the methods could be replaced, but that still does not give access to its secrets. seqer is simply a collection of functions, and those functions are capabilities that grant specific powers to use or modify the secret state.
  - If we passed seqer.gensym to a third party’s function, that function would be able to generate unique strings, but would be unable to change the prefix or seq.

## Cascade

- Some methods do not have a return value. For example, it is typical for methods that set or change the state of an object to return nothing. If we have those methods return this instead of undefined, we can enable cascades.
- In a cascade, we can call many methods on the same object in sequence in a single statement.

- An Ajax library
that enables cascades would allow us to write in a style like this:

  ```js
  getElement('myBoxDiv')
    .move(350, 150)
    .width(100)
    .height(100)
    .color('red')
    .border('10px outset')
    .padding('4px')
    .appendText("Please stand by")
    .on('mousedown', function (m) {
      this.startDrag(m, this.getNinth(m));
    })
    .on('mousemove', 'drag')
    .on('mouseup', 'stopDrag')
    .later(2000, function () {
      this
        .color('yellow')
        .setHTML("What hath God wraught?")
        .slide(400, 40, 200, 200);
    })
    .tip("This box is resizeable.");
  ```

  - In this example, the getElement function produces an object that gives functionality to the DOM element with id="myBoxDiv".
  - The methods allow us to move the element, change its dimensions and styling, and add behavior.
  - Each of those methods returns the object, so the result of the invocation can be used for the next invocation.
- Cascading can produce interfaces that are very expressive. It can help control the tendency to make interfaces that try to do too much at once.

## Curry

- **Currying** allows us to produce a new function by combining a function and an argument.
- The curry method works by creating a closure that holds that original function and the arguments to curry. It returns a function that, when invoked, returns the result of calling that original function, passing it all of the arguments from the invocation of curry and the current invocation. It uses the Array concat method to concatenate the two arrays of arguments together

> [Currying - Part 6 of Functional Programming in JavaScript](https://www.youtube.com/watch?v=iZLP4qOwY8I&t)

## Memoization

- In JavaScript we can use objects and arrays to remember the results of previous operations - without having to keep recalculating the it -.

- Particularly useful when a function is recursive and uses the results of its previous iteration in the current iteration.

>[Memoization And Dynamic Programming Explained](https://www.youtube.com/watch?v=WbwP4w6TpCk)

```js
// Return the fibonacci number by it's index
function fib(index, cache = [0, 1, 1]) {
  // Check if the number has been calculated
    if (cache[index]) {
        return cache[index];
    }
  // Adds Fibonacci number
    cache[index] = fib(index - 1, cache) + fib(index - 2, cache);
    console.log(index);
    return cache[index];
}

console.log(fib());
```
