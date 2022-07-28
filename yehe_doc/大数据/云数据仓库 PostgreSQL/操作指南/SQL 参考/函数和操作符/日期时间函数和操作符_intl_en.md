Common date and time functions and operators supported by the database are as listed below:

| Operator | Example | Result |
| ------ | ------------------------------------------------------------ | --------------------------------- |
| +      | date   '2001-09-28' + integer '7'                            | date   '2001-10-05'               |
| +      | date   '2001-09-28' + interval '1 hour'                      | timestamp   '2001-09-28 01:00:00' |
| +      | date   '2001-09-28' + time '03:00'                           | timestamp   '2001-09-28 03:00:00' |
| +      | interval   '1 day' + interval '1 hour'                       | interval   '1 day 01:00:00'       |
| +      | timestamp   '2001-09-28 01:00' + interval '23 hours'         | timestamp   '2001-09-29 00:00:00' |
| +      | time   '01:00' + interval '3 hours'                          | time   '04:00:00'                 |
| -      | -   interval '23 hours'                                      | interval   '-23:00:00'            |
| -      | date   '2001-10-01' - date '2001-09-28'                      | integer   '3'                     |
| -      | date   '2001-10-01' - integer '7'                            | date   '2001-09-24'               |
| -      | date   '2001-09-28' - interval '1 hour'                      | timestamp   '2001-09-27 23:00:00' |
| -      | time   '05:00' - time '03:00'                                | interval   '02:00:00'             |
| -      | time   '05:00' - interval '2 hours'                          | time   '03:00:00'                 |
| -      | timestamp   '2001-09-28 23:00' - interval '23 hours'         | timestamp   '2001-09-28 00:00:00' |
| -      | interval   '1 day' - interval '1 hour'                       | interval   '1 day -01:00:00'      |
| -      | timestamp   '2001-09-29 03:00' - timestamp '2001-09-27 12:00' | interval   '1 day 15:00:00'       |
| *      | 900 * interval   '1 second'                                  | interval   '00:15:00'             |
| *      | 21 *   interval '1 day'                                      | interval   '21 days'              |
| *      | double   precision '3.5' * interval '1 hour'                 | interval   '03:30:00'             |
| /      | interval   '1 hour' / double precision '1.5'                 | interval   '00:40:00'             |

Common date/time functions are as listed below:

| Function | Return Type | Description | Example | Result |
| ----------------------------- | -------------------------- | ------------------------ | --------------------------- | ------------ |
| age(timestamp, timestamp)     | interval   | Calculates time difference    | age(timestamp   '2001-04-10', timestamp '1957-06-13') | 43   years 9 mons 27 days             |
| age(timestamp)                | interval   | Calculates time difference               | age(timestamp   '1957-06-13')        | 43   years 8 mons 3 days              |
| current_date                  | date        | Current date               | select   current_date;                  | 2019-02-18                            |
| current_time                  | time   with time zone      | Current time of day       | select   current_time;   | 16:42:59.991189+08                    |
| current_timestamp             | timestamp   with time zone | Current timestamp  | select   current_timestamp;   | 2019-02-18   16:43:20.167284+08       |
| date_part(text, timestamp)    | double   precision  | Gets a part of datetime   | date_part('hour',   timestamp '2001-02-16 20:38:40')  | 20          |
| date_part(text, interval)     | double   precision         | Gets a part of datetime   | date_part('month',   interval '2 years 3 months')     | 3      |
| date_trunc(text, timestamp)   | timestamp    | Clears the specified part of datetime | date_trunc('hour',   timestamp '2001-02-16 20:38:40') | 2001-02-16   20:00:00   |
| extract(field from timestamp) | double   precision         | Similar to `date_part`          | extract(hour   from timestamp '2001-02-16 20:38:40')  | 20    |
| extract(field from interval)  | double   precision         | Similar to `date_part`          | extract(month   from interval '2 years 3 months')     | 3    |
| localtime                     | time                       | Gets local time             | select   localtime;    | 16:56:09.339026                       |
| localtimestamp                | timestamp                  | Local date and time           | select   localtimestamp;    | 2019-02-18   16:56:42.331012          |
| now()                         | timestamp   with time zone | Gets current time             | select   now();    | 2019-02-18   16:56:58.843212+08       |
| timeofday()                   | text                       | Current date and time           | select   timeofday();   | Mon   Feb 18 16:57:27.677262 2019 CST |
