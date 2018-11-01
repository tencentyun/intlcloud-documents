The names and feature descriptions of comparison functions are as follows:

| Function Name | Feature Description |
| ----- | ----- |
| value1 = value2 | Checks whether value1 is equal to value2. TRUE is returned if they are equal, otherwise FALSE is returned.<br> 1. NULL is returned when comparing NULL with any value, which is used as FALSE in WHERE conditions. Therefore, use IS NULL instead of = NULL when comparing values with NULL.<br> 2. `=` differs from IS NOT DISTINCT FROM mainly in the way NULL values are handled. |
| value1 <> value2  | Checks whether value1 is not equal to value2. |
| value1 > value2 | Checks whether value1 is greater than value2. |
| value1 >= value2  | Checks whether value1 is greater than or equal to value2. |
| value1 < value2 | Checks whether value1 is less than value2. |
| value1 <= value2  | Checks whether value1 is less than or equal to value2. |
| value IS NULL | Returns TRUE if value is NULL, otherwise returns FALSE. |
| value IS NOT NULL | Returns TRUE if value is not NULL, otherwise returns FALSE. |
| value1 IS DISTINCT FROM value2  | Returns TRUE if value1 is not equal to value2 (NULL values are equal to each other). |
| value1 IS NOT DISTINCT FROM value2  | Returns TRUE if value1 is equal to value2 (NULL values are equal to each other). |
| value1 BETWEEN [ASYMMETRIC &#124; SYMMETRIC ] value2 AND value3 | When ASYMMETRIC is specified (default), returns TRUE if value2 ≤ value1 ≤ value3. When SYMMETRIC is explicitly specified, returns TRUE if value2 ≤ value1 ≤ value3 or value3 ≤ value1 ≤ value2. |
| value1 NOT BETWEEN value2 AND value3	| Returns TRUE if value1 is less than value2 or greater than value3. |
| string1 LIKE string2 [ ESCAPE string3 ]	| Returns TRUE if string1 matches the pattern of string2. You can specify escape characters using ESCAPE. |
| string1 NOT LIKE string2 [ ESCAPE string3 ]	| Returns TRUE if string1 does not match the pattern of string2. You can specify escape characters using ESCAPE. |
| string1 SIMILAR TO string2 [ ESCAPE string3 ]	| Returns TRUE if string1 matches the regular expression of string2. You can specify escape characters using ESCAPE. |
| string1 NOT SIMILAR TO string2 [ ESCAPE string3 ]	| Returns TRUE if string1 does not match the regular expression of string2. You can specify escape characters using ESCAPE. |
| value IN (listItem [, listItem]\* )	| Returns TRUE if value is one of the values listed after IN. This statement is equivalent to using multiple OR expressions.<br> If the listed values include NULL, NULL is returned when value is not found. Otherwise, FALSE is returned. If value is NULL, NULL is always returned. |
| value NOT IN (listItem, [, listItem]\*)	| Returns TRUE if value is not one of the values listed after IN. |
| EXISTS (a subquery) | Returns TRUE if at least one row is returned for the subquery. |

