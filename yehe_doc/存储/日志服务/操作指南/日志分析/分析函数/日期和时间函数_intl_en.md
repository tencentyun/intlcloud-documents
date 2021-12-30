CLS provides time, date, time phase, time interval, and time sequence completion functions, and supports format conversion, grouping and aggregation, and other processing of date and time values in logs.


## Date and Time Functions

| Function        | Description                         | Example                                   |
| --------------- | --------------------- | ------------------------------------ |
| current_date                   | Returns the current date.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD, such as `2021-05-21`</li><li>Return value type: DATE </il></ul>| `* | select current_date`                              |
| current_time                   | Returns the current time.<ul  style="margin: 0;"><li>Return value format: HH:MM:SS.Ms Time zone, such as `17:07:52.143+08:00`</li><li>Return value type: TIME</li></ul> | `* | select current_time`                           |
| current_timestamp              | Returns the current timestamp.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DDTHH:MM:SS.Ms Time zone, such as `2021-07-15T17:10:56.735+08:00[Asia/Shanghai]`</li><li>Return value type: TIMESTAMP</li></ul> | `* | select current_timestamp`                        |
| current_timezone()             | Returns the time zone defined by IANA (America/Los_Angeles) or the offset from UTC (+08:35).<br/>Return value type: VARCHAR, such as `Asia/Shanghai` | `* | select current_timezone()`                     |
| localtime                      | Returns the local time.<ul  style="margin: 0;"><li>Return value format: HH:MM:SS.Ms, such as `19:56:36` </li><li>Return value type: TIME</li></ul> | `* | select localtime`<br/>                                  |
| localtimestamp                 | Returns the local date and time.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD HH:MM:SS.Ms, such as `2021-07-15 19:56:26.908`</li><li>Return value type: TIMESTAMP</li></ul> | `* | select localtimestamp`                             |
| now()                          | Returns the current date and time. This function is used in the same way as the current_timestamp function.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DDTHH:MM:SS.Ms Time zone, such as `2021-07-15T17:10:56.735+08:00[Asia/Shanghai]`</li><li>Return value type: TIMESTAMP</li></ul> | `* | select now()`                                    |
| last_day_of_month(x)           | Returns the last day of a month.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD, such as `2021-05-31`</li><li>Return value type: DATE</li></ul> | `* | select last_day_of_month(cast(__TIMESTAMP__ as timestamp))` |
| from_iso8601_date(string)      | Parses an ISO 8601 formatted string into a date.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD, such as `2021-05-31`</li><li>Return value type: DATE</li></ul> | `* | select from_iso8601_date('2021-03-21')`          |
| from_iso8601_timestamp(string) | Parses an ISO 8601 formatted string into a timestamp with a time zone.<ul  style="margin: 0;"><li>Return value format: HH:MM:SS.Ms Time zone, such as `17:07:52.143+08:00`</li><li>Return value type: TIMESTAMP</li></ul> | `* | select from_iso8601_timestamp('2020-05-13')`       |
| from_unixtime(unixtime)        | Parses a UNIX formatted string into a timestamp.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD HH:MM:SS.Ms, such as `2017-05-17 01:41:15.000`</li><li>Return value type: TIMESTAMP </li></ul>| `* | select from_unixtime(1494985275) `            |
| from_unixtime(unixtime, zone)  | Parses a UNIX formatted string into a timestamp with a time zone.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD HH:MM:SS.Ms Time zone, such as `2017-05-17T09:41:15+08:00[Asia/Shanghai]`</li><li>Return value type: TIMESTAMP</li></ul> | `* | select from_unixtime(1494985275, 'Asia/Shanghai')` |
| to_unixtime(timestamp)         | Parses a timestamp formatted string into a UNIX timestamp.</br>Return value type: LONG, such as `1626347592.037` | `* | select to_unixtime(cast(__TIMESTAMP__ as timestamp)) ` |
| to_milliseconds(interval)      | Returns a time interval in milliseconds.<br/>Return value type: BIGINT, such as `300000` | `* | select to_milliseconds(INTERVAL 5 MINUTE)`        |


## Time Truncation Function

The date_trunc() function truncates a date and time expression based on the date part you specify, supporting alignment by second, minute, hour, day, month, and year. This function is often used in scenarios that require statistical analysis based on time.

| Function             | Description                                  | Example                                                         |
| ------------------ | ------------------------------------- | ------------------------------------------------------------ |
| date_trunc(unit,x) | Truncates `x` to `unit`. `x` is of the TIMESTAMP type. | `* | SELECT date_trunc('second', cast(__TIMESTAMP__ as timestamp))` |

The date_trunc() function supports the following units:

| Unit    | Example Truncated Value                | Description                       |
| ------- | ----------------------- | -------------------------- |
| second  | 2021-05-21 05:20:01.000 | -                          |
| minute  | 2021-05-21 05:20:00.000 |-                          |
| hour    | 2021-05-21 05:00:00.000 | -                         |
| day     | 2021-05-21 00:00:00.000 | Returns the zero o'clock of a specified date.       |
| week    | 2021-05-17 00:00:00.000 | Returns the zero o'clock on Monday of a specified week.       |
| month   | 2021-05-01 00:00:00.000 | Returns the zero o'clock on the first day of a specified month. |
| quarter | 2021-04-01 00:00:00.000 | Returns the zero o'clock on the first day of a specified quarter.   |
| year    | 2021-01-01 00:00:00.000 | Returns the zero o'clock on the first day of a specified year.     |


## Time Interval Functions

Time interval functions perform time period-related operations, such as adding or subtracting a specified interval from a date or counting the time between two dates.

| Function                                  | Description                                                         | Example                                                         |
| ------------------------- | ------------------------------------------- | -------------------------------------------- |
| date_add(unit,value,timestamp)          | Adds N time units (`unit`) to timestamp. If `value` is a negative value, subtraction is performed.  | `* | SELECT date_add('day', -1, TIMESTAMP '2020-03-03 03:01:00')`<br/>The return value is the date and time one day earlier than `2020-03-03 03:01:00`, that is, `2020-03-02 03:01:00`. |
| date_diff(unit, timestamp1, timestamp2) | Returns the time difference between two time expressions, for example, calculates the number of time units (`unit`) between `timestamp1` and `timestamp2`. | `* |SELECT date_diff('hour', TIMESTAMP '2020-03-01 00:00:00', TIMESTAMP '2020-03-02 00:00:00')`<br>The return value is the time difference between 2020-03-01 and 2020-03-02, that is, one day. |

The following units (`unit`) are supported:

| Unit        | Description |
| ----------- | ---- |
| millisecond | Millisecond |
| second      | Second   |
| minute      | Minute |
| hour        | Hour |
| day         | Day   |
| week        | Week   |
| month       | Month   |
| quarter     | Quarter of a year |
| year        | Year   |


**Sample**

Return the interval value in seconds between '2020-03-01 00:00:00' and '2020-03-02 00:00:00':
```
* ｜ SELECT date_diff('second', TIMESTAMP '2020-03-01 00:00:00', TIMESTAMP '2020-03-02 00:00:00')
```




## Duration Functions

| Function                                  | Description                                                         | Example                                                         |
| ------------------------------ | ------------------------------------------------------------ | --------------------------------------- |
| parse_duration(string)         | Parses a unit value string into a duration expression.<br>Return value type: INTERVAL, such as `0 00:00:00.043 (D HH:MM:SS.Ms)` | `* | SELECT parse_duration('3.81 d')`   |
| human_readable_seconds(double) | Parses a unit value string into a duration expression.<br/>Return value type: VARCHAR, such as `1 minutes` and `36 seconds` | `* | SELECT human_readable_seconds(96)` |

The following units are supported:

| Unit        | Description |
| ---- | ---- |
| ns   | Nanosecond |
| us | Microsecond |
| ms | Millisecond |
| s | Second |
| m    | Minute |
| h    | Hour |
| d    | Day   |

**Sample**

Parse the unit value string '3.81 d' into a duration string:
```
* | SELECT parse_duration('3.81 d')
```



## **MySQL Date Functions**

| Function                                  | Description                                                         | Example                                                         |
| ------------------------------ | ---------------------------------------- | --------------------------------------------- |
| date_format(timestamp, format) | Parses a date and time expression of the `timestamp` type into a date and time expression of the `format` type. | `* | select date_format(TIMESTAMP '2017-05-17 09:45:00', '%Y-%m-%d')`</br>2017-05-17 |
| date_parse(string, format)     | Expresses a string in `format` format and then parses it into a date and time expression of the TIMESTAMP type. | `* | SELECT date_parse('2017-05-17 09:45:00','%Y-%m-%d %H:%i:%s')`</br>2017-05-17 09:45:00.0 |

The following formats (`format`) are supported:

| Format | Description                                                  |
| ------ | ----------------------------------------------------- |
| %a     | Abbreviated names of the days of the week, such as Sun and Sat                            |
| %b     | Abbreviated month name, such as Jan and Dec                            |
| %c     | Month, numeric. Value range: 1-12                      |
| %D     | Day of the month with English suffix, such as 0th, 1st, 2nd, and 3rd    |
| %d     | Day of the month, decimal. Value range: 01-31           |
| %e     | Day of the month, decimal. Value range: 1-31           |
| %f     | Millisecond. Value range: 0-000000                             |
| %H     | Hour, in the 24-hour time system                                      |
| %h     | Hour, in the 12-hour time system                                      |
| %I     | Hour, in the 12-hour time system                                      |
| %i     | Minute, numeric. Value range: 00-59                     |
| %j     | Day of the year. Value range: 001-366                     |
| %k     | Hour. Value range: 0-23                                |
| %l     | Hour. Value range: 1-12                                |
| %M     | Month name in English, such as January and December               |
| %m     | Month name in English, such as January and December               |
| %p     | AM or PM                                              |
| %r     | Time, in the 12-hour time system. Format: `hh:mm:ss AM/PM`              |
| %S     | Second. Value range: 00-59                                 |
| %s     | Second. Value range: 00-59                                 |
| %T     | Time, in the 24-hour time system. Format: `hh:mm:ss`                    |
| %V     | Week of the year, where Sunday is the first day of the week. Value range: 01-53 |
| %v     | Week of the year, where Monday is the first day of the week. Value range: 01-53 |
| %W     | Names of the days of the week, such as Sunday and Saturday                  |
| %w     | Day of the week, where Sunday is day 0                         |
| %Y     | Year (4-digit), such as 2020                               |
| %y     | Year (2-digit), such as 20                               |
| %%     | Escape character of %                                         |
| %x     | Arbitrary value                                                |

**Sample**

Parse the time string '2017-05-17 09:45:00' in `format` into a date and time expression of the TIMESTAMP type, that is, '2017-05-17 09:45:00.0':
```
* | SELECT date_parse('2017-05-17 09:45:00','%Y-%m-%d %H:%i:%s')
```



## Time Completion Function

The time_series() function is used to complete missing data in your query time window.

>! The time_series() function must be used with the GROUP BY and ORDER BY syntax, and ORDER BY syntax does not support `desc` sorting.
>

**Function format**

```
time_series(time_column, interval, format, padding)
```

**Parameter description**

| Parameter | Description |
| ----------- | ------------------------------------------------------------ |
| time_column | Time column (KEY), such as `\_\_TIMESTAMP\_\_`</br>The value in this column must be a date and time expression of the LONG or TIMESTAMP type in milliseconds. |
| interval    | Time interval. Valid values are `s` (second), `m` (minute), `h` (hour), and `d` (day). For example, `5m` indicates 5 minutes. |
| format      | Time format of the return result.                                   |
| padding     | Value used to complete missing data. Valid values include:<ul  style="margin: 0;"><li>0: complete a missing value with `0`</li><li>null: complete a missing value with `null`</li><li>last: complete a missing value with the value of the previous point in time</li><li>next: complete a missing value with the value of the next point in time</li><li>avg: complete a missing value with the average value of the previous and next points in time</li></ul> |

**Sample**

Complete data with a time unit of 2 minutes:
```
* | select time_series(__TIMESTAMP__, '2m', '%Y-%m-%dT%H:%i:%s+08:00', '0')  as time, count(*) as count group by time order by time limit 1000
```



