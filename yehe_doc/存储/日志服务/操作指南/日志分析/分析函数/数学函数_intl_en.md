
The log analysis feature of CLS can analyze log fields in `int`, `long`, and `double` types through statistical functions and mathematical functions. Detailed statements and descriptions are as follows:

| Function        | Description                                                         |
| ------------- | ------------------------------------------------------------ |
| ABS(KEY)      | Returns the absolute value of the KEY column.                                        |
| SQRT(KEY)     | Returns the square root of the KEY column.                                        |
| POWER(KEY, y) | Returns the yth power of the KEY column.                                         |
| ROUND(KEY, y) | Rounds to y decimal place(s) for the KEY column; for example, round(1.012345,2) = 1.01. If y is empty, decimal places are ignored. |
| FLOOR(KEY)    | Returns the largest integer smaller than KEY.                                      |
| LOG(KEY)      | Returns the natural logarithm of the KEY column.                                      |
| LOG10(KEY)    | Returns the natural logarithm with base 10 of the KEY column.                               |
