## 언어 구조
TDSQL for MySQL은 다음을 포함한 MySQL에서 사용하는 모든 리터럴 값을 지원합니다.
```
String Literals
Numeric Literals
Date and Time Literals
Hexadecimal Literals
Bit-Value Literals
Boolean Literals
NULL Values
```

### String Literals
String Literals는 작은 따옴표 `‘` 또는 큰 따옴표 `“`로 묶인 bytes 또는 characters입니다. 현재 TDSQL for MySQL은 ANSI_QUOTES SQL MODE를 지원하지 않으므로 큰 따옴표 `“`로 묶인 것은 항상 identifier 대신 String Literals로 해석됩니다.

TDSQL은 character set introducer를 지원하지 않습니다. 즉, `[_charset_name]'string' [COLLATE collation_name]` 형식입니다.

TDSQL은 다음 이스케이프 문자를 지원합니다.
```
\0: ASCII NUL (X’00’) 캐릭터
\‘: 작은 따옴표
\“: 큰 따옴표
\b: 백스페이스
\n: 줄 바꿈
\r: 리턴
\t: tab
\z: ASCII 26 (Ctrl + Z)
\\: 백슬래시 \
\%: \%
\_: _
```

### Numeric Literals
숫자 리터럴에는 integer, Decimal 및 부동 소수점 리터럴이 포함됩니다.
integer는 소수점 구분 기호`.`를 포함할 수 있는 일련의 숫자로 표시됩니다. 숫자 리터럴 앞에 `-`또는`+`가 붙어 각각 음수 또는 양수 값을 나타낼 수 있습니다.
정확한 값 숫자 리터럴은 `1, .2, 3.4, -5, -6.78, +9.10`과 같이 나타낼 수 있습니다.
과학적 표기법 예시: `1.2E3, 1.2E-3, -1.2E3, -1.2E-3`.

### Date and Time Literals
TDSQL은 다음 DATE 형식을 지원합니다.
```
'YYYY-MM-DD' or 'YY-MM-DD'
'YYYYMMDD' or 'YYMMDD'
YYYYMMDD or YYMMDD

예시: '2012-12-31', '2012/12/31', '2012^12^31',  '2012@12@31'  '20070523' , '070523' 
```

TDSQL은 다음 DATETIME 및 TIMESTAMP 형식을 지원합니다.
```
'YYYY-MM-DD HH:MM:SS' or 'YY-MM-DD HH:MM:SS'
'YYYYMMDDHHMMSS' or 'YYMMDDHHMMSS'
YYYYMMDDHHMMSS or YYMMDDHHMMSS 

예시: '2012-12-31 11:30:45', '2012^12^31 11+30+45', '2012/12/31 11*30*45',  '2012@12@31 11^30^45'，19830905132800 
```

### Hexadecimal Literals
TDSQL은 다음 형식을 지원합니다.
```
X'01AF'
X'01af'
x'01AF'
x'01af'
0x01AF
0x01af
```

### Bit-Value Literals
TDSQL은 다음 형식을 지원합니다.
```
b'01'
B'01'
0b01
```

### Boolean Literals
상수 TRUE 및 FALSE는 각각 1 및 0으로 평가됩니다. 상수 이름은 모든 문자로 작성할 수 있습니다.
```
mysql>  SELECT TRUE, true, FALSE, false;
+------+------+-------+-------+
| TRUE | TRUE | FALSE | FALSE |
+------+------+-------+-------+
|    1 |    1 |     0 |     0 |
+------+------+-------+-------+
1 row in set (0.03 sec)
```

### NULL Values
NULL 값은 데이터가 없음을 의미합니다. NULL은 모든 문자에 쓸 수 있습니다. 동의어는 \N(대소문자 구분)입니다.
NULL 값은 숫자 유형의 경우 0, 문자열 유형의 경우 빈 문자열(`''`)과 같은 값과 다릅니다.

## 문자 집합 및 시간대
TDSQL은 MySQL에서 지원하는 모든 문자 집합과 데이터 정렬을 지원합니다.
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

현재 연결의 문자 집합 보기:
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

현재 연결의 문자 집합을 설정합니다.
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

>?TDSQL은 프론트엔드 API를 호출해야만 설정할 수 있는 전역 매개변수 설정을 지원하지 않습니다.

time_zone 변수를 설정하여 시간대 속성 수정을 지원합니다.
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

## 데이터 유형
TDSQL은 숫자, 문자열, 날짜 및 시간, 공간 유형 및 JSON을 포함하여 MySQL에서 지원하는 모든 데이터 유형을 지원합니다.

### 숫자
정수 유형의 경우 INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT 및 BIGINT가 지원됩니다.

| 유형      | 바이트 | 최소값(서명/부호 없음)  | 최대값(서명/부호 없음)                 |
| --------- | ------ | ---------------------- | ---------------------------------------- |
| TINYINT   | 1      | -128/0                 | 127/255                                  |
| SMALLINT  | 2      | -32768/0               | 32767/65535                              |
| MEDIUMINT | 3      | -8388608/0             | 8388607/16777215                         |
| INT       | 4      | -2147483648/0          | 2147483647/4294967295                    |
| BIGINT    | 8      | -9223372036854775808/0 | 9223372036854775807/18446744073709551615 |

부동 소수점 유형의 경우 FLOAT(M,D), REAL(M,D) 또는 DOUBLE PRECISION(M,D) 형식으로 FLOAT 및 DOUBLE이 지원됩니다.

고정 소수점 유형의 경우 DECIMAL 및 NUMERIC은 DECIMAL(M,D) 형식으로 지원됩니다.

### 문자열
TDSQL은 다음 문자열 유형을 지원합니다.
```
CHAR 및 VARCHAR Types
BINARY 및 VARBINARY Types
BLOB 및 TEXT Types
	TINYBLOB，TINYTEXT，MEDIUMBLOB,MEDIUMTEXT，LONGBLOB，LONGTEXT
ENUM Type
SET Type
```

### 날짜와 시간
TDSQL은 다음 날짜 및 시간 유형을 지원합니다.
```
DATE, DATETIME,  TIMESTAMP Types
TIME Type
YEAR Type
```

### 공간 데이터
TDSQL은 다음과 같은 공간 유형을 지원합니다.
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
TDSQL은 JSON 형식의 데이터 저장을 지원하므로 JSON 처리를 보다 효율적으로 수행하는 동시에 오류를 미리 감지할 수 있습니다.
>!다른 유형의 JSON 값은 정렬할 수 없습니다. 예를 들어 string 유형의 JSON 값은 int 유형의 값과 비교할 수 없습니다. 동일한 유형의 JSON 값의 경우 숫자와 string만 비교 및 정렬할 수 있습니다. 다음 SQL 문으로 생성된 테이블에서 `select * from t1 order by t1->"$.key2"`는 정렬된 열에 숫자와 문자열이 모두 포함되어 있기 때문에 지원되지 않습니다.

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



## 지원되는 함수
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

