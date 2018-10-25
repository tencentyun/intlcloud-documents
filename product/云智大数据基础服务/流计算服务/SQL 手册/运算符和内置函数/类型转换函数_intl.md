The names and feature descriptions of type conversion functions are as follows:

| Function Name | Feature Description | 
| ----- | ----- |
| CAST(value AS type)	| Changes the type of a value to "type". For example, CAST(`hello` AS VARCHAR) changes the type of `hello' to VARCHAR. |
| TO_TIMESTAMP(string, simple_format) | Formats a string into a timestamp supported by SCS using simple_format, a time formatting template supported by Java's SimpleDateFormat.<br> For example, TO_TIMESTAMP(ts, 'yyyy-MM-dd HH:mm:ss') |
| DATE_FORMAT_SIMPLE(timestamp, simple_format | Converts a timestamp into a string using the time formatting template supported by Java's SimpleDateFormat.<br> For example, DATE_FORMAT_SIMPLE(ts, 'yyyy-MM-dd HH:mm:ss') |
| DATE_FORMAT(timestamp, format) | Formats a timestamp into a string using a template format compatible with MySQL. Different from DATE_FORMAT_SIMPLE, it uses MySQL formatting syntax instead of Java SimpleDateFormat formatting syntax.<br> You can use this function in the same way with date_parse() function of MySQL.<br> For example, '2017, 05 May' is returned by using the function DATE_FORMAT(ts, '%Y, %d %M') |

