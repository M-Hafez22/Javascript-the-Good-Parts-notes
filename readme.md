# JavaScript: The Good Parts

#### Content

- [x]  [Chapter 1 - Good Parts](./chapters/1_Good_Parts.md)
- [x]  [Chapter 2 -  Grammar](./chapters/2_Grammar.md)
- [x]  [Chapter 3 - Objects](./chapters/3_Objects.md)
- [ ]  [Chapter 4 - Functions](./chapters/4_Functions.md)
- [ ]  Chapter 5 - Inheritance
- [ ]  Chapter 6 - Arrays
- [ ]  Chapter 7 - Regular Expressions
- [ ]  Chapter 8 - Methods
- [ ]  Chapter 9 - Style
- [ ]  Chapter 10 - Beautiful Features
- [ ]  Appendix A - the Awful Parts
- [ ]  Appendix B - the Bad Parts
- [ ]  Appendix C - JSLint


---

## Chapter 4 - Functions

- **<span style="color:#497a6d">Function Objects</span>**
    - **Functions in JavaScript are objects**. Objects are collections of name/value pairs having a hidden link to a prototype object. Objects produced from object literals are linked to Object.prototype. 
    - Function objects are linked to Function.prototype (which is itself linked to Object.prototype). 
    - Every function is also created with two additional hidden properties: 
        - the function’s context 
        - the code that implements the function’s behavior.

    - Since functions are objects, they can be used like any other value. 
        - **Functions can be stored in variables, objects, and arrays.**
        - **Functions can be passed as arguments to functions.**
        - **Functions can be returned from functions.**
        - **Functions can have methods.**
        - **Functions can be defined inside of other functions.**
    - The thing that is special about functions is that they can be **invoked**.

- **<span style="color:#497a6d">Function Literal</span>**
    ```js
        // Create a variable called add and store a function in it that adds two numbers.
        var add = function (a, b) {
        return a + b;
        };
    ```
    - A function literal has four parts:
        1. The reserved word **function**.
        2. The **function’s name** which is  *optional*.
            -  If a function is not given a name, it is said to be *anonymous*.
        3.  the set of **parameters** of the function, wrapped in parentheses.
            - These parameters will be defined as variables in the function. and will be initialized to the arguments supplied when the function is invoked.
        4. The set of statements wrapped in curly braces. These statements are the body of the function. They are executed when the function is invoked.
    - **closure**
        - An inner function has access to its parameters and variables.and also enjoys access to the parameters and variables of the functions it is nested within. The function object created by a function literal contains a link to that outer context. This is called closure.


- **<span style="color:#497a6d">Invocation</span>**

    - When invoking the function receives two additional parameters:
        1. **this**
            - The this parameter is very important in object oriented programming, and its value is determined by the invocation pattern.The patterns differ in how the bonus parameter this is initialized.
            - *There are four patterns of invocation in JavaScript*: 
                1. the method invocation pattern
                2. the function invocation pattern
                3. the constructor invocation pattern
                4. the apply invocation pattern. 
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
    
    
    - **The Method Invocation Pattern**
        When a function is stored as a property of an object, we call it a method. When a method is invoked, this is bound to that object. If an invocation expression contains a refinement (that is, a . dot expression or [subscript] expression), it is invoked as a method:

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
            document.writeln(myObject.value); // 1

            myObject.increment(2);
            document.writeln(myObject.value); // 3
        ```
    - A method can use **this** to access the object so that it can retrieve values from the object or modify the object. The binding of **this** to the object happens at invocation time. This very late binding makes functions that use **this** highly reusable. Methods that get their object context from **this** are called *public methods*.
