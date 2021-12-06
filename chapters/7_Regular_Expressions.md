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
    - `//g` Global (match multiple times - Match All -)
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

## Elements

### Regexp Choice `|`

- A regexp choice contains one or more regexp sequences.
- The sequences are separated by the `|` (vertical bar) character.
- The choice matches if any of the sequences match. It attempts to _match each of the sequences in order_. So:
  `"into".match(/in|int/)`
  matches the `in` in `into`. It wouldn’t match `int` because the match of `in` was successful.

### Regexp Sequence

- A regexp sequence contains one or more regexp [factors](#regexp-factor). Each factor can optionally be followed by a quantifier that determines how many times the factor is allowed to appear. If there is no quantifier, then the factor will be matched one time.

### Regexp Factor

- A regexp factor can be a character, a parenthesized group, a character class, or an escape sequence.
- The following special characters must all be escaped with a backslash `\` to be taken literally, or they will take on an alternative meaning:

  ```js
  \ / [ ] ( ) { } ? + * | . ˆ$
  ```

- An unescaped
  - `.` matches any character except a line-ending character.
  - `^` matches the beginning of the text when the `lastIndex` property is zero. It can also match line-ending characters when the `m` flag is specified.
  - `$` matches the end of the text. It can also match line-ending characters when the `m` flag is specified.

### Regexp Escape

- The backslash character indicates escapement in regexp factors as well as in strings, but in regexp factors, it works a little differently.

- `\f` is the formfeed character
- `\n` is new line
- `\r` is carriage return
- `\t` is tab
- `\u` specifies Unicode as a 16-bit hex. But `\b` is not a backspace character
- `\d` is the same as [0-9]. It matches a digit. `\D` is the opposite: [^0-9].
- `\s` is the same as [\f\n\r\t\u000B\u0020\u00A0\u2028\u2029]. This is a partial set of *Unicode whitespace characters*. `\S` is the opposite: [^\f\n\r\t\u000b\u0020\u00a0\u2028\u2029].
- `\w` is the same as [0-9A-Z_a-z]. `\W` is the opposite: [^0-9a-z_a-z].This is supposed to represent the characters that appear in words. Unfortunately, it's useless for working with virtually any real language.
- `\b` was supposed to be a word-boundary anchor. Unfortunately, it uses \w to find word boundaries, so it is completely *useless for multilingual applications*.
- `\1` is a reference to the text that was captured by group 1. also `\2` is a reference to group 2, `\3` is a reference to group 3.

### Regexp Group

- There are four kinds of groups
  - **Capturing** (?:...)
    - A capturing group is a regexp choice wrapped in parentheses.
    - Every capture group is given a number (The first capturing is group 1. The second capturing is group 2.).
  - **Noncapturing** (?:...)
    - The text is matched, but not captured.
    - slight faster
    - has no bearing on numbering of capturing groups
  - **Positive lookahead**: (?=...)
    - It is like a noncapturing group except that after the group matches, the text is rewound to where the group started, effectively matching nothing.
  - **Negative lookahead** (?!...)
    - It is like a positive lookahead group, except that it matches only if it fails to match.

### Regexp Class

- is a convenient way of specifying one of a set of characters by square brackets `[]`.
- example
  - vowel characters

    ```js
    (?:a|e|i|o|u)
    ```

    Can be

    ```js
    [aeiou]
    ```

  - the set of 32 ASCII special characters

    ```js
    (?:!|"|#|\$|%|&|'|\(|\)|\*|\+|,|-|\.|\/|:|;|<|=|>|@|\[|\\|]|\^|_|` |\{|\||\}|~)
    ```

    will be

    ```js
    [!-\/:-@\[-`{-~]
    ```

### Regexp Class Escape

There are specific characters that must be escaped in a character class: `- / [ \ ] ˆ`

### Regexp Quantifier

- A number wrapped in curly braces `{}` after the factor means that the factor should match that many times.
- So, `/www/` matches the same as `/w{3}/`.
- `/w{3,6}/` will match 3, 4, 5, or 6 times. `/w{3,}/` will match 3 or more times.
- `?` is the same as `{0,1}` zero or one (optional).
- `*` is the same as `{0,}` zero or more.
- `+` is the same as `{1,}` at least one.
