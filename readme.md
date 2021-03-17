# JavaScript: The Good Parts

#### Content

- [x]  [Chapter 1 - Good Parts](#chapter-1-good-parts)
- [x]  [Chapter 2 -  Grammar](#chapter-2-grammar)
- [x]  [Chapter 3 - Objects](#chapter-3-objects)
- [ ]  [Chapter 4 - Functions](#chapter-4-functions)
- [ ]  Chapter 5 - Inheritance
- [ ]  Chapter 6 - Arrays
- [ ]  Chapter 7 - Regular Expressions
- [ ]  Chapter 8 - Methods
- [ ]  Chapter 9 - Style
- [ ]  Chapter 10 - Beautiful Features
- [ ]  Appendix A - the Awful Parts
- [ ]  Appendix B - the Bad Parts
- [ ]  Appendix C - JSLint


## Chapter 1 - Good Parts

- Why JavaScript?
    - The reasons that make it a despised programming language for some Developers are:
        - the  poorly specified and inconsistently implemented in the *DOM*.
        - Some developers - who forced to work with JS - *didn't put effort to learn the differences*.

- Analyzing JavaScript
    - JavaScript is built on some very good ideas and a few very bad ones.
        - <span style="color:green">The very good ideas</span> include
            - <span style="color:orange">functions</span> : JavaScript’s functions are first class objects with (mostly) lexical scoping.
            - <span style="color:orange">loose typing</span>
            - <span style="color:orange">dynamic objects</span>:  JavaScript has a very powerful object literal notation. Objects can be created simply by listing their components. This notation was the inspiration for JSON
            - <span style="color:orange">JavaScript is prototypal inheritance</span>.  ( objects inherit properties directly from other objects ) But you have to learn to work with JavaScript’s prototypal nature.

        - <span style="color:red">The bad ideas</span> include a programming model based on global variables.
            - <span style="color:orange">global variables</span>: All of the top-level variables of all compilation units are tossed together in a common namespace called the global object.


        > JavaScript is lightweight and expressive.

	---
## Chapter 2 - Grammar

- <span style="color:green">Whitespace</span>

    ```js
    var first = 'First';
    var second ='Second';
    ```

    - the space between ***var** and **variable name** cannot be removed*, but the other spaces can be removed

- <span style="color:green">Comments</span>
    - single line comment formed with <span style="color:orange">//</span> 
        ```js
        // 
        ```
    - block comments formed with <span style="color:orange">/* */</span>, But this type may cause problems like this:

        ```js
        /*
            var rm_a = /a*/.match(s);
        */
        ```
    - JSDoc 
        ```js
        /**
        * Function return a name.
        *
        * @param {string} n - A string param
        * @return {string} A good string
        */

        function foo(n) {
            return n
        }
        ```
- <span style="color:green">Names</span>
    - A name is a letter optionally followed by one or more letters, digits, or underbars. A name cannot be one of these reserved words:
        - abstract
        - boolean break byte
        - case catch char class const continue
        - debugger default delete do double
        - else enum export extends
        - false final finally float for function
        - goto
        - if implements import in instanceof int interface
        - long
        - native new null
        - package private protected public
        - return
        - short static super switch synchronized
        - this throw throws transient true try typeof
        - var volatile void
        - while with
    - Names are used for statements, variables, parameters, property names, operators, and labels.
- <span style="color:green">Numbers</span>
    - JavaScript has a single number type. Internally, it is represented as 64-bit floating point, the same as Java’s double. 
    - there is **no separate integer type**, so 1 and 1.0 are the same value. so problems of overflow in short integers are completely avoided.
    - **Negative numbers** can be formed by using the <span style="color:orange">–</span> prefix operator.
    - The value  <span style="color:orange">NaN</span> is a number value that is the result of an operation that cannot produce a normal result. 
        - NaN is not equal to any value, including itself. 
            ```js 
                console.log(NaN === NaN); // false
            ```
        - You can detect NaN with the `isNaN(number)` function.
    - If a number literal has an exponent part, then the value of the literal is computed by
     multiplying the part before the <span style="color:orange">e</span> by 10 raised to the power of the part after the <span style="color:orange">e</span>. So:

        ```js
            console.log(5e2 === 500);  // true
        ```


- <span style="color:green">Strings</span>
    - A string literal can be wrapped in single quotes <span style="color:orange">' '</span>  or double quotes <span style="color:orange">" "</span> .
    - all characters in JavaScript are 16 bits wide.
    - JavaScript does not have a character type. To represent a character, make a string with just one character in it.
    - The <span style="color:orange"> \ </span> (backslash) is the escape character. it used with:
        <span style="color:orange"> " </span> double quote
        <span style="color:orange"> ' </span> single quote
        <span style="color:orange"> \ </span> backslash
        <span style="color:orange"> / </span> slash
        <span style="color:orange"> b </span> backspace
        <span style="color:orange"> f </span> formfeed
        <span style="color:orange"> n </span> new line
        <span style="color:orange"> r </span> carriage return
        <span style="color:orange"> t </span> tab
        <span style="color:orange"> u </span> 4 hexadecimal digits

        ```js
            console.log("A" === "\u0041"); // true
        ```

    - Strings have a length property.
        ```js
            console.log("seven".length); // 5
        ```

    - Strings are <span style="color:orange"> immutable</span>. Once it is made, a string can never be changed. But you make a new string
    - You can concatenate more than one string together with the + operator.

        ```js
        console.log('c' + 'a' + 't' === 'cat'); // true
        ```


- <span style="color:green">Statements</span>
    - A compilation unit contains a set of executable statements. In web browsers, each
**script** tag delivers a compilation unit that is compiled and immediately executed. Lacking a linker, JavaScript throws them all together in a common global namespace. 
    - The switch, while, for, and do statements are allowed to have an optional label prefix that interacts with the break statement.
    - Statements tend to be executed in order from top to bottom. The sequence of execution can be altered by the conditional statements ( if and switch ), by the looping statements ( while, for, and do ), by the disruptive statements ( break, return, and throw ), and by function invocation.
    - A block is a set of statements wrapped in curly braces. Unlike many other languages, ***blocks in JavaScript do not create a new scope***, so variables should be defined at the top of the function, not in blocks.
    - The if statement changes the flow of the program based on the value of the expression. The ***then*** block is executed if the expression is truthy; otherwise, the optional **else** branch is taken.

    Here are the falsy values:
    • false
    • null
    • undefined
    • The empty string ''
    • The number 0
    • The number NaN
    All other values are truthy, including **true** , **the string 'false**' , and **all objects**.

    - **switch** statement
        - The **switch** statement performs a multiway branch. It compares the expression for
        equality with all of the specified cases. The expression can produce a number or a
        string. When an exact match is found, the statements of the matching case clause are
        executed. If there is no match, the optional default statements are executed.
        - The break statement can be used to exit from a switch.

        ```js
        switch(expression) {
          case x:
            // code block
            break;
          case y:
            // code block
            break;
          default:
            // code block
        }
        ```

    - **while** statement
        - The **while** statement performs a simple loop. While the expression is truthy, the block will be executed.

        ```js
        while (condition) {
          // code block to be executed
        }
        ```

    - The **for** statement
        - The **for** statement is a more complicated looping statement. It comes in two forms.
        1. The conventional form is controlled by three optional clauses: the initialization, the
        condition, and the increment. First, the initialization is done, which typically initializes the loop variable. Then, the condition is evaluated. Typically, this tests the loop variable against a completion criterion. If the condition is omitted, then a condition of true is assumed. If the condition is falsy, the loop breaks. Otherwise, the block is executed, then the increment executes, and then the loop repeats with the condition.
        2. The other form (called for in ) enumerates the property names (or keys) of an object.
        On each iteration, another property name string from the object is assigned to the
        variable.

            ```js
            for (myvar in obj) {
            	if (obj.hasOwnProperty(myvar)) {
            		...
            	}
            }
            ```

    - **do** statement
        - The do statement is like the while statement except that the expression is tested after the block is executed instead of before. That means that the block will always be executed at least once.

        ```js
        s = 0; i = 0;
        do {
          s += a[i] * b[i];
          i++;
        } while ( i < n );
        ```

    - **try** statement
        - The try statement executes a block and catches any exceptions that were thrown by the block. The catch clause defines a new variable that will receive the exception object.

        ```js
        try {
          //  Block of code to try
        }
        catch(Exception e) {
          //  Block of code to handle errors
        }
        ```

    - **throw** statement
        - The throw statement raises an exception. If the throw statement is in a try block, then
        control goes to the catch clause. Otherwise, the function invocation is abandoned,
        and control goes to the catch clause of the try in the calling function.
        The expression is usually an object literal containing a name property and a message
        property. The catcher of the exception can use that information to determine what to
        do.

        ```js
        <!DOCTYPE html>
        <html>
        <body>

        <p>Please input a number between 5 and 10:</p>

        <input id="demo" type="text">
        <button type="button" onclick="myFunction()">Test Input</button>
        <p id="message"></p>

        <script>
        function myFunction() {
          var message, x;
          message = document.getElementById("message");
          message.innerHTML = "";
          x = document.getElementById("demo").value;
          try {
            if(x == "") throw "is Empty";
            if(isNaN(x)) throw "not a number";
            if(x > 10) throw "too high";
            if(x < 5) throw "too low";
          }
          catch(err) {
            message.innerHTML = "Input " + err;
          }
        }
        </script>

        </body>
        </html>
        ```

    - **return** statement
        - The return statement causes the early return from a function. It can also specify the value to be returned. If a return expression is not specified, then the return value will be undefined.
        - JavaScript does not allow a line end between the return and the expression.
    - **break** statement
        - The break statement causes the exit from a loop statement or a switch statement. It can optionally have a label that will cause an exit from the labeled statement.
        - JavaScript does not allow a line end between the break and the label.

- <span style="color:green">Expressions</span>
    - An expression statement can either assign values to one or more variables or members, invoke a method, delete a property from an object.

    Operator precedence

        1. **. [] ( )**  Refinement and invocation
        2. **delete new typeof + - !** Unary operator
        3. *** / %** Multiplication, division, remainder
        4. **+ -** Addition/concatenation, subtraction
        5. **>= <= > <** Inequality
        6. **=== !==** Equality
        7. **&&** Logical and
        8. **||**  Logical or
        9. **? :**  Ternary

    - The values produced by **typeof** are 'number', 'string', 'boolean', 'undefined', 'function', and 'object'. If the operand is an array or null, then the result is 'object'
    - The **+** operator adds or concatenates. If you want it to add, make sure both operands are numbers.
    - The **/** operator can produce a non-integer result even if both operands are integers.
    - The **&&** operator produces the value of its first operand if the first operand is falsy. Otherwise, it produces the value of the second operand.
    - The **||** operator produces the value of its first operand if the first operand is truth. Otherwise, it produces the value of the second operand.
    - **( )** Invocation causes the execution of a function value. The invocation operator is a pair of parentheses that follow the function value. The parentheses can contain arguments that will be delivered to the function.
    - **.**  refinement is used to specify a property or element of an object or array.


- <span style="color:green">Functions</span>
    - A function literal defines a function value. It can have an optional name that it can use to call itself recursively. It can specify a list of parameters that will act as variables initialized by the invocation arguments. The body of the function includes variable definitions and statements.

---


## Chapter 3 - Objects

- The simple types of JavaScript are numbers, strings, booleans (true and false), null, and undefined. All other values are objects.
- **Numbers**, **strings**, and **booleans** are **object-like** in that they have methods, but they are **immutable**.
- **Objects in JavaScript are mutable keyed collections.**
- In JavaScript, arrays are objects, functions are objects, regular expressions are objects, and, of course, objects are objects.
- The **<span style="color:blue">object</span>** is a container of properties, where a property has a name and a value.
    - the property **<span style="color:orange">name</span>** can be any string, including the empty string.
    - property **<span style="color:orange">value</span>** can be any JavaScript value except for undefined
    - **Objects can contain other objects**, so they can easily represent tree or graph
    structures.

- **<span style="color:#497a6d">Object Literals</span>**

    An object literal is a pair of curly braces surrounding zero or more name/value pairs. An object literal can appear anywhere an expression can appear:

    ```js
    var empty_object = {};
    var stooge = {
        "first-name": "Jerome",
        "last-name": "Howard"
    };
    ```

    - **A property’s name**
        - can be any string, including the empty string.
        - The quotes around a property’s name in an object literal are optional if the name would be a legal JavaScript name and not a reserved word. So quotes are required around "first-name", but are optional around first_name.
    - Commas are used to separate the pairs.
    - **A property’s value** can be obtained from any expression, including another object literal. Objects can nest:

    ```js
    var flight = {
    	airline: "Oceanic",
    	number: 815,
    	departure: {
    		IATA: "SYD",
    		time: "2004-09-22 14:55",
    		city: "Sydney"
    	},
    	arrival: {
    		IATA: "LAX",
    		time: "2004-09-23 10:42",
    		city: "Los Angeles"
    	}
    };
    ```

- **<span style="color:#497a6d">Retrieval</span>**
    - Values can be retrieved from an object by wrapping a string expression in a **[ ]**
    - If the string expression is a string literal, and if it is a legal JavaScript name and
    not a reserved word, then the **.** notation can be used instead

    ```js
        stooge["first-name"] // "Jerome"
        flight.departure.IATA // "SYD"
    ```

    - The **undefined** value is produced if an attempt is made to retrieve a nonexistent
    member
    - Attempting to retrieve values from undefined will throw a **TypeError** exception

- Update
    - A value in an object can be updated by assignment. If the property name already exists in the object, the property value is replaced

        ```js
            stooge['first-name'] = 'Jerome';
        ```

    - If the object does not already have that property name, the object is augmented

        ```js
            stooge['middle-name'] = 'Lester';
            stooge.nickname = 'Curly';
            flight.equipment = {
                model: 'Boeing 777'
            };
            flight.status = 'overdue';
        ```

- **<span style="color:#497a6d">Reference</span>**
    - Objects are passed around by reference. They are never copied:
        - Passing values

            ```js
            // Passing values
            var x = 10;
            var y = x; // The value of (x) is copied to (y)
            x = 20;
            // NOW:  x = 20 , y = 10

            // Passing values
            var x = { value : 10};
            var y = x.value; // The value of (x.value) is copied to (y)
            x.value = 20;
            // NOW:  x = { value: 20 } , y = 10
            ```

        - Passing by reference

            ```js
            // Passing by reference
            var x = { value : 10}; 
            var y = x; // (X) and (Y) are pointing to the same object
            x.value = 20; 
            // NOW:  x = { value: 20 } , y = { value: 20 }
            ```

            for more details watch this: [JavaScript Value vs Reference Types](https://www.youtube.com/watch?v=fD0t_DKREbE) 

            [JavaScript Value vs Reference Types](https://www.youtube.com/watch?v=fD0t_DKREbE)

            Objects are copied by their **reference.**

- **<span style="color:#497a6d">Prototype</span>**
    - Every object is linked to a prototype object from which it can inherit properties. All objects created from object literals are linked to **Object.prototype**, an object that comes standard with JavaScript.
    - If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called ***delegation***.
    - The prototype relationship is a dynamic relationship. If we add a new property to a prototype, that property will immediately be visible in all of the objects that are based on that prototype

- **<span style="color:#497a6d">Reflection</span>**
    - when you are reflecting, you are interested in data, and so you should be aware that some values could be functions.
    - hasOwnProperty
        - returns true if the object has a particular property or false if it hasn't.
        - The hasOwnProperty method does not look at the prototype chain
    - typeof
        - You can use typeof but it will
        - The typeof method looks at all the prototype chain, and some values could be functions.

- **<span style="color:#497a6d">Enumeration</span>**
    - for in
        - The **for in** statement can loop over all of the property names in an object.  including functions and prototype properties

        ```js
            var name;
            for (name in another_stooge) {
                //to filter out the values you don’t want
                if (typeof another_stooge[name] !== 'function') {
                    document.writeln(name + ': ' + another_stooge[name]);
                }
            }
        ```

    - **Object.keys -** **Object.entries()**
        - You can also use **Object.keys or** **Object.entries()** to generate an array with all its enumerable properties, and loop through that array.

        ```js
            const obj = { a: 1, b: 2, c: 3 };

            for (const property in obj) {
            console.log(`${property}: ${obj[property]}`);
            }
            Object.keys(obj).forEach(item => console.log(`key=${item}  value=${obj[item]}`));

            Object.entries(obj).forEach(item => console.log(`${item}`));
        ```

- **<span style="color:#497a6d">Delete</span>**
    - The delete operator can be used to remove a property from an object.
    - It will not touch any of the objects in the prototype linkage.
    - Removing a property from an object may allow a property from the prototype linkage to shine through:

    ```js
        another_stooge.nickname   // 'Moe'
        // Remove nickname from another_stooge, revealing
        // the nickname of the prototype.
        delete another_stooge.nickname;
        another_stooge.nickname   // 'Curly'
    ```

- **<span style="color:#497a6d">Global Abatement</span>**
    - JavaScript makes it easy to define ***global variables*** that can hold all of the assets of your application. Unfortunately, *global variables weaken the resiliency of programs* and should be avoided.
    - One way to minimize the use of global variables is to create a single global variable for your application

    ```js
        // Create a global variable
        var MYAPP = {};
        // That variable then becomes the container for your application:
        MYAPP.stooge = {
            "first-name": "Joe",
            "last-name": "Howard"
        };
        MYAPP.flight = {
            airline: "Oceanic",
            number: 815,
            departure: {
                IATA: "SYD",
                time: "2004-09-22 14:55",
                city: "Sydney"
            },
            arrival: {
                IATA: "LAX",
                time: "2004-09-23 10:42",
                city: "Los Angeles"
            }
        };
    ```
---

