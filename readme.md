# JavaScript: The Good Parts

#### Content

- [x]  [Chapter 1 - Good Parts](./chapters/1_Good_Parts.md)
- [x]  [Chapter 2 -  Grammar](./chapters/2_Grammar.md)
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
