

CLS requires a time attribute for each log so that the system can manage the data by the time dimension. When logs are collected using LogListener, the time attribute can be configured using two methods:

- Default method: use LogListener collection time as the time attribute.
- Custom method: use a time field in the log content as the time attribute. In this method, you need to configure a time parsing format.

>? The time precision of LogListener collection is millisecond. Therefore, the time parsing format needs to be accurate to milliseconds. If the time specified in the required format is less than 1 millisecond, 0 is automatically filled in.
>

## About Parsing Formats

| Parameter Format | Description                                                         | Example        |
| -------- | ------------------------------------------------------------ | ----------- |
| %a       | Abbreviation for a weekday                                       | Fri         |
| %A       | Full name for a weekday                                       | Friday      |
| %b       | Abbreviation for a month                                       | Jan         |
| %B       | Full name for a month                                       | January     |
| %d       | A day of a month (01 to 31)                                    | 31 
| %h       | Abbreviation for a month, same as `%b`                         | Jan         |
| %H       | An hour in the 24-hour system (00 to 23)                                      | 22          |
| %I       | An hour in the 12-hour system (01 to 12)                                      | 11          |
| %m       | Month (01 to 12), with 01 indicating January                                  | 08          |
| %M       | Minute (00 to 59), with 01 indicating one minute                                | 59          |
| %n       | Line break                                                       | Line break      |
| %p       | Morning (AM) or afternoon (PM)                                       | AM/PM       |
| %r       | Specific 12-hour combined time format, equivalent to `%I:%M:%S %p`          | 11:59:59 AM |
| %R       | Specific 24-hour combined time format, equivalent to `%H:%M`                  | 23:59       |
| %S       | Second (00 to 59)                                                | 59          |
| %f       | Millisecond |0.123          |
| %t       | Tab                                                    | Tab   |
| %y       | Year, without the century (00 to 99)                                | 19          |
| %Y       | Year, with the century, with 2018 indicating the year of 2018                           | 2019        |
| %C       | Century (obtained by dividing the year by 100, ranging from 00 to 99)                             | 20          |
| %e       | A day of a month (01 to 31)                                    | 31          |
| %j       | A day of a year (001 to 366)                                    | 365         |
| %u       | Weekday represented by a digit (1 to 7), with 1 indicating Monday and 7 indicating Sunday          | 1           |
| %U       | A week of a year (00 to 53), with the weeks starting from Sunday, that is, the first Sunday as the first day of the first week | 23          |
| %w       | Weekday represented by a digit (0 to 6), with 0 indicating Sunday and 6 indicating Saturday          | 5           |
| %W       | A week of a year (00 to 53), with the weeks starting from Monday, that is, the first Monday as the first day of the first week | 23          |
| %s       | Second-level (10-digit) UNIX timestamp                                       | 1571394459  |
| %F      | Millisecond-level (13-bit) UNIX timestamp                                        | 1571394459123  |
| %z      | Supports time zone parsing for time fields, including ISO 8601 time format and GMT time format                  | UTC/+0800/MST  |



## Configuration Samples

| Time Indication Sample                   | Time Extraction Format          |
| ------------------------------ | --------------------- |
| 2018-07-16 13:12:57.123            | %Y-%m-%d %H:%M:%S.%f     |
| [2018-07-16 13:12:57.012]      | [%Y-%m-%d %H:%M:%S.%f]   |
| 06/Aug/2019 12:12:19 +0800     | %d/%b/%Y %H:%M:%S     |
| Monday, 02-Oct-19 16:07:05 MST | %A, %d-%b-%y %H:%M:%S |
| 1571394459                     | %s                    |
| 1571394459123                     | %F (LogListener 2.6.4 or later)                   |
| 06/Aug/2019 12:12:19 +0800                    |  %d/%b/%Y %H:%M:%S %z                   |
| Monday, 02-Oct-19 16:07:05 MST             |  %A, %d-%b-%y %H:%M:%S %z                   |


