## LIKE
The database supports many pattern matching modes. The first is LIKE or NOT LIKE.

| Example | Result |
| ------------------- | ----- |
| 'abc'   LIKE 'abc'  | true  |
| 'abc'   LIKE 'abcz' | false |
| 'abc'   LIKE 'a%'   | true  |
| 'abc'   LIKE '\_a\_'  | false |
| 'abc'   LIKE 'a\_'   | false |
| 'abc'   LIKE 'a'    | false |

## SIMILAR TO
The second pattern matching mode supported by the database is SIMILAR TO, which is similar to LIKE but supports more matching syntaxes as listed below:

| Syntax | Description | Example | Result |
| -------------------------- | ------------------------- | ----------------------------------- | ---- |
| \|                         | Supports optional matching            | 'abc'   SIMILAR TO '%(b\|d\|c\|e)%' | True |
| *                          | Zero or more repetitions of the previous element   | 'abc'   SIMILAR TO 'abcd*'          | True |
| 'abc'   SIMILAR TO 'abc*'  | true                      |        -                             |    -  |
| 'abc'   SIMILAR TO 'ab*'   | false                     |              -                       |   -   |
| +                          | One or more repetitions of the previous element | 'abc'   SIMILAR TO 'abc+'           | True |
| 'abc'   SIMILAR TO 'abcc+' | false                     |           -                          | -     |

## POSIX Regular Expressions
The database also supports POSIX regular expression, which provides more powerful functions than the LIKE and SIMILAR TO operators as listed below:

| Function | Description | Example | Result |
| ----------------------- | --------------------------- | -------------------------------- | ----------------------------------- |
| substring(string from pattern)     | Extracts a substring that matches a regular expression pattern      | substring('foobar'   from 'o.b')      | oob            |
| regexp_replace(source,   pattern, replacement [, flags ]) | Replaces the matched string in source    | regexp_replace('foobarbaz',   'b..', 'X')  | fooXX    |
| regexp_matches(string,   pattern [, flags ])     | Returns a text array consisting of all captured substrings matching a POSIX regular expression pattern | regexp_matches('foobarbequebaz',   '(bar)(beque)');          | {bar,beque}                            |
| regexp_split_to_table(string,   pattern [, flags ])       | Splits a string by using a POSIX regular expression pattern as a delimiter  | SELECT   regexp_split_to_table('the quick brown fox jumped', E'\\\s+') ; | the    quick    brown    fox    jumped |
| regexp_split_to_array(string,   pattern [, flags ])       | Is a regular expression splitting function similar to `regexp_split_to_table`, but returns a text array | SELECT   regexp_split_to_array('the quick brown fox jumped', E'\\\s+'); | {the,quick,brown,fox,jumped}           |
