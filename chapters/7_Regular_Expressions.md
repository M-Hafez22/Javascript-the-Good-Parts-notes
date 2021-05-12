# Chapter 7 - Regular Expressions

- Regular expressions are used with methods to **search, replace, and extract** information from strings.

> [regexr](https://regexr.com/)
> [Learn Regular Expressions In 20 Minutes](https://www.youtube.com/watch?v=rhzKDrUiJVk&t)
> [Regular Expressions Cheatsheet - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Cheatsheet)

- The methods that work with regular expressions are:
  - `regexp.exec`
  - `regexp.test`
  - `string.match`
  - `string.replace`
  - `string.search`
  - `and string.split.`

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
- `?` indicates that the group is optional - *repeat zero or one time*.
- `\/` The backslash `\` escapes the forward slash `/` (which traditionally symbolises the end of the regular expression literal) and together they indicate that the forward slash `/` should be matched.
