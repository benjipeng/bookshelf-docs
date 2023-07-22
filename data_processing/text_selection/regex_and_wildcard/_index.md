---
bookCollapseSection: true
weight: 20
---

# RegEx and Wildcard

## Wildcards

Wildcards are characters used to represent `any` number of `characters` or ***specific*** character sets within a string. They're commonly used in *search patterns for file names and text*.

> For instance, in UNIX-like operating systems, the `'*'` and `'?'` characters are popular wildcards. Here's a brief explanation of these two wildcard characters:

- `Asterisk (*):` Represents zero or more characters, often used for matching multiple files or text patterns.
- `Question mark (?):` Represents exactly one character, typically used when you want to match a pattern with a variable single character.

## RegEx

{{< hint info >}}
`Regular expressions` are a powerful tool for `pattern matching` and `searching within text`. They allow you to define a search pattern and apply it to a string to **find**, **extract**, or **modify** the desired text. RegEx is available in most programming languages, such as Python, JavaScript, Java, and Perl.
{{< /hint >}}

### Basic RegEx Concept

- Literal characters: Matches the exact character(s) in the string.
  - `Example:` The RegEx pattern `"abc"` would match the substring `"abc"` in the string `"abcdef"`.

- Metacharacters: Special characters that have a specific meaning in the context of a regular expression.
  - `Example:` The dot `(.)` is a metacharacter that matches any single character except a newline.

- Character classes: Enclosed in square brackets `[]`, they define a set of characters to match.
  - `Example:` The RegEx pattern `"[aeiou]"` would match any single vowel in the string `"hello world"`.

### RegEx Quantifiers

**Zero or one:** A question mark `(?)` indicates that the **preceding** character or group may appear zero or one time.
> Example: The RegEx pattern "colou?r" matches both "color" and "colour".

**Zero or more:** An asterisk `(*)` indicates that the **preceding** character or group may appear zero or more times.
> Example: The RegEx pattern `"ab*c"` matches "ac", "abc", "abbc", and so on.

**One or more:** A plus sign `(+)` indicates that the preceding character or group must appear at least once.
> Example: The RegEx pattern `"ab+c"` matches "abc", "abbc", but not "ac".

**Specific number:** Curly braces {} contain a number to indicate how many times the preceding character or group should appear.
> Example: The RegEx pattern `"ab{3}c"` matches "abbbc", but not "abc" or "abbc".

### Anchors

**Start of the string:** The caret `(^)` symbol indicates that the pattern must start at the beginning of the string.
> Example: The RegEx pattern "^abc" matches "abcde", but not "xabcde".

{{< hint danger >}}
**Note:** In `[]`, `^`, on the other hand, *ONLY* means ***"not the following"*** when *inside* AND *at the start* of `[]`.
{{< /hint >}}

To clarify, therefore:

- [x] `[^abc]` >> *not* a, b or c
- [ ] `[ab^cd]` >> a, b, ^ (*character*), c or d
- [ ] `\^` >> an *actual* `^` character

**End of the string:** The dollar sign `($)` indicates that the pattern must appear at the end of the string.
> Example: The RegEx pattern "abc$" matches "xabc", but not "xabcx".

### Grouping and Capturing

**Vertical bar** `(|)`: Represents an *OR* operator, allowing a match for either the expression on the left or the right.
> Example: The RegEx pattern "abc|xyz" matches either "abc" or "xyz".

### Predefined character classes

`\d` : Matches any digit (0-9).  
`\D` : Matches any non-digit character.  
`\s` : Matches any whitespace character (space, tab, newline, etc.).  
`\S` : Matches any non-whitespace character.  
`\w` : Matches any word character (alphanumeric, including underscore).  
`\W` : Matches any non-word character.

`^(\d{3}-\d{2}-\d{4})|(\d{9})$` >> >> *valid* Social Security numbers
