# Basic Matching


## Literals, Special, and Classes

- Literal characters are acceptable ```abc```, ```158```
- You can also use alternation with literals ```cat|dog```
- Special characters mean something special ```+```, ```-```, ```[]```
- Escape special character to use ```\\+```
- Its easy to define ranges, or character classes ```[a-z]```, ```[0-9]```


## Whitespace and Shorthand

- ```\n``` is new line
- ```\r``` is return carriage (thanks windows)
- ```\t``` is tab
- ```\s``` is whitespace ```[ \t\f]``` (and maybe ```[\r\n]```)
- ```\w``` is word character ```[A-Za-z0-9_]```
- ```\b``` is word boundary (zero-length)
- ```\d``` is digit
- Capitalize to negate (```\D``` matches !digit)


## Quantifiers

- ```*``` matches 0 or more
- ```+``` matches 1 or more
- ```{4}``` matches four characters
- ```{4,6}``` matches between four and six characters
- ```?``` makes things optional


## Dots and Boundaries

- ```.``` matches everything except line breaks
- Dot is too powerful - avoid if possible
- Negated character classes are better
- ```^```, ```$``` force boundaries
- ```/^\d+$/``` vs ```/\d+/``` on 123abc456


## Example - Valid Password

- Only contain letters (upper and lower) and numbers
- Between six and eight characters

---

```/^[a-zA-Z0-9]{6,8}$/```


## Example - Full Name

- First, last, optional middle name
- Space between name pieces
- First letter capitalized, no special chars allowed

---

```/^[A-Z][a-z]+ ([A-Z][a-z]+ )?[A-Z][a-z]+$/```


## Greediness

- Regex is by nature greedy
- Example: ```/<a\b.*>/``` for anchor tags
- Add ```?``` to make quantifiers lazy
- ```+?```, ```*?```, ```??```
- Alternatively, use negatated character classes ```/<a\b[^>]*>```


## Capturing Groups

- ```()``` for capturing blocks for later parsing
- Also useful for limiting quantifiers or alternations
- If you need a group but don't want it captured, ```(?:```
- Alternation can spawn multiple captures, use ```(?|```
- You can also name groups with ```(?P<name>pattern)```


## Examples - Basic Link

- Create a regex to only capture url and anchor from a link
- If title is present, capture that too

---

```/<a href="(?P<link>[^"]+)"(?: title="(?P<title>[^"]+)")?>(?P<anchor>[^<]+)<\/a>/```


## Backreferences

- Allows you to reference previous capturing groups
- Indexed left to right ```\\1```
- You can also backreference named captured ```(?P=name)```
- Backtracking is tricky
- ```/<([a-z]+)[^>]*>[^<]+<\/\1>/```


## Pattern Modifiers

- ```i``` sets case-insensitive
- ```m``` sets multiline (for ```^``` and ```$```)
- ```s``` sets ```.``` to match everything, including newlines
- ```x``` ignores whitespace in pattern (so it can breathe more)
- ```e``` evaluates the code (deprecated, don't do this!)
- Many more on [PHP's PCRE page](http://www.php.net/manual/en/reference.pcre.pattern.modifiers.php)