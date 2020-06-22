
CLS supports using a datetime function for log analysis. Once you enable **Collection Time** under **Log Parsing Mode** in the console, CLS will automatically add a key-value pair
as collection time to each log, and save it in TIMESTAMP format.



## Datetime Type

**UNIX Timestamp**: datetime type; a time value in microseconds since January 1, 1970. For example, `1561013773000000` represents the datetime `2019/6/20 14:56:13`. It appears as the `__UNINXTIME_US__` in each CLS log.

## Datetime Function

| Function Name                          | Description                                  | Sample                                                |
| :------------------------------ | :------------------------------------ | :-------------------------------------------------- |
| `CAST(date_string)` | Translates an ISO 8601 datetime (2019-12-25T16:17:01+08:00) to `timestamp` | `SELECTcast(time_iso8601 asTIMESTAMP)` |

## Datetime Format

| Format | Description                                                         |
| :--- | :----------------------------------------------------------- |
| %a   | Abbreviation name of the day of the week, such as Sun and Sat.                                 |
| %b   | Abbreviation name of the month, such as an and Dec.                                |
| %c   | Number of the month, such as 1, 2, 3...12.                        |
| %D   | Number with ordinal suffix of the day of the month, such as 1st, 2nd, 3rd, and 4th.               |
| %d   | Number without ordinal suffix of the day of the month, such as 01, 02, 03...31.           |
| %e   | Number without ordinal suffix of the day of the month, such as 1, 2, 3...31.                |
| %f   | Microseconds                                                         |
| %H   | Number of the hour on a 24-hour time clock, such as 00, 01, 02...23.                     |
| %h   | Number of the hour on a 12-hour time clock, such as 01, 02, 03...12.                     |
| %I   | Number of the hour on a 12-hour time clock, such as 01, 02, 03...12.                     |
| %i   | Number of the minute, such as 00, 01, 02...59.                     |
| %j   | Number of the day of the year, such as 000, 001, 002... 366.         |
| %k   | Number of the hour on a 24-hour time clock, such as 00, 01, 02...23.                     |
| %l   | Number of the hour on a 12-hour time clock, such as 01, 02, 03...12.                     |
| %M   | Full month name, such as January and December.                    |
| %m   | Number of the month, such as 01, 02. 03...12.                     |
| %p   | AM or PM                                                     |
| %r   | Time on a 12-hour time clock; format: `hh:mm:ss [AM \| PM]`                 |
| %S   | Number of the second, such as 00, 01, 02...59                       |
| %s   | Number of the second, such as 00, 01, 02...59                       |
| %T   | Time on a 24-hour time clock; format: `hh:mm:ss`                           |
| %U   | Number of the week of the year, with the week starting Sunday, such as 00, 01, 02...53 |
| %u   | Number of the week of the year, with the week starting Monday, such as 00, 01, 02...53 |
| %V   | Number of the week of the year, with the week starting Sunday. Used together with %X.          |
| %v  | Number of the week of the year, with the week starting Monday. Used together with %x.          |
| %W   | Name of the day of the week, such as Sunday, Saturday.                             |
| %w   | Number of the day of the week, from 0 for Sunday to 6 for Saturday      |
| %X   | 4-digit year; used together with %V.                                     |
| %x   | 4-digit year; used together with %v.                                     |
| %Y   | 4-digit year                                                     |
| %Y   | 2-digit year                                                     |

## Samples

The sample below casts a datetime to TIMESTAMP:

```plaintext
CAST('2019-12-25T16:17:01+08:00' as TIMESTAMP)
```


