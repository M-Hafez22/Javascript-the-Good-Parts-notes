
## Chapter 4 - Functions

#### Table of Content

- [Function Objects](#function-objects)
- [Function Literal](#function-literal)
- [Invocation](#invocation)

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
        -  If a function is not given a *name*, it is said to be **anonymous**.
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

-  In addition to the declared parameters, *the function receives two additional parameters*:
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
