## LIKE
```
string LIKE pattern [ESCAPE escape-character]
string NOT LIKE pattern [ESCAPE escape-character]
```
The `LIKE` expression returns true if the `string` matches the supplied `pattern`. (As expected, the `NOT LIKE` expression returns false if `LIKE` returns true, and vice versa.)
An equivalent expression is `NOT` (`string` LIKE `pattern`).
Sample code:
```
postgres=# SELECT 'abc' LIKE 'abc';
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT 'abc' LIKE 'a%';
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT 'abc' LIKE '_b_';
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT 'abc' LIKE 'c';
 ?column? 
----------
 f
(1 row)
```

## `SIMILAR TO` Regular Expressions
```
string SIMILAR TO pattern [ESCAPE escape-character]
string NOT SIMILAR TO pattern [ESCAPE escape-character]
```
The `SIMILAR TO` operator returns true or false depending on whether its pattern matches the given string. It is similar to `LIKE`, except that it interprets the pattern using the SQL standard's definition of a regular expression.

In addition to these facilities borrowed from `LIKE`, `SIMILAR TO` supports these pattern-matching metacharacters borrowed from POSIX regular expressions:
- `|` denotes alternation (either of two alternatives).
- `*` denotes the repetition of the previous item zero or more times.
- `+` denotes the repetition of the previous item one or more times.
- `?` denotes the repetition of the previous item zero times or one time.
- `{m}` denotes the repetition of the previous item exactly `m` times.
- `{m,}` denotes the repetition of the previous item `m` or more times.
- `{m,n}` denotes the repetition of the previous item at least `m` and not more than `n` times.
- Parentheses () can be used to group items into a single logical item.
- A bracket expression [...] specifies a character class, just as in POSIX regular expressions.
- Notice that the period (.) is not a metacharacter for `SIMILAR TO`.

Sample code:
```
postgres=# SELECT 'abc' SIMILAR TO 'abc';
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT 'abc' SIMILAR TO 'a';
 ?column? 
----------
 f
(1 row)
 
postgres=# SELECT 'abc' SIMILAR TO '%(b|d)%';
 ?column? 
----------
 t
(1 row)
```

## POSIX Regular Expressions
POSIX regular expressions provide a more powerful means for pattern matching than the `LIKE` and `SIMILAR TO` operators.
The following are the available operators for pattern matching by using POSIX regular expressions:

| **Operator** | **Description**                       |
| ---------- | ------------------------------ |
| ~          | Matches regular expression, case sensitive     |
| ~*         | Matches regular expression, case insensitive   |
| !~         | Does not match regular expression, case sensitive  |
| !~*        | Does not match regular expression, case insensitive |

Sample code:
```
postgres=# SELECT 'abc' ~ 'abc' ;
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT 'abc' ~ '^a' ;
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT 'abc' ~ '^(b|c)';
 ?column? 
----------
 f
(1 row)
```
