# PHP Implementation


## Matching

- preg_match() for single, preg_match_all() for global
- args: pattern, subject, matches (by reference), flags, offset

```
preg_match(
    '/<a href="(?P<link>[^"]+)"(?: title="(?P<title>[^"]+)")?>(?P<anchor>[^<]+)<\/a>/',
    '<a href="url" title="seo title">seo anchor</a>',
    $matches);

{
    [0]=> string(46) "<a href="url" title="seo title">seo anchor</a>",
    ["link"]=> string(3) "url",
    [1]=> string(3) "url",
    ["title"]=> string(9) "seo title",
    [2]=> string(9) "seo title",
    ["anchor"]=> string(10) "seo anchor",
    [3]=> string(10) "seo anchor",
}
```


## Replacing

- preg_replace() and preg_filter()
- args: pattern, replacement, subject, limit, count
- returns modified subject
- preg_filter() will return null or empty array on failure
- can accept strings or arrays for replacements and strings
- preg_replace_callback() accepts a callback (awesome)


## Misc

- preg_split() splits a string into an array by a regex
- preg_quote() escapes chacters
- preg_last_error() returns an error code (for debugging)
- [PHP's PCRE functions](http://www.php.net/manual/en/ref.pcre.php)
