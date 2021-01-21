

CLS requires a time attribute for each log so that the system can manage the data by the time dimension. When logs are collected by LogListener, the time attribute can be configured in the following two methods:

- Default method: use LogListener collection time as the time attribute.
- Custom method: use a time field in the log content as the time attribute. For this method, you need to configure a time parsing format.

>?The LogListener collection time can be accurate down to the second. Therefore, the time parsing format only needs to be configured at the second level.



## Parsing Format Description

| Parameter Format | Description                                                         | Example        |
| -------- | ------------------------------------------------------------ | ----------- |
| %a       | Abbreviation of a day in a week                                       | Fri         |
| %A       | Full name of a day in a week                                       | Friday      |
| %b       | Abbreviation of a month                                       | Jan         |
| %B       | Full name of a month                                       | January     |
| %d       | A day in a month (01–31)                                    | 31          |
| %h       | Abbreviation of a month, which is the same as `%b`                         | Jan         |
| %H       | An hour in the 24-hour system (00–23)                                      | 22          |
| %I       | An hour in the 12-hour system (01–12)                                      | 11          |
| %m       | Month (01–12), with 01 indicating January                                  | 08          |
| %M       | Minute (00–59), with 01 indicating the first minute                                | 59          |
| %n       | Line break                                                       | Line break      |
| %p       | Morning (AM) or afternoon (PM)                                       | AM/PM       |
| %r       | Specific 12-hour combined time format, which is equivalent to `%I:%M:%S %p`          | 11:59:59 AM |
| %R       | Specific 24-hour combined time format, which is equivalent to `%H:%M`                  | 23:59       |
| %S       | Second (00–59)                                                | 59          |
| %f       | Millisecond |0.123          |
| %t       | Tab                                                    | Tab   |
| %y       | Year without the century (00–99)                                | 19          |
| %Y       | Year with the century, with 2018 indicating the year of 2018                           | 2019        |
| %C       | Century in the range from 00 to 99, which is obtained by dividing the year by 100                             | 20          |
| %e       | A day in a month (01–31)                                    | 31          |
| %j       | A day in a year (001–366)                                    | 365         |
| %u       | A day in a week represented by a digit (1–7), with 1 indicating Monday and 7 indicating Sunday          | 1           |
| %U       | A week in a year (00–53), with the week starting on Sunday, that is, the first Sunday is the first day of the first week | 23          |
| %w       | A day in a week represented by a digit (0–6), with 0 indicating Sunday and 6 indicating Saturday          | 5           |
| %W       | A week in a year (00–53), with the week starting on Monday, that is, the first Monday is the first day of the first week | 23          |
| %s       | Second-level (10-digit) Unix timestamp                                       | 1571394459  |
| %F      | Millisecond-level (13-digit) Unix timestamp                                        | 1571394459123  |



## Configuration Samples

| Time Indication Sample                   | Time Extraction Format          |
| ------------------------------ | --------------------- |
| 2018-07-16 13:12:57.123            | %Y-%m-%d %H:%M:%S.%f     |
| [2018-07-16 13:12:57.012]      | [%Y-%m-%d %H:%M:%S.%f]   |
| 06/Aug/2019 12:12:19 +0800     | %d/%b/%Y %H:%M:%S     |
| Monday, 02-Oct-19 16:07:05 MST | %A, %d-%b-%y %H:%M:%S |
| 1571394459                     | %s                    |
| 1571394459123                     | %F                    |


