The names and feature descriptions of condition functions are as follows:

| Function Name | Feature Description |
| ----- | ----- | 
| CASE value<br>WHEN value1 [, value11 ]\* THEN result1<br>[ WHEN valueN [, valueN1 ]\* THEN resultN ]\*<br>[ ELSE resultZ ]<br>END | If the value equals to any value between value1 and value11, result1 is returned.<br>If the value equals to any value between valueN and valueN1, resultN is returned.<br>Otherwise resultZ is returned. |
| CASE<br>WHEN condition1 THEN result1<br>[ WHEN conditionN THEN resultN ]<br>\*<br>[ ELSE resultZ ]<br>END | If condition1 is met, result1 is returned.<br>If conditionN is met, resultN is returned.<br>Otherwise resultZ is returned. |
| NULLIF(value1, value2)  | Returns NULL if value1 equals to value2. Otherwise value1 is returned. For example, in function NULLIF(5, 5), NULL is returned, and in function NULLIF(5, 0), 5 is returned. |
| COALESCE(value, value [, value ]\* )  | Returns the first non-NULL value. For example, in function COLAESCE(NULL, 5), 5 is returned. |

