
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
