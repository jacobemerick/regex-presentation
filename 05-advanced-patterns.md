# Advanced Patterns


## Atomic Groupings

- Throws away all backtracking information after matching `(?>`
- Useful for optimization
- `/\b(brogrammer|bro)\b/` vs `/\b(?>brogrammer|bro)\b/`
- Order is important
- Avoid catastrophic backtracking!


## Possessive Quantifier

- Greedy, stubborn quantifier `*+`, `++`, `?+`
- Refuses to give up matches during backtracking
- Useful for optimization
- `/\b<span class="[^"]+">[^<]<\/span>/` on mismatched element tags
- Avoid catastrophic backtracking!


## Example - Optimize This

- Example from the author of RegexBuddy
- For a 12-column CSV, find row with the last element of 'P'
- `/^(.*?,){11}P/` results in thousands of backtrack steps for mismatch
- `/^(?>([^,\r\n]*+,){11})P/`


## Positive and Negative Lookarounds

- Zero-length assertions at the beginning and end of patterns
- Lookaheads are `(?=` and `(?!`
- Lookbehinds are `(<?<=` and `(?<!`
- More complex `/\b(?=[a-z]+\b)[a-z]*(nike|viagra|nfl)[a-z]*/`
- Lookbehinds only support fixed width, no quantifiers
- Workaround (in some languages) is `\K`


## Example - Lookarounds

- Match all states that end with the letter 'a'
- Given a list of states comma separated
- `/[A-Za-z ]+a(?=,)/`


## Conditionals

- Conditionals are awesome
- `(?ifthen|else)`
- You can use either lookarounds or capturing groups in the (if)


## Example - Parsing HTTP Headers

- Given a standard response headers, pull code and date out

```
HTTP/1.x 200 OK
Date: Sat, 28 Nov 2009 04:36:25 GMT
Expires: Sat, 28 Nov 2009 05:36:25 GMT
```

- `/(?:(HTTP)\/\d\.[a-z]|(Date|Expires):) (?(1)(\d+)|([A-Za-z ,\d:]+))/`


## Recursion and Subroutines

- `(?R)?` for recursion
- Example: `/(?:b(?R)?o)+/` matches bobo, bboobboobboo, etc
- Subroutines allow recursion based on capturing groups
- Syntax is similar but references `(?1)`, `(?<name>)`
