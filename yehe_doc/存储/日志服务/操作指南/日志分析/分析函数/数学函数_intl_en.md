>? Currently, CLS functions can be used in most regions. If they are required in Beijing, Shanghai, Guangzhou, and Nanjing, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

CLS's log analysis feature allows you to analyze logs by analyzing fields of int, long, and double types via mathematical calculation functions and mathematical statistical functions. The detailed statements and meanings of the functions are listed below.

| Function        | Description                                                         |
| ------------- | ------------------------------------------------------------ |
| ABS(KEY)      | Returns the absolute value of the `KEY` column.                                        |
| SQRT(KEY)     | Returns the square root of the `KEY` column.                                         |
| POWER(KEY, y) | Returns `KEY` raised to the power of `y`.                                         |
| ROUND(KEY, y) | Returns `KEY` rounded to `y` decimal places. Example: round(1.012345,2)   = 1.01. If `y` is empty, decimal places are ignored. |
| FLOOR(KEY)    | Returns `KEY` rounded down to the nearest integer.                                      |
| LOG(KEY)      | Returns the natural logarithm of `KEY`.                                      |
| LOG10(KEY)      | Returns the base-10 natural logarithm of `KEY`.                                      |
