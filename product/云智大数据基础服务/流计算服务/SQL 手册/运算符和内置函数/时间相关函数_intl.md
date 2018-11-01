The names and feature descriptions of time-related functions are as follows:

| Function Name | Feature Description |
| ----- | ----- |
| DATE string	| Converts a date string in "yy-MM-dd" format to that in SQL format. |
| TIME string	| Converts a time string in "hh:mm:ss" format to that in SQL format. |
| TIMESTAMP string	| Converts a string in "yy-MM-dd hh:mm:ss.fff" format to an SQL timestamp. |
| INTERVAL string range	| Accepts strings (in milliseconds) in "dd hh:mm:ss.fff" format, or strings (in months) in "yyyy-MM" format.<br> DAY, MINUTE, DAY TO HOUR and DAY TO SECOND are supported for the range of strings in milliseconds. YEAR and YEAR TO MONTH are supported for the range of strings in months. For example, INTERVAL '10 00:00:00.004' DAY TO SECOND, INTERVAL '10' DAY, and INTERVAL '2-10' YEAR TO MONTH. |
| CURRENT_DATE	| Returns the current date (UTC) in SQL format. |
| CURRENT_TIME	| Returns the current time (UTC) in SQL format. |
| CURRENT_TIMESTAMP	| Returns the current timestamp (UTC) in SQL format. |
| LOCALTIME	| Returns the local time in SQL format. |
| LOCALTIMESTAMP	| Returns the local timestamp in SQL format. |
| EXTRACT(timeintervalunit FROM temporal)	| Returns the specified information in the string of a time point or a time period. For example, 5 is returned by using the function EXTRACT(DAY FROM DATE '2006-06-05'), and 2018 is returned by using the function EXTRACT(YEAR FROM DATE '2018-06-12'). |
| FLOOR(timepoint TO timeintervalunit)	| Rounds down a time point. For example, 12:44:00 is returned by using the function FLOOR(TIME '12:44:31' TO MINUTE). |
| CEIL(timepoint TO timeintervalunit)	| Rounds up a time point. For example, 12:45:00 is returned by using the function CEIL(TIME '12:44:31' TO MINUTE). |
| QUARTER(date)	| Returns the quarter of the specified SQL date. For example, 3 is returned by using the function QUARTER(DATE '1994-09-27'), indicating it is the 3rd quarter. |
| (timepoint, temporal) OVERLAPS (timepoint, temporal)	| Determines whether the two time periods overlap with each other. For example, in function (TIME<br>'2:55:00', INTERVAL '1' HOUR) OVERLAPS (TIME<br>'3:30:00', INTERVAL '2' HOUR), TRUE is returned, and in function (TIME<br>'9:00:00', TIME '10:00:00') OVERLAPS (TIME<br>'10:15:00', INTERVAL '3' HOUR), FALSE is returned. |
| TO_TIMESTAMP(string, simple_format) | Formats a string into a timestamp supported by SCS using simple_format, a time formatting template supported by Java's SimpleDateFormat. For more information, see [Type Conversion Function](/document/product/849/18079). |
| DATE_FORMAT_SIMPLE (timestamp, simple_format	| Converts a timestamp into a string using the time formatting template supported by Java's SimpleDateFormat. For more information, see [Type Conversion Function](/document/product/849/18079). |
| DATE_FORMAT(timestamp, format) | Formats a timestamp into a string using "format", a format string compatible with MySQL. Different from DATE_FORMAT_SIMPLE, it uses MySQL formatting syntax instead of Java SimpleDateFormat formatting syntax. For more information, see [Type Conversion Function](/document/product/849/18079). |
| TIMESTAMPADD(unit, interval, timestamp)	| Add a time period to the specified timestamp. Negative time period is supported. "interval" must be one of SECOND, MINUTE, HOUR, DAY, WEEK, MONTH, QUARTER or YEAR. For example, '2013-01-09' is returned by using the function TIMESTAMPADD(WEEK, 1, '2013-01-02'). |

