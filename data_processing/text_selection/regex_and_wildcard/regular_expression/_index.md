# More RegEx

{{< hint info >}}
There are certainly more practical aspects of `RegEx`. Here, we discuss additional syntax elements and provide examples of how to use them effectively in various scenarios.
{{< /hint >}}

## Capturing Groups

A capturing group is a portion of a RegEx pattern enclosed in parentheses `(...)`. Capturing groups serve two main purposes:

1. They allow you to apply *quantifiers* and *alternation* to a group of characters or subpatterns.
2. They *capture* the matched text within the group for later use, such as for *extracting*, *replacing*, or *referencing* the matched content.

### Extracting Dates and Their Components

Suppose you have dates formatted as `MM-DD-YYYY` and want to extract the entire date and its components (month, day, and year). The following RegEx pattern uses capturing groups to achieve this:

```javascript
(\d{2})-(\d{2})-(\d{4})
```

- [ ] `(\d{2})`: Capturing group that matches two digits (the month, the date)...
- [ ] `-`: Matches a hyphen (the separator).

### Reformatting Dates

> Suppose you have dates formatted as `MM-DD-YYYY` and want to reformat them to the `YYYY-MM-DD` format. This pattern is the same as in the previous example.

In a programming language that supports RegEx, such as `Python` or `JavaScript`, you can use the captured groups to reformat the date:

```python
import re

date_string = "12-25-2021"
pattern = r"(\d{2})-(\d{2})-(\d{4})"
reformatted_date = re.sub(pattern, r"\3-\1-\2", date_string)

print(reformatted_date)  # Output: "2021-12-25"
```

## Non-capturing Groups

`(?:...)` creates a non-capturing group, which means the matched content within the group won't be captured for later use. Non-capturing groups are useful when you need to apply quantifiers or alternation to a group of characters but don't need to reference the matched content.
> *Example:* The RegEx pattern "^(?:\+1\s)?\d{3}-\d{3}-\d{4}$" matches both US phone numbers with and without the "+1" country code prefix but doesn't capture the prefix.

### Matching dates with different separators

> Suppose you have dates formatted as `MM-DD-YYYY` or `MM/DD/YYYY`, and you want to match the dates without capturing the separators.

```python
(?:\d{2})(?:-|\/)(?:\d{2})(?:-|\/)(?:\d{4})
```

## Lookaround assertions

## Greedy vs. Lazy quantifiers

## Flags/Modifiers
