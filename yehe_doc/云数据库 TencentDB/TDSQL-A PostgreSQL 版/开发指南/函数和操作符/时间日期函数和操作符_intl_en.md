## Date/Time Operators
| **Operator** | **Example**                                                    | **Result**                        |
| ---------- | ----------------------------------------------------------- | ------------------------------- |
| +          | date '2001-09-28' + integer '7'                             | date '2001-10-05'               |
| +          | date '2001-09-28' + interval '1 hour'                       | timestamp '2001-09-28 01:00:00' |
| +          | date '2001-09-28' + time '03:00'                            | timestamp '2001-09-28 03:00:00' |
| +          | interval '1 day' + interval '1 hour'                        | interval '1 day 01:00:00'       |
| +          | timestamp '2001-09-28 01:00' + interval '23 hours'          | timestamp '2001-09-29 00:00:00' |
| +          | time '01:00' + interval '3 hours'                           | time '04:00:00'                 |
| -          | - interval '23 hours'                                       | interval '-23:00:00'            |
| -          | date '2001-10-01' - date '2001-09-28'                       | integer '3' (days)            |
| -          | date '2001-10-01' - integer '7'                             | date '2001-09-24'               |
| -          | date '2001-09-28' - interval '1 hour'                       | timestamp '2001-09-27 23:00:00' |
| -          | time '05:00' - time '03:00'                                 | interval '02:00:00'             |
| -          | time '05:00' - interval '2 hours'                           | time '03:00:00'                 |
| -          | timestamp '2001-09-28 23:00' - interval '23 hours'          | timestamp '2001-09-28 00:00:00' |
| -          | interval '1 day' - interval '1 hour'                        | interval '1 day -01:00:00'      |
| -          | timestamp '2001-09-29 03:00' - timestamp '2001-09-27 12:00' | interval '1 day 15:00:00'       |
| *          | 900 * interval '1 second'                                   | interval '00:15:00'             |
| *          | 21 * interval '1 day'                                       | interval '21 days'              |
| *          | double precision '3.5' * interval '1 hour'                  | interval '03:30:00'             |
| /          | interval '1 hour' / double precision '1.5'                  | interval '00:40:00'             |

## Date/Time Functions
| **Function**                                                     | **Return Type**           | **Description**                                                     |
| ------------------------------------------------ | ------------------------ | ----------------------------------------- |
| age(timestamp,timestamp)                   | interval                 | Subtracts arguments, producing a "symbolic" result that uses years and months, rather than just days        |
| age(timestamp)                                               | interval                 | Subtracts from `current_date` (at midnight)                           |
| clock_timestamp()                                            | timestamp with time zone | Current date and time (changes during statement execution)                              |
| current_date                                                 | date                     | Current date                                     |
| current_time                                                 | time with time zone      | Current time of day                              |
| current_timestamp                                            | timestamp with time zone | Current date and time                         |
| date_part(text,timestamp)                                    | double precision         | Gets subfield                            |
| date_part(text,interval)                                     | double precision         | Gets subfield                                |
| date_trunc(text,timestamp)                                   | timestamp                | Truncates to specified precision                         |
| date_trunc(text,interval)                                    | interval                 | Truncates to specified precision                          |
| extract(field from timestamp)                                | double precision         | Gets subfield                                |
| extract(field from interval)                                 | double precision         | Gets subfield                           |
| isfinite(date)                                               | bool                     | Test for finite date                     |
| isfinite(timestamp)                                          | bool                     | Test for finite timestamp                           |
| isfinite(interval)                                           | bool                     | Test for finite interval                                 |
| justify_days(interval)                       | interval                 | Adjusts interval so 30-day time periods are represented as months                     |
| justify_hours(interval)                      | interval                 | Adjusts interval so 24-hour time periods are represented as days                         |
| justif_interval(interval)                                    | interval                 | Adjusts interval                                                     |
| localtime                                                    | time                     | Current time of day                                                     |
| localtimestamp                                | timestamp                | Current date and time                                               |
| make_date(year int,   month int,  day int)       | date         | Creates date from year, month, and day fields                 |
| make_interval(  years int DEFAULT 0,   months int DEFAULT 0,   weeksint DEFAULT 0,   days int DEFAULT 0,   hours int DEFAULT 0,   minsint DEFAULT 0,   secs double precision   DEFAULT 0.0) | interval                 | Creates interval from years, months, weeks, days, hours, minutes, and seconds fields         |
| make_time(hour int,   min int,  sec double precision) | time           | Creates time from hour, minute, and seconds fields                     |
| make_timestamp(year int,   monthint,   day int,   hour int,   minint, sec double precision) | timestamp         | Creates timestamp from year, month, day, hour, minute, and seconds fields                 |
| make_timestamptz(year int,  month int,   day int,   hour int,  min int,  sec double precision,   [ timezone text ]) | timestamp with time zone | Creates timestamp with time zone from year, month, day, hour, minute, and seconds fields; if `timezone` is not specified, the current time zone is used |
| now()                                                        | timestamp with time zone | Current date and time                        |
| statement_timestamp()                                        | timestamp with time zone | Current date and time               |
| timeofday()                                                  | text                     | Current date and time                                               |
| transaction_timestamp()                                      | timestamp with time zone | Current date and time                           |
| to_timestamp(double precision)             | timestamp with time zone | Converts Unix epoch to timestamp                |

## OVERLAPS
```
(start1, end1) OVERLAPS (start2, end2)
(start1, length1) OVERLAPS (start2, length2)
```
The `OVERLAPS` operator uses the above two expressions to yield true when two time periods overlap or false when they do not overlap.
Sample code:
```
postgres=# SELECT (DATE '2001-02-16', DATE '2001-12-21') OVERLAPS
postgres-#    (DATE '2001-10-30', DATE '2002-10-30');
 overlaps 
----------
 t
(1 row)

postgres=# SELECT (DATE '2001-02-16', INTERVAL '100 days') OVERLAPS
postgres-#    (DATE '2001-10-30', DATE '2002-10-30');
 overlaps 
----------
 f
(1 row)
```

## EXTRACT
```
EXTRACT(field FROM source)
```
The `EXTRACT` function retrieves subfields from date/time values.
- `source` must be a value expression of type `timestamp`, `time`, or `interval`.
- `field` is an identifier or string that selects what field to extract from the source value.

The `EXTRACT` function returns values of type `double precision`.
Sample code:
```
postgres=# SELECT EXTRACT(DAY FROM TIMESTAMP '2001-02-16 20:38:40');
 date_part 
-----------
    16
(1 row)
 
postgres=# SELECT EXTRACT(DECADE FROM TIMESTAMP '2001-02-16 20:38:40');
 date_part 
-----------
    200
(1 row)
 
postgres=# SELECT EXTRACT(DOY FROM TIMESTAMP '2001-02-16 20:38:40');
 date_part 
-----------
    47
(1 row)
 
postgres=# SELECT EXTRACT(HOUR FROM TIMESTAMP '2001-02-16 20:38:40');
 date_part 
-----------
    20
(1 row)
```

## DATE_TRUNC
```
date_trunc('field', source)
```
The function `DATE_TRUNC` is conceptually similar to the `trunc` function for numbers.
- `source` is a value expression of type `timestamp` or `interval`.
- `field` selects to which precision to truncate the input value. Valid values are: `microseconds`, `milliseconds`, `second`, `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year`, `decade`, `century`, and `millennium`.

The return value is of type `timestamp` or `interval` with all fields that are less significant than the selected one set to zero.
Sample code:
```
postgres=# SELECT date_trunc('hour', TIMESTAMP '2001-02-16 20:38:40');
   date_trunc   
---------------------
 2001-02-16 20:00:00
(1 row)

postgres=# SELECT date_trunc('year', TIMESTAMP '2001-02-16 20:38:40');
   date_trunc   
---------------------
 2001-01-01 00:00:00
(1 row)
```

## AT TIME ZONE
The `AT TIME ZONE` function converts timestamp without time zone to/from timestamp with time zone.
Sample code:
```
postgres=# SELECT TIMESTAMP '2001-02-16 20:38:40' AT TIME ZONE 'MST';
    timezone    
------------------------
 2001-02-17 11:38:40+08
(1 row)
 
postgres=# SELECT TIMESTAMP WITH TIME ZONE '2001-02-16 20:38:40-05' AT TIME ZONE 'MST';
    timezone   
---------------------
 2001-02-16 18:38:40
(1 row)
```
The first example adds a time zone to a value that lacks it to convert it to an MST (UTC-7) time and displays the value as PST (UTC-8). The second example shifts the timestamp specified as EST (UTC-5) to the local time zone MST (UTC-7).
The function `timezone(zone, timestamp)` is equivalent to the SQL-conforming construct `timestamp AT TIME ZONE zone`.

## Current Date/Time
The following functions can be used to get the current date and time:
```
CURRENT_DATE
CURRENT_TIME
CURRENT_TIMESTAMP
CURRENT_TIME(precision)
CURRENT_TIMESTAMP(precision)
LOCALTIME
LOCALTIMESTAMP
LOCALTIME(precision)
LOCALTIMESTAMP(precision)
```

## Delaying Execution
The following functions are available to delay the execution of the server process:
```
pg_sleep(seconds)
pg_sleep_for(interval)
pg_sleep_until(timestamp with time zone)
```
`pg_sleep` makes the current session's process sleep until `seconds` seconds have elapsed.
`seconds` is a value of type `double precision`, so fractional-second delays can be specified.
`pg_sleep_for` is a convenience function for larger sleep times specified as an `interval`.
`pg_sleep_until` is a convenience function for when a specific wake-up time is desired.
Sample code:
```
SELECT pg_sleep(1.5);
SELECT pg_sleep_for('5 minutes');
SELECT pg_sleep_until('tomorrow 03:00');
```
