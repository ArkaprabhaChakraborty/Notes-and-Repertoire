---
description: A primer on writing regexes
---

# Regex 101

## Introduction

### Matching the beginning of a line using the caret `^`&#x20;

The caret or `^` matches the beginning of the line. Anything coming after the caret will only match if it's present at the beginning of any line in a multiline string.

{% code overflow="wrap" %}
```
`^abc` matches "abc" only if it appears at the beginning of a string or line.
`^Hello` will match the string "Hello" only if it is at the very beginning of a line.
```
{% endcode %}

### The dot operator `.`

A dot `.` matches any single character other than an newline `\n`.  A dot can be used a wildcard for any single character except for a newline character. This makes it very versatile for matching any character in a specific position within a string.&#x20;

{% code overflow="wrap" %}
```
`a.b` will match any string that has an "a", followed by any single character (except a newline), followed by a "b". For example, it will match "acb", "a1b", and "a-b".

`...` will match any three characters in a row (except for newlines). For example, it will match "abc", "123", and "a b".
```
{% endcode %}

### The end operator `$`

The end operator `$` is used to denote the end of a string or the end of line. This is useful for ensuring that a match occurs only at the end of a string or line. The `$` operator in regex is not a character but a positional assertion that denotes the end of a line or string.

<pre><code><strong>`abc$` will match the string "abc" only if it appears at the very end of a string.
</strong>It will match "xabc" but not "abcy".

regex: abc$
string: "xabc\nyabc\nzabc"
matches: "xabc", "yabc", "zabc" (all three "abc" at the end of each line)
</code></pre>

### The asterisk or star operator `*`

The asterisk `*` is a quantifier that matches the preceding element zero or more times. This means that the element it follows can appear any number of times, including not at all.

{% code overflow="wrap" %}
```
regex: ba*n
strings: "bn", "ban", "baan", "baaan"
matches: "bn", "ban", "baan", "baaan"

regex: a.*b
strings: "ab", "acb", "axyzb", "a123b"
matches: "ab", "acb", "axyzb", "a123b" (Since . matches any character other than $ and * represents 0 or more times)
```
{% endcode %}

### The digit matcher `\d` and the non digit matcher `\D`&#x20;

The `\d` used to match any digits (0-9). The `\D`  operator is used to match any non-digit characters.&#x20;

{% code overflow="wrap" %}
```
The following regex matches a sequence of 2 digits, 1 non-digit, 2 digit, 1 non-digit and 4 digits.

"\d\d\D\d\d\D\d\d\d\d"
```
{% endcode %}

The `\D` will match any whitespace operator too since they are non digits.

### The whitespace matcher `\s` and the non whitespace matcher `\S`

The `\s` matches nay of the white space characters (`\r`, `\n`, `\t`, `\f`). The `\S` matches any non whitespace character.

```
The string "12 11 15" matches the regex "\S\S\s\S\S\s\S\S"
```

### The word `\w` and the non word `\W` &#x20;

The \w matches a word character, it could be a letter, a digit or an underscore. The \W matches a non-word character, anything that other than what \w matches.

{% code overflow="wrap" %}
```
The following pattern matches
# 3 word characters, 1 non-words, 10 word characters, 1 non-word character and finally 3 word characters.

"\w\w\w\W\w\w\w\w\w\w\w\w\w\w\W\w\w\w"
```
{% endcode %}

### The `{}` quantifier

The {} quantifier is used to specify the exact number of occurrences, or a range of occurrences, of the preceding element. The syntax within the braces allows for various forms of repetition.

{% code overflow="wrap" %}
```
The string "aaa" matches regex "a{3}", whereas "aa" wil not match it. 

The string "12 11 15" matches the regex "\S{2}\s\S{2}\s\S{2}" and the regex "\d{2}\D\d{2}\D\d{2}".
```
{% endcode %}

When paired with `,` within the `{}`, ranges or "atleast" logic can be used.

```
At Least n Occurrences:
{n,}: Matches at least n occurrences of the preceding element.
Example: a{2,} matches "aa", "aaa", "aaaa", etc.

Range of Occurrences:
{n,m}: Matches between n and m occurrences (inclusive) of the preceding element.
Example: a{2,4} matches "aa", "aaa", and "aaaa".
```



