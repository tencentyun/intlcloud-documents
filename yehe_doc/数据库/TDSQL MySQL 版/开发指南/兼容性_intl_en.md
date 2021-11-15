## Language Structures
TDSQL for MySQL supports all literal values used by MySQL, including:
```
String Literals
Numeric Literals
Date and Time Literals
Hexadecimal Literals
Bit-Value Literals
Boolean Literals
NULL Values
```

### String literals
A string literal is a sequence of bytes or characters, enclosed within either single quote `'` or double quote `"` characters. Currently, TDSQL does not support the ANSI_QUOTES SQL mode, so things enclosed with double quote `"` characters are always interpreted as string literals instead of identifiers.

TDSQL does not support character set introducers, i.e., the format of `[_charset_name]'string' [COLLATE collation_name]`.

TDSQL supports the following escape characters:
```
\0: an ASCII NUL (X'00') character
\': a single quote (') character
\": a double quote (") character
\b: a backspace character
\n: a newline (linefeed) character
\r: a carriage return character
\t: a tab character
\z: ASCII 26 (Ctrl+Z)
\\: a backslash (\) character
\%: \%
\_: _
```

### Numeric literals
Numeric literals include integer, decimal, and floating-point literals.
Integers are represented as a sequence of digits which may include `.` as a decimal separator. A numeric literal may be preceded by `-` or `+` to indicate a negative or positive value, respectively.
Exact-value numeric literals can be represented as follows: `1, .2, 3.4, -5, -6.78, +9.10`.
Scientific notation examples: `1.2E3, 1.2E-3, -1.2E3, -1.2E-3`.

### Date and time literals
TDSQL supports the following DATE formats:
```
'YYYY-MM-DD' or 'YY-MM-DD'
'YYYYMMDD' or 'YYMMDD'
YYYYMMDD or YYMMDD

For example, '2012-12-31', '2012/12/31', '2012^12^31', '2012@12@31', '20070523', and '070523'. 
```

TDSQL supports the following DATETIME and TIMESTAMP formats:
```
'YYYY-MM-DD HH:MM:SS' or 'YY-MM-DD HH:MM:SS'
'YYYYMMDDHHMMSS' or 'YYMMDDHHMMSS'
YYYYMMDDHHMMSS or YYMMDDHHMMSS 

For example, '2012-12-31 11:30:45', '2012^12^31 11+30+45', '2012/12/31 11*30*45', '2012@12@31 11^30^45', and 19830905132800. 
```

### Hexadecimal literals
TDSQL supports the following formats:
```
X'01AF'
X'01af'
x'01AF'
x'01af'
0x01AF
0x01af
```

### Bit-value literals
TDSQL supports the following formats:
```
b'01'
B'01'
0b01
```

### Boolean literals
The constants TRUE and FALSE evaluate to 1 and 0, respectively. The constant names can be written in any lettercase.
```
mysql>  SELECT TRUE, true, FALSE, false;
+------+------+-------+-------+
| TRUE | TRUE | FALSE | FALSE |
+------+------+-------+-------+
|    1 |    1 |     0 |     0 |
+------+------+-------+-------+
1 row in set (0.03 sec)
```

### NULL values
The NULL value means no data. NULL can be written in any lettercase. A synonym is \N (case-sensitive).
Be aware that the NULL value is different from values such as 0 for numeric types or the empty string (`''`) for string types.

## Character Sets and Time Zones
TDSQL supports all character sets and collations supported by MySQL.
```
mysql> show character set;
+----------+---------------------------------+---------------------+--------+
| Charset  | Description                     | Default collation   | Maxlen |
+----------+---------------------------------+---------------------+--------+
| big5     | Big5 Traditional Chinese        | big5_chinese_ci     |      2 |
| dec8     | DEC West European               | dec8_swedish_ci     |      1 |
| cp850    | DOS West European               | cp850_general_ci    |      1 |
| hp8      | HP West European                | hp8_english_ci      |      1 |
| koi8r    | KOI8-R Relcom Russian           | koi8r_general_ci    |      1 |
| latin1   | cp1252 West European            | latin1_swedish_ci   |      1 |
| latin2   | ISO 8859-2 Central European     | latin2_general_ci   |      1 |
| swe7     | 7bit Swedish                    | swe7_swedish_ci     |      1 |
| ascii    | US ASCII                        | ascii_general_ci    |      1 |
| ujis     | EUC-JP Japanese                 | ujis_japanese_ci    |      3 |
| sjis     | Shift-JIS Japanese              | sjis_japanese_ci    |      2 |
| hebrew   | ISO 8859-8 Hebrew               | hebrew_general_ci   |      1 |
| tis620   | TIS620 Thai                     | tis620_thai_ci      |      1 |
| euckr    | EUC-KR Korean                   | euckr_korean_ci     |      2 |
| koi8u    | KOI8-U Ukrainian                | koi8u_general_ci    |      1 |
| gb2312   | GB2312 Simplified Chinese       | gb2312_chinese_ci   |      2 |
| greek    | ISO 8859-7 Greek                | greek_general_ci    |      1 |
| cp1250   | Windows Central European        | cp1250_general_ci   |      1 |
| gbk      | GBK Simplified Chinese          | gbk_chinese_ci      |      2 |
| latin5   | ISO 8859-9 Turkish              | latin5_turkish_ci   |      1 |
| armscii8 | ARMSCII-8 Armenian              | armscii8_general_ci |      1 |
| utf8     | UTF-8 Unicode                   | utf8_general_ci     |      3 |
| ucs2     | UCS-2 Unicode                   | ucs2_general_ci     |      2 |
| cp866    | DOS Russian                     | cp866_general_ci    |      1 |
| keybcs2  | DOS Kamenicky Czech-Slovak      | keybcs2_general_ci  |      1 |
| macce    | Mac Central European            | macce_general_ci    |      1 |
| macroman | Mac West European               | macroman_general_ci |      1 |
| cp852    | DOS Central European            | cp852_general_ci    |      1 |
| latin7   | ISO 8859-13 Baltic              | latin7_general_ci   |      1 |
| utf8mb4  | UTF-8 Unicode                   | utf8mb4_general_ci  |      4 |
| cp1251   | Windows Cyrillic                | cp1251_general_ci   |      1 |
| utf16    | UTF-16 Unicode                  | utf16_general_ci    |      4 |
| utf16le  | UTF-16LE Unicode                | utf16le_general_ci  |      4 |
| cp1256   | Windows Arabic                  | cp1256_general_ci   |      1 |
| cp1257   | Windows Baltic                  | cp1257_general_ci   |      1 |
| utf32    | UTF-32 Unicode                  | utf32_general_ci    |      4 |
| binary   | Binary pseudo charset           | binary              |      1 |
| geostd8  | GEOSTD8 Georgian                | geostd8_general_ci  |      1 |
| cp932    | SJIS for Windows Japanese       | cp932_japanese_ci   |      2 |
| eucjpms  | UJIS for Windows Japanese       | eucjpms_japanese_ci |      3 |
| gb18030  | China National Standard GB18030 | gb18030_chinese_ci  |      4 |
+----------+---------------------------------+---------------------+--------+
41 rows in set (0.02 sec)
```

View character sets of the current connection:
```
mysql> show variables like "%char%";
+--------------------------+-----------------------------------------------------+
| Variable_name            | Value                                               |
+--------------------------+-----------------------------------------------------+
| character_set_client     | latin1                                              |
| character_set_connection | latin1                                              |
| character_set_database   | utf8                                                |
| character_set_filesystem | binary                                              |
| character_set_results    | latin1                                              |
| character_set_server     | utf8                                                |
| character_set_system     | utf8                                                |
| character_sets_dir       | /data/tdsql_run/8812/percona-5.7.17/share/charsets/ |
+--------------------------+-----------------------------------------------------+
```

Set character sets of the current connection:
```
mysql> set names utf8;
Query OK, 0 rows affected (0.03 sec)

mysql> show variables like "%char%";
+--------------------------+-----------------------------------------------------+
| Variable_name            | Value                                               |
+--------------------------+-----------------------------------------------------+
| character_set_client     | utf8                                                |
| character_set_connection | utf8                                                |
| character_set_database   | utf8                                                |
| character_set_filesystem | binary                                              |
| character_set_results    | utf8                                                |
| character_set_server     | utf8                                                |
| character_set_system     | utf8                                                |
| character_sets_dir       | /data/tdsql_run/8811/percona-5.7.17/share/charsets/ |
+--------------------------+-----------------------------------------------------+
```

>?TDSQL does not support setting global parameters which can only be set by calling frontend APIs.

Support modifying time zone attributes by setting the `time_zone` variable.
```
mysql> show variables like '%time_zone%';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | CST    |
| time_zone        | SYSTEM |
+------------------+--------+
2 rows in set (0.00 sec)

mysql> create table test.tt (ts timestamp, dt datetime,c int) shardkey=c;
Query OK, 0 rows affected (0.49 sec)

mysql>  insert into test.tt (ts,dt,c)values ('2017-10-01 12:12:12', '2017-10-01 12:12:12',1);
Query OK, 1 row affected (0.09 sec)

mysql> select * from test.tt;
+---------------------+---------------------+------+
| ts                  | dt                  | c    |
+---------------------+---------------------+------+
| 2017-10-01 12:12:12 | 2017-10-01 12:12:12 |    1 |
+---------------------+---------------------+------+
1 row in set (0.04 sec)

mysql> set time_zone = '+12:00';
Query OK, 0 rows affected (0.00 sec)

mysql> show variables like '%time_zone%';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | CST    |
| time_zone        | +12:00 |
+------------------+--------+
2 rows in set (0.00 sec)

mysql> select * from test.tt;
+---------------------+---------------------+------+
| ts                  | dt                  | c    |
+---------------------+---------------------+------+
| 2017-10-01 16:12:12 | 2017-10-01 12:12:12 |    1 |
+---------------------+---------------------+------+
1 row in set (0.06 sec)
```

## Data Types
TDSQL supports all data types supported by MySQL, including numbers, strings, date and time, spatial types, and JSON.

### Numbers
For integer types, INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, and BIGINT are supported.

| Type      | Bytes | Minimum Value (Signed/Unsigned)  | Maximum Value (Signed/Unsigned)                |
| --------- | ------ | ---------------------- | ---------------------------------------- |
| TINYINT   | 1      | -128/0                 | 127/255                                  |
| SMALLINT  | 2      | -32768/0               | 32767/65535                              |
| MEDIUMINT | 3      | -8388608/0             | 8388607/16777215                         |
| INT       | 4      | -2147483648/0          | 2147483647/4294967295                    |
| BIGINT    | 8      | -9223372036854775808/0 | 9223372036854775807/18446744073709551615 |

For floating-point types, FLOAT and DOUBLE are supported in the format of FLOAT(M,D), REAL(M,D), or DOUBLE PRECISION(M,D).

For fixed-point types, DECIMAL and NUMERIC are supported in the format of DECIMAL(M,D).

### Strings
TDSQL supports the following string types:
```
CHAR and VARCHAR
BINARY and VARBINARY
BLOB and TEXT
	TINYBLOB, TINYTEXT, MEDIUMBLOB, MEDIUMTEXT, LONGBLOB, and LONGTEXT
ENUM
SET
```

### Date and time
TDSQL supports the following date and time types:
```
DATE, DATETIME, and TIMESTAMP
TIME
YEAR
```

### Spatial data
TDSQL supports the following spatial types:
```
GEOMETRY
POINT
LINESTRING
POLYGON

MULTIPOINT
MULTILINESTRING
MULTIPOLYGON
GEOMETRYCOLLECTION
```

### JSON
TDSQL supports storing data in JSON format, making JSON processing more efficient while ensuring that errors can be detected in advance.
>!You cannot sort JSON values of different types. For example, you cannot compare JSON values of STRING type with those of INTEGER type. For JSON values of the same type, only numbers and strings can be compared and sorted. In the table created by the following SQL statements, the statement `select * from t1 order by t1->"$.key2"` is not supported because the column sorted by the ORDER BY clause contains both numbers and strings.

```sql
mysql>  CREATE TABLE t1 (jdoc JSON,a int) shardkey=a;
Query OK, 0 rows affected (0.30 sec)

mysql> INSERT INTO t1 (jdoc,a)VALUES('{"key1": "value1", "key2": "value2"}',1);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO t1 (jdoc,a)VALUES('{"key1": "value1", "key2": 2}',2);

mysql> INSERT INTO t1 (jdoc,a)VALUES('[1, 2,',5);
ERROR 3140 (22032): Invalid JSON text: "Invalid value." at position 6 in value for column 't1.jdoc'.

mysql> select * from t1;
+--------------------------------------+---+
| jdoc                                 | a |
+--------------------------------------+---+
| {"key1": "value1", "key2": "value2"} | 1 |
| {"key1": "value1", "key2": 2}        | 2 |
+--------------------------------------+---+
2 rows in set (0.00 sec)

```



## Supported Functions
Control Flow Functions

| Name     | Description                  |
| -------- | ---------------------------- |
| CASE     | Case operator                |
| IF()     | If/else construct            |
| IFNULL() | Null if/else construct       |
| NULLIF() | Return NULL if expr1 = expr2 |


 String Functions

| Name               | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| ASCII()            | Return numeric value of left-most character                  |
| BIN()              | Return a string containing binary representation of a number |
| BIT_LENGTH()       | Return length of argument in bits                            |
| CHAR()             | Return the character for each integer passed                 |
| CHAR_LENGTH()      | Return number of characters in argument                      |
| CHARACTER_LENGTH() | Synonym for CHAR_LENGTH()                                    |
| CONCAT()           | Return concatenated string                                   |
| CONCAT_WS()        | Return concatenate with separator                            |
| ELT()              | Return string at index number                                |
| EXPORT_SET()       | Return a string such that for every bit set in the value bits, you get an on string and for every unset bit, you get an off string |
| FIELD()            | Return the index (position) of the first argument in the subsequent arguments |
| FIND_IN_SET()      | Return the index position of the first argument within the second argument |
| FORMAT()           | Return a number formatted to specified number of decimal places |
| FROM_BASE64()      | Decode to a base-64 string and return result                 |
| HEX()              | Return a hexadecimal representation of a decimal or string value |
| INSERT()           | Insert a substring at the specified position up to the specified number of characters |
| INSTR()            | Return the index of the first occurrence of substring        |
| LCASE()            | Synonym for LOWER()                                          |
| LEFT()             | Return the leftmost number of characters as specified        |
| LENGTH()           | Return the length of a string in bytes                       |
| LIKE               | Simple pattern matching                                      |
| LOAD_FILE()        | Load the named file                                          |
| LOCATE()           | Return the position of the first occurrence of substring     |
| LOWER()            | Return the argument in lowercase                             |
| LPAD()             | Return the string argument, left-padded with the specified string |
| LTRIM()            | Remove leading spaces                                        |
| MAKE_SET()         | Return a set of comma-separated strings that have the corresponding bit in bits set |
| MATCH              | Perform full-text search                                     |
| MID()              | Return a substring starting from the specified position      |
| NOT LIKE           | Negation of simple pattern matching                          |
| NOT REGEXP         | Negation of REGEXP                                           |
| OCT()              | Return a string containing octal representation of a number  |
| OCTET_LENGTH()     | Synonym for LENGTH()                                         |
| ORD()              | Return character code for leftmost character of the argument |
| POSITION()         | Synonym for LOCATE()                                         |
| QUOTE()            | Escape the argument for use in an SQL statement              |
| REGEXP             | Pattern matching using regular expressions                   |
| REPEAT()           | Repeat a string the specified number of times                |
| REPLACE()          | Replace occurrences of a specified string                    |
| REVERSE()          | Reverse the characters in a string                           |
| RIGHT()            | Return the specified rightmost number of characters          |
| RLIKE              | Synonym for REGEXP                                           |
| RPAD()             | Append string the specified number of times                  |
| RTRIM()            | Remove trailing spaces                                       |
| SOUNDEX()          | Return a soundex string                                      |
| SOUNDS LIKE        | Compare sounds                                               |
| SPACE()            | Return a string of the specified number of spaces            |
| STRCMP()           | Compare two strings                                          |
| SUBSTR()           | Return the substring as specified                            |
| SUBSTRING()        | Return the substring as specified                            |
| SUBSTRING_INDEX()  | Return a substring from a string before the specified number of occurrences of the delimiter |
| TO_BASE64()        | Return the argument converted to a base-64 string            |
| TRIM()             | Remove leading and trailing spaces                           |
| UCASE()            | Synonym for UPPER()                                          |
| UNHEX()            | Return a string containing hex representation of a number    |
| UPPER()            | Convert to uppercase                                         |
| WEIGHT_STRING()    | Return the weight string for a string                        |


 Numeric Functions and Operators

| Name            | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| ABS()           | Return the absolute value                                    |
| ACOS()          | Return the arc cosine                                        |
| ASIN()          | Return the arc sine                                          |
| ATAN()          | Return the arc tangent                                       |
| ATAN2(), ATAN() | Return the arc tangent of the two arguments                  |
| CEIL()          | Return the smallest integer value not less than the argument |
| CEILING()       | Return the smallest integer value not less than the argument |
| CONV()          | Convert numbers between different number bases               |
| COS()           | Return the cosine                                            |
| COT()           | Return the cotangent                                         |
| CRC32()         | Compute a cyclic redundancy check value                      |
| DEGREES()       | Convert radians to degrees                                   |
| DIV             | Integer division                                             |
| /               | Division operator                                            |
| EXP()           | Raise to the power of                                        |
| FLOOR()         | Return the largest integer value not greater than the argument |
| LN()            | Return the natural logarithm of the argument                 |
| LOG()           | Return the natural logarithm of the first argument           |
| LOG10()         | Return the base-10 logarithm of the argument                 |
| LOG2()          | Return the base-2 logarithm of the argument                  |
| -               | Minus operator                                               |
| MOD()           | Return the remainder                                         |
| %, MOD          | Modulo operator                                              |
| PI()            | Return the value of pi                                       |
| +               | Addition operator                                            |
| POW()           | Return the argument raised to the specified power            |
| POWER()         | Return the argument raised to the specified power            |
| RADIANS()       | Return argument converted to radians                         |
| RAND()          | Return a random floating-point value                         |
| ROUND()         | Round the argument                                           |
| SIGN()          | Return the sign of the argument                              |
| SIN()           | Return the sine of the argument                              |
| SQRT()          | Return the square root of the argument                       |
| TAN()           | Return the tangent of the argument                           |
| *               | Multiplication operator                                      |
| TRUNCATE()      | Truncate to specified number of decimal places               |
| -               | Change the sign of the argument                              |


Date and Time Functions

| Name                                   | Description                                                  |
| -------------------------------------- | ------------------------------------------------------------ |
| ADDDATE()                              | Add time values (intervals) to a date value                  |
| ADDTIME()                              | Add time                                                     |
| CONVERT_TZ()                           | Convert from one time zone to another                        |
| CURDATE()                              | Return the current date                                      |
| CURRENT_DATE(), CURRENT_DATE           | Synonyms for CURDATE()                                       |
| CURRENT_TIME(), CURRENT_TIME           | Synonyms for CURTIME()                                       |
| CURRENT_TIMESTAMP(), CURRENT_TIMESTAMP | Synonyms for NOW()                                           |
| CURTIME()                              | Return the current time                                      |
| DATE()                                 | Extract the date part of a date or datetime expression       |
| DATE_ADD()                             | Add time values (intervals) to a date value                  |
| DATE_FORMAT()                          | Format date as specified                                     |
| DATE_SUB()                             | Subtract a time value (interval) from a date                 |
| DATEDIFF()                             | Subtract two dates                                           |
| DAY()                                  | Synonym for DAYOFMONTH()                                     |
| DAYNAME()                              | Return the name of the weekday                               |
| DAYOFMONTH()                           | Return the day of the month (0-31)                           |
| DAYOFWEEK()                            | Return the weekday index of the argument                     |
| DAYOFYEAR()                            | Return the day of the year (1-366)                           |
| EXTRACT()                              | Extract part of a date                                       |
| FROM_DAYS()                            | Convert a day number to a date                               |
| FROM_UNIXTIME()                        | Format Unix timestamp as a date                              |
| GET_FORMAT()                           | Return a date format string                                  |
| HOUR()                                 | Extract the hour                                             |
| LAST_DAY                               | Return the last day of the month for the argument            |
| LOCALTIME(), LOCALTIME                 | Synonym for NOW()                                            |
| LOCALTIMESTAMP, LOCALTIMESTAMP()       | Synonym for NOW()                                            |
| MAKEDATE()                             | Create a date from the year and day of year                  |
| MAKETIME()                             | Create time from hour, minute, second                        |
| MICROSECOND()                          | Return the microseconds from argument                        |
| MINUTE()                               | Return the minute from the argument                          |
| MONTH()                                | Return the month from the date passed                        |
| MONTHNAME()                            | Return the name of the month                                 |
| NOW()                                  | Return the current date and time                             |
| PERIOD_ADD()                           | Add a period to a year-month                                 |
| PERIOD_DIFF()                          | Return the number of months between periods                  |
| QUARTER()                              | Return the quarter from a date argument                      |
| SEC_TO_TIME()                          | Converts seconds to 'HH:MM:SS' format                        |
| SECOND()                               | Return the second (0-59)                                     |
| STR_TO_DATE()                          | Convert a string to a date                                   |
| SUBDATE()                              | Synonym for DATE_SUB() when invoked with three arguments     |
| SUBTIME()                              | Subtract times                                               |
| SYSDATE()                              | Return the time at which the function executes               |
| TIME()                                 | Extract the time portion of the expression passed            |
| TIME_FORMAT()                          | Format as time                                               |
| TIME_TO_SEC()                          | Return the argument converted to seconds                     |
| TIMEDIFF()                             | Subtract time                                                |
| TIMESTAMP()                            | With a single argument, this function returns the date or datetime expression; with two arguments, the sum of the arguments |
| TIMESTAMPADD()                         | Add an interval to a datetime expression                     |
| TIMESTAMPDIFF()                        | Subtract an interval from a datetime expression              |
| TO_DAYS()                              | Return the date argument converted to days                   |
| TO_SECONDS()                           | Return the date or datetime argument converted to seconds since Year 0 |
| UNIX_TIMESTAMP()                       | Return a Unix timestamp                                      |
| UTC_DATE()                             | Return the current UTC date                                  |
| UTC_TIME()                             | Return the current UTC time                                  |
| UTC_TIMESTAMP()                        | Return the current UTC date and time                         |
| WEEK()                                 | Return the week number                                       |
| WEEKDAY()                              | Return the weekday index                                     |
| WEEKOFYEAR()                           | Return the calendar week of the date (1-53)                  |
| YEAR()                                 | Return the year                                              |
| YEARWEEK()                             | Return the year and week                                     |

Aggregate (GROUP BY) Functions     

| Name    | Description                                   |
| ------- | --------------------------------------------- |
| AVG()   | Return the average value of the argument      |
| COUNT() | Return a count of the number of rows returned |
| MAX()   | Return the maximum value                      |
| MIN()   | Return the minimum value                      |
| SUM()   | Return the sum                                |


Bit Functions and Operators

| Name        | Description                            |
| ----------- | -------------------------------------- |
| BIT_COUNT() | Return the number of bits that are set |
| &           | Bitwise AND                            |
| ~           | Bitwise inversion                      |
| \           | Bitwise OR                             |
| ^           | Bitwise XOR                            |
| <<          | Left shift                             |
| >>          | Right shift                            |


Cast Functions and Operators

| Name      | Description                      |
| --------- | -------------------------------- |
| BINARY    | Cast a string to a binary string |
| CAST()    | Cast a value as a certain type   |
| CONVERT() | Cast a value as a certain type   |

