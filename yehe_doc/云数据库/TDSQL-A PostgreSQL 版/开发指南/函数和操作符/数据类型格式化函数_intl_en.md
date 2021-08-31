Formatting functions can be used to convert various data types (date/time, integer, floating point, and numeric) to formatted strings or from formatted strings to specific data types.
The functions listed below all follow a common calling convention: the first argument is the value to be formatted and the second argument is a template that defines the output or input format.

| **Function**                        | **Return Type**              | **Description**                 |
| ------------------------------- | ------------------------- | ------------------------ |
| to_char(timestamp,text)         | text                      | Converts timestamp to string        |
| to_char(interval,text)          | text                      | Converts interval to string         |
| to_char(int,text)               | text                      | Converts integer to string         |
| to_char(double  precision,text) | text                      | Converts real/double precision to string |
| to_char(numeric,text)           | text                      | Converts numeric to string         |
| to_date(text,text)              | date                      | Converts string to date         |
| to_number(text,text)            | numeric                   | Converts string to numeric         |
| to_timestamp(text,text)         | timestamp  with time zone | Converts string to timestamp       |

Sample code:
```
postgres=# SELECT to_char(interval '15h 2m 12s', 'HH24:MI:SS');
 to_char 
----------
 15:02:12
(1 row)
 
postgres=# SELECT to_char(125, '999');
 to_char 
---------
 125
(1 row)
 
postgres=# SELECT to_char(125.8::real, '999D9');
 to_char 
---------
 125.8
(1 row)
 
postgres=# SELECT to_char(-125.8, '999D99S');
 to_char 
---------
 125.80-
(1 row)
 
postgres=# SELECT to_date('05 Dec 2000', 'DD Mon YYYY');
 to_date 
------------
 2000-12-05
(1 row)
```
