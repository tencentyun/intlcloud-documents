CLS provides time grouping, time truncation, time interval, and time sequence completion functions, and supports format conversion, grouping and aggregation, and other processing of date and time values in logs.

>! Among date and time functions, except the `histogram` and `time_series` functions that adopt the UTC+8 time zone, other Unix timestamp (`unixtime`) conversion functions adopt the UTC+0 time zone. To use another time zone, you need to use a function with the specified time zone feature, for example, such as `from_unixtime(__TIMESTAMP__/1000, 'Asia/Shanghai')`, or manually add the time zone offset for `unixtime`, for example, `date_trunc('second', cast(__TIMESTAMP__+8*60*60*1000 as timestamp))`.
>


## Basic Functions

| Function                                                    | Description                                                  | Example                                                      |
| ----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| current_date[](id:current_date)                             | Returns the current date.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD, such as `2021-05-21`</li><li>Return value type: DATE </il></ul> | `* \| select current_date`                                    |
| current_time [](id:current_time)                            | Returns the current time.<ul  style="margin: 0;"><li>Return value format: HH:MM:SS.Ms Time zone, such as `17:07:52.143+08:00`</li><li>Return value type: TIME</li></ul> | `* \| select current_time`                                    |
| current_timestamp[](id:current_timestamp)                   | Returns the current timestamp.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DDTHH:MM:SS.Ms Time zone, such as `2021-07-15T17:10:56.735+08:00[Asia/Shanghai]`</li><li>Return value type: TIMESTAMP</li></ul> | `* \| select current_timestamp`                               |
| current_timezone()[](id:current_timezone)                   | Returns the time zone defined by IANA (America/Los_Angeles) or the offset from UTC (+08:35).<br/>Return value type: VARCHAR, such as `Asia/Shanghai` | `* \| select current_timezone()`                              |
| localtime [](id:localtime)                                  | Returns the local time.<ul  style="margin: 0;"><li>Return value format: HH:MM:SS.Ms, such as `19:56:36` </li><li>Return value type: TIME</li></ul> | `* \| select localtime`<br/>                                  |
| localtimestamp[](id:localtimestamp)                         | Returns the local date and time.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD HH:MM:SS.Ms, such as `2021-07-15 19:56:26.908`</li><li>Return value type: TIMESTAMP</li></ul> | `* \| select localtimestamp`                                  |
| now()[](id:now)                                             | Returns the current date and time. This function is used in the same way as the current_timestamp function.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DDTHH:MM:SS.Ms Time zone, such as `2021-07-15T17:10:56.735+08:00[Asia/Shanghai]`</li><li>Return value type: TIMESTAMP</li></ul> | `* \| select now()`                                           |
| last_day_of_month(x)[](id:last_day_of_month)                | Returns the last day of a month.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD, such as `2021-05-31`</li><li>Return value type: DATE</li></ul> | `* \| select last_day_of_month(cast(__TIMESTAMP__ as timestamp))` |
| from_iso8601_date(string) [](id:from_iso8601_date)          | Parses an ISO 8601 formatted string into a date.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD, such as `2021-05-31`</li><li>Return value type: DATE</li></ul> | `* \| select from_iso8601_date('2021-03-21')`                 |
| from_iso8601_timestamp(string)[](id:from_iso8601_timestamp) | Parses an ISO 8601 formatted string into a timestamp with a time zone.<ul  style="margin: 0;"><li>Return value format: HH:MM:SS.Ms Time zone, such as `17:07:52.143+08:00`</li><li>Return value type: TIMESTAMP</li></ul> | `* \| select from_iso8601_timestamp('2020-05-13')`            |
| from_unixtime(unixtime)[](id:from_unixtime_1)               | Parses a Unix formatted string into a timestamp.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD HH:MM:SS.Ms, such as `2017-05-17 01:41:15.000`</li><li>Return value type: TIMESTAMP </li></ul> | Example 1: `* \| select from_unixtime(1494985275) `</br>Example 2: `* \| select from_unixtime(__TIMESTAMP__/1000)` |
| from_unixtime(unixtime, zone)[](id:from_unixtime_2)         | Parses a Unix formatted string into a timestamp with a time zone.<ul  style="margin: 0;"><li>Return value format: YYYY-MM-DD HH:MM:SS.Ms Time zone, such as `2017-05-17T09:41:15+08:00[Asia/Shanghai]`</li><li>Return value type: TIMESTAMP</li></ul> | Example 1: `* \| select from_unixtime(1494985275, 'Asia/Shanghai')`</br>Example 2: `* \| select from_unixtime(__TIMESTAMP__/1000, 'Asia/Shanghai')` |
| to_unixtime(timestamp)[](id:to_unixtime)                    | Parses a timestamp formatted string into a Unix timestamp.</br>Return value type: LONG, such as `1626347592.037` | `* \| select to_unixtime(cast(__TIMESTAMP__ as timestamp)) `  |
| to_milliseconds(interval)[](id:to_milliseconds)             | Returns a time interval in milliseconds.<br/>Return value type: BIGINT, such as `300000` | `* \| select to_milliseconds(INTERVAL 5 MINUTE)`              |
| to_iso8601(x)[](id:to_iso8601)                              | Parses a date and time expression of the DATE or TIMESTAMP type into a date and time expression in the ISO8601 format. | `* \| select to_iso8601(current_timestamp)`                   |
| timezone_hour(timestamp)[](id:timezone_hour)                | Returns the hour offset of the timestamp's time zone.        | `* \| SELECT current_timestamp, timezone_hour(current_timestamp)` |
| timezone_minute(timestamp)[](id:timezone_minute)            | Returns the minute offset of the timestamp's time zone.      | `* \| SELECT current_timestamp, timezone_minute(current_timestamp)` |



## Time Grouping Function

The time grouping function can be used to group and aggregate the log data at a given interval. For example, you can use it to count page views (PV) every 5 minutes.

**Function format**

```
histogram(time_column, interval)
```

**Parameter description**

| Parameter                       | Description                                                  |
| ------------------------------- | ------------------------------------------------------------ |
| time_column[](id:time_column_1) | Time column (KEY), such as `\_\_TIMESTAMP\_\_`. The value in this column must be a UNIX timestamp of the LONG type or a date and time expression of the TIMESTAMP type in milliseconds. </br>If a value does not meet the requirement, use the `cast` function to convert the ISO 8601 formatted time string into the TIMESTAMP type, for example, `cast('2020-08-19T03:18:29.000Z' as timestamp)`, or use the `[date_parse](#date_parse)` function to convert a time string of another custom type. </br> If the time column adopts the TIMESTAMP type, the corresponding date and time expression must be in the UTC+0 time zone. If the date and time expression itself is in a different time zone, adjust it to UTC+0 by calculation. For example, if the time zone of the original time is UTC+8, use `cast('2020-08-19T03:18:29.000Z' as timestamp) - interval 8 hour` to adjust the time zone. |
| interval[](id:interval_1)       | Time interval. The following time units are supported: SECOND, MINUTE, HOUR, and DAY. For example, `INTERVAL 5 MINUTE` indicates an interval of 5 minutes. |

**Sample**

Count the PV value every 5 minutes:

```
* | select histogram(__TIMESTAMP__, INTERVAL 5 MINUTE) AS dt, count(*) as PV group by dt order by dt limit 1000
```




## Time Completion Function

The `time_series()` function can be used to group and aggregate the log data at a given interval. Its main difference from the `histogram()` function is that it can complete missing data in your query time window.

>! The time_series() function must be used with the GROUP BY and ORDER BY syntax, and ORDER BY syntax does not support `desc` sorting.
>

**Function format**

```
time_series(time_column, interval, format, padding)
```

**Parameter description**

| Parameter                       | Description                                                  |
| ------------------------------- | ------------------------------------------------------------ |
| time_column[](id:time_column_2) | Time column (KEY), such as `\_\_TIMESTAMP\_\_`. The value in this column must be a UNIX timestamp of the LONG type or a date and time expression of the TIMESTAMP type in milliseconds. </br>If a value does not meet the requirement, use the `cast` function to convert the ISO 8601 formatted time string into the TIMESTAMP type, for example, `cast('2020-08-19T03:18:29.000Z' as timestamp)`, or use the `[date_parse](#date_parse)` function to convert a time string of another custom type. </br> If the time column adopts the TIMESTAMP type, the corresponding date and time expression must be in the UTC+0 time zone. If the date and time expression itself is in a different time zone, adjust it to UTC+0 by calculation. For example, if the time zone of the original time is UTC+8, use `cast('2020-08-19T03:18:29.000Z' as timestamp) - interval 8 hour` to adjust the time zone. |
| interval[](id:interval_2)       | Time interval. Valid values are `s` (second), `m` (minute), `h` (hour), and `d` (day). For example, `5m` indicates 5 minutes. |
| format [](id:format)            | Time format of the return result.                            |
| padding [](id:padding)          | Value used to complete missing data. Valid values include:<ul  style="margin: 0;"><li>0: Complete a missing value with `0`</li><li>null: Complete a missing value with `null`</li><li>last: Complete a missing value with the value of the previous point in time</li><li>next: Complete a missing value with the value of the next point in time</li><li>avg: Complete a missing value with the average value of the previous and next points in time</li></ul> |

**Sample**

Complete data with a time unit of 2 minutes:

```
* | select time_series(__TIMESTAMP__, '2m', '%Y-%m-%dT%H:%i:%s+08:00', '0')  as time, count(*) as count group by time order by time limit 1000
```



## Time Truncation Function

The date_trunc() function truncates a date and time expression based on the date part you specify, supporting alignment by second, minute, hour, day, month, and year. This function is often used in scenarios that require statistical analysis based on time.

| Function           | Description                                            | Example                                                      |
| ------------------ | ------------------------------------------------------ | ------------------------------------------------------------ |
| date_trunc(unit,x) | Truncates `x` to `unit`. `x` is of the TIMESTAMP type. | `* \| SELECT date_trunc('second', cast(__TIMESTAMP__ as timestamp))` |

The date_trunc() function supports the following units:

| Unit    | Example Truncated Value | Description                                                  |
| ------- | ----------------------- | ------------------------------------------------------------ |
| second  | 2021-05-21 05:20:01.000 | -                                                            |
| minute  | 2021-05-21 05:20:00.000 | -                                                            |
| hour    | 2021-05-21 05:00:00.000 | -                                                            |
| day     | 2021-05-21 00:00:00.000 | Returns the zero o'clock of a specified date.                |
| week    | 2021-05-19 00:00:00.000 | Returns the zero o'clock on Monday of a specified week.      |
| month   | 2021-05-01 00:00:00.000 | Returns the zero o'clock on the first day of a specified month. |
| quarter | 2021-04-01 00:00:00.000 | Returns the zero o'clock on the first day of a specified quarter. |
| year    | 2021-01-01 00:00:00.000 | Returns the zero o'clock on the first day of a specified year. |

## Time Extraction Functions

Time extraction functions are used to extract the specified time fields, such as the year and month, from date and time expressions.

| Function              | Description                                                  | Example                                                      |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| extract(field FROM x) | Extracts the specified fields from the date and time expression (x). | ` * \|select extract(hour from cast('2021-05-21 05:20:01.100' as timestamp))` |

`field` supports the following values: year, quarter, month, week, day, day_of_month, day_of_week, dow, day_of_year, doy, year_of_week, yow, hour, minute, second.

`extract(field FROM x)` can be simplified to `field()`; for example, `extract(hour from cast('2021-05-21 05:20:01.100' as timestamp))` can be simplified to `hour(cast('2021-05-21 05:20:01.100' as timestamp))`.

| Field         | Extraction Result | Description                                                  | Simplified Format |
| :------------ | :---------------- | :----------------------------------------------------------- | ----------------- |
| year          | 2021              | Extracts the year from the target date.                      | year(x)           |
| quarter       | 2                 | Extracts the quarter from the target date.                   | quarter(x)        |
| month         | 5                 | Extracts the month from the target date.                     | month(x)          |
| week          | 20                | Calculates the week of the year the target date is in.       | week(x)           |
| day           | 21                | Extracts the day from the target date by month, which is equivalent to `day_of_month`. | day(x)            |
| day_of_month  | 21                | Equivalent to `day`.                                         | day(x)            |
| day_of_week[] | 5                 | Calculates the day of the week for the target date, which is equivalent to `dow`. | day_of_week(x)    |
| dow[]         | 5                 | Equivalent to `day_of_week`.                                 | day_of_week(x)    |
| day_of_year   | 141               | Calculates the day of the year for the target date, which is equivalent to `doy`. | day_of_year(x)    |
| doy           | 141               | Equivalent to `day_of_year`.                                 | day_of_year(x)    |
| year_of_week  | 2021              | Returns the year for the target date in [ISO week date](https://en.wikipedia.org/wiki/ISO_week_date), which is equivalent to `yow`. | year_of_week(x)   |
| yow           | 2021              | Equivalent to `year_of_week`.                                | year_of_week(x)   |
| hour          | 5                 | Extracts the hour from the target date.                      | hour(x)           |
| minute        | 20                | Extracts the minute from the target date.                    | minute(x)         |
| second        | 1                 | Extracts the second from the target date.                    | second(x)         |


## Time Interval Functions

Time interval functions perform time period-related operations, such as adding or subtracting a specified interval from a date or counting the time between two dates.

| Function                                                | Description                                                  | Example                                                      |
| ------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| date_add(unit,value,timestamp) [](id:date_add)          | Adds N time units (`unit`) to timestamp. If `value` is a negative value, subtraction is performed. | `* \| SELECT date_add('day', -1, TIMESTAMP '2020-03-03 03:01:00')`<br/>The return value is the date and time one day earlier than `2020-03-03 03:01:00`, i.e., `2020-03-02 03:01:00`. |
| date_diff(unit, timestamp1, timestamp2)[](id:date_diff) | Returns the time difference between two time expressions, for example, calculates the number of time units (`unit`) between `timestamp1` and `timestamp2`. | `* \|SELECT date_diff('hour', TIMESTAMP '2020-03-01 00:00:00', TIMESTAMP '2020-03-02 00:00:00')`<br>The return value is the time difference between 2020-03-01 and 2020-03-02, i.e., one day. |

The following units (`unit`) are supported:

| unit        | Description       |
| ----------- | ----------------- |
| millisecond | Millisecond       |
| second      | Second            |
| minute      | Minute            |
| hour        | Hour              |
| day         | Day               |
| week        | Week              |
| month       | Month             |
| quarter     | Quarter of a year |
| year        | Year              |


**Sample**

Return the interval value in seconds between '2020-03-01 00:00:00' and '2020-03-02 00:00:00':
```
* | SELECT date_diff('second', TIMESTAMP '2020-03-01 00:00:00', TIMESTAMP '2020-03-02 00:00:00')
```




## Duration Functions

| Function                                                    | Description                                                  | Example                                 |
| ----------------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| parse_duration(string)[](id:parse_duration)                 | Parses a unit value string into a duration expression.<br>Return value type: INTERVAL, such as `0 00:00:00.043 (D HH:MM:SS.Ms)` | `* \| SELECT parse_duration('3.81 d')`   |
| human_readable_seconds(double)[](id:human_readable_seconds) | Parses a unit value string into a duration expression.<br/>Return value type: VARCHAR, such as `1 minutes` and `36 seconds` | `* \| SELECT human_readable_seconds(96)` |

The following units are supported:

| Unit | Description |
| ---- | ----------- |
| ns   | Nanosecond  |
| us   | Microsecond |
| ms   | Millisecond |
| s    | Second      |
| m    | Minute      |
| h    | Hour        |
| d    | Day         |

**Sample**

Parse the unit value string '3.81 d' into a duration string:
```
* | SELECT parse_duration('3.81 d')
```



<span id="date_parse"></span>
## Time Formatting Function

| Function                                         | Description                                                  | Example                                                      |
| ------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| date_format(timestamp, format)[](id:date_format) | Parses a date and time string of the `timestamp` type into a string in the `format` format. | `* \| select date_format(cast(__TIMESTAMP__ as timestamp), '%Y-%m-%d')` |
| date_parse(string, format)[](id:date_parse)      | Parses a date and time string in the `format` format into the `timestamp` type. | `* \| select date_parse('2017-05-17 09:45:00','%Y-%m-%d %H:%i:%s')` |

The following formats (`format`) are supported:

| Format | Description                                                  |
| ------ | ------------------------------------------------------------ |
| %a     | Abbreviated names of the days of the week, such as Sun and Sat |
| %b     | Abbreviated month name, such as Jan and Dec                  |
| %c     | Month, numeric. Value range: 1-12                            |
| %d     | Day of the month, decimal. Value range: 01-31                |
| %e     | Day of the month, decimal. Value range: 1-31                 |
| %f     | Millisecond. Value range: 0-000000                           |
| %H     | Hour, in the 24-hour time system                             |
| %h     | Hour, in the 12-hour time system                             |
| %I     | Hour, in the 12-hour time system                             |
| %i     | Minute, numeric. Value range: 00-59                          |
| %j     | Day of the year. Value range: 001-366                        |
| %k     | Hour. Value range: 0-23                                      |
| %l     | Hour. Value range: 1-12                                      |
| %M     | Month name in English, such as January and December          |
| %m     | Month name in digits, such as 01 and 02                      |
| %p     | AM or PM                                                     |
| %r     | Time, in the 12-hour time system. Format: `hh:mm:ss AM/PM`   |
| %S     | Second. Value range: 00-59                                   |
| %s     | Second. Value range: 00-59                                   |
| %T     | Time, in the 24-hour time system. Format: `hh:mm:ss`         |
| %v     | Week of the year, where Monday is the first day of the week. Value range: 01-53 |
| %W     | Names of the days of the week, such as Sunday and Saturday   |
| %Y     | Year (4-digit), such as 2020                                 |
| %y     | Year (2-digit), such as 20                                   |
| %%     | Escape character of %                                        |

**Sample**

Parse the time string '2017-05-17 09:45:00' in `format` into a date and time expression of the TIMESTAMP type, i.e., '2017-05-17 09:45:00.0':
```
* | SELECT date_parse('2017-05-17 09:45:00','%Y-%m-%d %H:%i:%s')
```
