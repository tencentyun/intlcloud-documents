The names and feature descriptions of aggregate functions are as follows:

| Function Name | Feature Description | 
| ----- | ----- |
| COUNT(value [, value]\* ) | Returns the number of input rows of which the value is not NULL. |
| COUNT(\*) | Returns the number of input rows. |
| AVG(numeric)  | Returns the arithmetic average of all inputs in the specified column. |
| SUM(numeric)  | Returns the sum of all inputs in the specified column. |
| MAX(value)  | Returns the maximum value of all inputs in the specified column (note: cannot be used for TIMESTAMP type). |
| MIN(value)  | Returns the minimum value of all inputs in the specified column (note: cannot be used for TIMESTAMP type). |
| STDDEV_POP(value) | Calculates the population standard deviation for all inputs in the specified column. |
| STDDEV_SAMP(value)  | Calculates the sample standard deviation for all inputs in the specified column. |
| VAR_POP(value)  | Calculates the population variance for all inputs in the specified column. |
| VAR_SAMP(value) | Calculates the sample variance for all inputs in the specified column. |
| COLLECT(value)  | Returns the collection of all non-NULL inputs in the specified column (duplicate values are allowed). If all values are NULL, an empty set is returned. |

