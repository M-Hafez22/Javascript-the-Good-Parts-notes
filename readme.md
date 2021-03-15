# JavaScript: The Good Parts

#### Content

- [x]  [Chapter 1 - Good Parts](#chapter-1-good-parts)
- [ ]  [Chapter 2 -  Grammar](#chapter-2-grammar)
- [ ]  Chapter 3 - Objects
- [ ]  Chapter 4 - Functions
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
## Chapter 2 Grammar

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

