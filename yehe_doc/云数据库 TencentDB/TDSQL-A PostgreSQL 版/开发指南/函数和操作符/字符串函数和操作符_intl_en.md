TDSQL-A for PostgreSQL supports many types of feature-rich string functions and operators. This document only lists commonly used ones. For more information, please see [String Functions and Operators](http://www.postgres.cn/docs/10/functions-string.html).

| **Operator/Function**                                              | **Return Type** | **Description**                                                     |
| ----------------------------------------- | ------------ | ------------------------------------------ |
| string \|\| string                                           | text         | String concatenation                                                         |
| char_length(string) or  character_length(string)        | int          | Number of characters in string                                                   |
| lower(string)                                              | text         | Converts string to lower case                                       |
| overlay(string   placing   stringfrom int   [for int]) | text         | Replaces substring                           |
| position(substring   in string)                          | int          | Location of specified substring                                                 |
| substring(  string [from int] [for int])               | text         | Extracts substring                                                     |
| trim(  [leading \| trailing \| both]   [characters]  fromstring) | text         | Removes the longest string containing only characters from `characters` (a space by default) from the start, end, or both ends (`both` is the default) of `string` |
| upper(string)                                              | text         | Converts string to upper case                                       |
| ascii(string)                                              | int          | ASCII code of the first character of the argument. For UTF8, it returns the Unicode code point of the character. For other multibyte encodings, the argument must be an ASCII character |
| btrim(string text   [, characterstext])                | text         | Removes the longest string consisting only of characters in `characters` (a space by default) from the start and end of `string` |
| concat(str "any"   [, str "any"   [, ...] ])         | text         | Concatenates the text representations of all the arguments. NULL arguments are ignored               |
| decode(string text,  format text)                    | bytea        | Decodes binary data from textual representation in `string`. Options for `format` are the same as in `encode` |
| left(str text,  n int)                               | text         | Returns first n characters in the string. When n is negative, return all but last |n| characters |
| length(string)                                             | int          | Number of characters in `string`                                           |
| lpad(string text,  length int   [, fill text])   | text         | Fills up the string to length `length` by prepending the characters `fill` (a space by default). If the `string` is already longer than `length`, then it is truncated (on the right) |
| ltrim(string text   [, characterstext])                | text         | Removes the longest string consisting only of characters from `characters` (a space by default) from the start of `string` |
| repeat(string text,  number int)                     | text         | Repeats `string` the specified `number` of times                    |

Sample code:
```
postgres=# SELECT 'T'||'dapg';
 ?column? 
----------
 Tdapg
(1 row)
 
postgres=# SELECT char_length('jose');
 char_length 
-------------
      4
(1 row)
 
postgres=# SELECT overlay('Txxxxas' placing 'hom' from 2 for 4);
 overlay 
---------
 Thomas
(1 row)
 
postgres=# SELECT position('om' in 'Thomas');
 position 
----------
    3
(1 row)
 
postgres=# SELECT substring('Thomas' from 2 for 3);
 substring 
-----------
 hom
(1 row)
 
postgres=# SELECT trim(both from 'yxTomxx', 'xyz');
 btrim 
-------
 Tom
(1 row)
 
postgres=# SELECT ascii('x');
 ascii 
-------
  120
(1 row)
 
postgres=# SELECT btrim('xyxtrimyyx', 'xyz');
 btrim 
-------
 trim
(1 row)
 
postgres=# SELECT concat('abcde', 2, NULL, 22);
 concat 
----------
 abcde222
(1 row)
```

