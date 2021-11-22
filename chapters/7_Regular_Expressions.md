# Chapter 7 - Regular Expressions

- Regular expressions are used with methods to **search, replace, and extract** information from strings.

> [regexr](https://regexr.com/) > [Learn Regular Expressions In 20 Minutes](https://www.youtube.com/watch?v=rhzKDrUiJVk&t) > [Regular Expressions Cheatsheet - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Cheatsheet)

- The methods that work with regular expressions are:
  - `regexp.exec`
  - `regexp.test`
  - `string.match`
  - `string.replace`
  - `string.search`
  - `string.split`

> Regular expressions usually have a significant performance advantage over equivalent string operations in JavaScript.
> These will all be described in **Chapter 8**

- regular expression rols

  - No comments or whitespace.
  - It must be on a single line.
  - It cannot be broken into smaller pieces the way that functions can

- Construction a regular expression literal
  - it must be enclosed in slashes `/ /`
  - There are three **flags**:
    - `//g` Global (match multiple times; the precise meaning of this varies with the method)
    - `//i` Insensitive (ignore character case)
    - `//m` Multiline (^ and $ can match line-ending characters)

## An Example

- `(...)` indicates a capturing group
- A **capturing group** copies the text it matches and places it in the result array.
- `(?:...)` indicates a noncapturing group.
- `[...]` indicates a character class.

- `ˆ` indicates the beginning of a string
- `-` The hyphens indicate ranges. (A-Za-z)
- `+` indicates that the character class will be matched one or more times.
- `:` matched literally
- `?` indicates that the group is optional - _repeat zero or one time_.
- `\/` The backslash `\` escapes the forward slash `/` (which traditionally symbolises the end of the regular expression literal) and together they indicate that the forward slash `/` should be matched.

## Construction

- Two ways to build a regular expression:

- **Regular Expression literals** as per the examples above start and end with a slash `/`

  - Here the flags are appended after the final slash, for example `/i`
  - Be careful: RegExp objects made by regular expression literals share a single instance

- **Use RegExp constructor**

  - The first parameter is the string to be made into a RegExp object, the second is the flag
  - Useful when all information for creating the regular expression is not available at time of programming
  - Backslashes mean something in the constructor, so these must be doubled and quotes must be escaped

  ```js
  var my_regexp = new RegExp("'(?:\\\\.|[ˆ\\\\\\'])*'", "g");
  ```
