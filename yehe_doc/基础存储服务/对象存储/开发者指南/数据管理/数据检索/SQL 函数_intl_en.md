## Aggregate Functions

COS Select supports the following aggregate functions:

| Function Name | Parameter Type | Return Type |
| :-------------- | :-------------------------- | :----------------------------------------------------------- |
| AVG(expression) | INT, FLOAT, and DECIMAL | DECIMAL will be returned if the input parameter is of integer type, and FLOAT if float type. The same type as the input parameter will be returned in all other cases. |
| COUNT | - | INT |
| MAX(expression) | INT and DECIMAL | The return value type is the same as that of the input parameter |
| MIN(expression) | INT and DECIMAL | The return value type is the same as that of the input parameter |
| SUM(expression) | INT, FLOAT, DOUBLE, and DECIMAL | INT will be returned if the input parameter is of integer type, and FLOAT if float type. The same type as the input parameter will be returned in all other cases. |

## Condition Functions

COS Select supports the following condition functions:

### COALESCE

The COALESCE function determines the input parameters in sequence and returns the first non-null parameter value. If the input parameters do not include a non-null parameter, the function will return a null value.

#### Syntax

```sql
COALESCE ( expression, expression, ... )
```

> ?Values, arrays, or nested functions of INT, String, and Float types can be passed in for the `expression` parameter.

#### Sample

```shell
COALESCE(1)                -- 1
COALESCE(1, null)          -- 1
COALESCE(null, null, 1)    -- 1
COALESCE(missing, 1)       -- 1
COALESCE(null, 'string')   -- 'string'
COALESCE(null)             -- null
COALESCE(null, null)       -- null
COALESCE(missing)          -- null
COALESCE(missing, missing) -- null
```

### NULLIF

The NULLIF function determines the difference between two parameters passed in. If the two parameters have the same value, NULL will be returned; otherwise, the value of the first parameter passed in will be returned.

#### Syntax

```sql
NULLIF ( expression1, expression2 )
```

> ? Values, arrays, or nested functions of INT, String, and Float types can be passed in for the `expression` parameter.

#### Sample

```shell
NULLIF(1, 2)             -- 1
NULLIF(1, '1')           -- 1
NULLIF(1, NULL)          -- 1
NULLIF(1, 1)             -- null
NULLIF(1.0, 1)           -- null
NULLIF(missing, null)    -- null
NULLIF(missing, missing) -- null
NULLIF([1], [1])         -- null
NULLIF(NULL, 1)          -- null
NULLIF(null, null)       -- null
```

## Conversion Functions

COS Select supports the following conversion functions:

### CAST

The CAST function converts one instance to another instance. The instance can be either a value or a function that can be calculated to a certain value.

#### Syntax

```shell
CAST ( expression AS data_type )
```

> ?
>
> - The `expression` parameter can be a value, an array, an operator, or an SQL function that can be calculated to a certain value.
> - The `data_type` parameter is the data type after conversion, such as INT. For the data types currently supported by COS Select, see [Data Types](https://intl.cloud.tencent.com/document/product/436/32476).

#### Sample

```shell
CAST('2007-04-05T14:30Z' AS TIMESTAMP)
CAST(0.456 AS FLOAT)
```

## Date Functions

COS Select supports the following date functions:

### DATE_ADD

The DATE_ADD function adds a specified time interval to a part (year, month, day, hour, minute, or second) of a specific timestamp and returns a new timestamp.

#### Syntax

```shell
DATE_ADD( date_part, quantity, timestamp )
```

> ?
> - The `date_part` parameter specifies the part of the timestamp to be modified, which can be year, month, day, hour, minute, or second.
> - The `quantity` parameter represents the value to be added, which must be a positive integer.
> - The `timestamp` parameter represents the timestamp to be modified.

#### Sample

```shell
DATE_ADD(year, 5, `2010-01-01T`)                -- 2015-01-01
DATE_ADD(month, 1, `2010T`)                     -- 2010-02T 
DATE_ADD(month, 13, `2010T`)                    -- 2011-02T
DATE_ADD(hour, 1, `2017T`)                      -- 2017-01-01T01:00-00:00
DATE_ADD(hour, 1, `2017-01-02T03:04Z`)          -- 2017-01-02T04:04Z
DATE_ADD(minute, 1, `2017-01-02T03:04:05.006Z`) -- 2017-01-02T03:05:05.006Z
DATE_ADD(second, 1, `2017-01-02T03:04:05.006Z`) -- 2017-01-02T03:04:06.006Z
```

### DATE_DIFF

The DATE_DIFF function compares two valid timestamps and returns the difference between them, which can be displayed in the specified unit of time. If the `date_part` value of timestamp1 is greater than that of timestamp2, a positive number will be returned; otherwise, a negative number will be returned.

#### Syntax

```shell
DATE_DIFF( date_part, timestamp1, timestamp2 )
```

> ?
> - The `date_part` parameter specifies the unit of time which the two timestamps are compared in and can be year, month, day, hour, minute, or second.
> - The `timestamp1` parameter is the first input timestamp.
> - The `timestamp2` parameter is the second input timestamp.

#### Sample

```shell
DATE_DIFF(year, `2010-01-01T`, `2011-01-01T`)            -- 1
DATE_DIFF(year, `2010T`, `2010-05T`)                     -- 4 
DATE_DIFF(month, `2010T`, `2011T`)                       -- 12
DATE_DIFF(month, `2011T`, `2010T`)                       -- -12
DATE_DIFF(day, `2010-01-01T23:00T`, `2010-01-02T01:00T`) -- 0 
```

### EXTRACT

 The EXTRACT function extracts a value in the specified unit of time from a given timestamp.

#### Syntax

```shell
EXTRACT( date_part FROM timestamp )
```

> ?
> - The parameter `date_part` specifies the unit of time to be extracted, which can be year, month, day, hour, minute, or second.
> - The `timestamp` parameter represents the input timestamp.

#### Sample

```shell
EXTRACT(YEAR FROM `2010-01-01T`)                           -- 2010
EXTRACT(MONTH FROM `2010T`)                                -- 1 
EXTRACT(MONTH FROM `2010-10T`)                             -- 10
EXTRACT(HOUR FROM `2017-01-02T03:04:05+07:08`)             -- 3
EXTRACT(MINUTE FROM `2017-01-02T03:04:05+07:08`)           -- 4
EXTRACT(TIMEZONE_HOUR FROM `2017-01-02T03:04:05+07:08`)    -- 7
EXTRACT(TIMEZONE_MINUTE FROM `2017-01-02T03:04:05+07:08`)  -- 8
```

### TO_STRING

The TO_STRING function converts a timestamp to a string of time in the specified format.

#### Syntax

```shell
TO_STRING ( timestamp time_format_pattern )
```

> ?
> - The `timestamp` parameter specifies the timestamp to be converted.
> - The `time_format_pattern` parameter specifies the time format.

| Format | Description | Sample |
| ---------------- | ------------------------------------------------------------ | --------------------------------- |
| yy | 2-digit year | 98 |
| y | 4-digit year | 1998 |
| yyyy | Year expressed by 4 digits. If there are less than 4 digits, 0 will be automatically added | 0199 |
| M | Month | 1 |
| MM | Month expressed by 2 digits. If there are less than 2 digits, 0 will be automatically added | 01 |
| MMM | English abbreviation of a month | Jan |
| MMMM | Full English name of a month | January |
| MMMMM | Initial of a month | J (not applicable to the to_timestamp function) |
| d | Day (1-31) in a month | 1 |
| dd | Day expressed by 2 digits (1-31) | 01 |
| a | Symbol for morning or afternoon (AM/PM) | AM |
| h | Hour in 12-hour time | 1 |
| hh | Hour expressed by 2 digits in 12-hour time | 01 |
| H | Hour in 24-hour time | 1 |
| HH | Hour expressed by 2 digits in 24-hour time | 01 |
| m | Minute (00-59) | 1 |
| mm | Minute expressed by 2 digits in 24-hour time | 01 |
| s | Second (00-59) | 1 |
| ss | Second expressed by 2 digits in 24-hour time | 01 |
| S | Decimal part of the second (accuracy: 0.1; value range: 0.0 - 0.9) | 0 |
| SS | Decimal part of the second (accuracy: 0.01; value range: 0.00 - 0.99) | 6 |
| SSS | Decimal part of the second (accuracy: 0.001; value range: 0.000 - 0.999) | 60 |
| ...              | ...                                                          | ...                               |
| SSSSSSSSS | Decimal part of the second (accuracy: 0.000000001; value range: 0.000000000 - 0.999999999) | 60000000 |
| n | Nanosecond | 60000000 |
| X | Hour-level offset. If the offset is 0, then this will be "Z" | +01 or Z |
| XX or XXXX | Hour- or minute-level offset. If the offset is 0, then this will be "Z" | +0100 or Z |
| xxx or xxxxx | Hour- or minute-level offset. If the offset is 0, then this will be "Z" | +01:00 or Z |
| x | Hour-level offset | 1 |
| xx or xxxx | Hour- or minute-level offset | 0100 |
| xxx or xxxxx | Hour- or minute-level offset | 01:00 |

#### Sample

```shell
TO_STRING(`1998-07-20T20:18Z`,  'MMMM d, y')                    -- "July 20, 1998"
TO_STRING(`1998-07-20T20:18Z`, 'MMM d, yyyy')                   -- "Jul 20, 1998"
TO_STRING(`1998-07-20T20:18Z`, 'M-d-yy')                        -- "7-20-69"
TO_STRING(`1998-07-20T20:18Z`, 'MM-d-y')                        -- "07-20-1998"
TO_STRING(`1998-07-20T20:18Z`, 'MMMM d, y h:m a')               -- "July 20, 1998 8:18 PM"
TO_STRING(`1998-07-20T20:18Z`, 'y-MM-dd''T''H:m:ssX')           -- "1998-07-20T20:18:00Z"
TO_STRING(`1998-07-20T20:18+08:00Z`, 'y-MM-dd''T''H:m:ssX')     -- "1998-07-20T20:18:00Z"
TO_STRING(`1998-07-20T20:18+08:00`, 'y-MM-dd''T''H:m:ssXXXX')   -- "1998-07-20T20:18:00+0800"
TO_STRING(`1998-07-20T20:18+08:00`, 'y-MM-dd''T''H:m:ssXXXXX')  -- "1998-07-20T20:18:00+08:00"
```

### TO_TIMESTAMP

 The TO_TIMESTAMP function converts a string of time to a timestamp.

#### Syntax

```shell
TO_TIMESTAMP ( string )
```

> ? The `string` parameter represents the input time string.

#### Sample

```shell
TO_TIMESTAMP('2007T')                         -- `2007T`
TO_TIMESTAMP('2007-02-23T12:14:33.079-08:00') -- `2007-02-23T12:14:33.079-08:00`
```

### UTCNOW

 The UTCNOW function returns the current timestamp in UTC.

#### Syntax

```
UTCNOW()
```

#### Sample

```shell
UTCNOW() -- 2019-01-01T14:23:12.123Z
```

## String Functions

COS Select supports the following string functions:

### CHAR_LENGTH, CHARACTER_LENGTH

Both CHAR_LENGTH and CHARACTER_LENGTH can compute the number of characters in a string, and they have the same semantics.

#### Syntax

```shell
CHAR_LENGTH ( string )
```

> ? The `string` parameter specifies the string for character counting

#### Sample

```shell
CHAR_LENGTH('null')      -- 4
CHAR_LENGTH('tencent')   -- 7
```

### LOWER

 The LOWER function converts all uppercase letters in the specified string to lowercase letters, with all non-uppercase letters left unchanged.

#### Syntax

```shell
LOWER ( string )
```

> ? The `string` parameter specifies the string for which to convert uppercase letters to lowercase letters.

#### Sample

```shell
LOWER('TENcent') -- 'tencent'
```

### SUBSTRING

 The SUBSTRING function returns a substring of a string. You can specify an index from which the SUBSTRING function will extract the remainder of the original string based on the length of the specified substring and return the result.

>? If the input string contains only 1 character, and the index is set to be greater than 1, the SUBSTRING function will automatically switch it to 1.
>

#### Syntax

```shell
SUBSTRING( string FROM start [ FOR length ] )
```

> ?
> - The `string` parameter specifies the string from which to extract a substring.
> - The `start` parameter represents an index value of the string as the starting position for extraction.
> - The `length` parameter specifies the length of the substring. If the length of the substring is not specified, the remainder of the string will be extracted.

#### Sample

```shell
SUBSTRING("123456789", 0)      -- "123456789"
SUBSTRING("123456789", 1)      -- "123456789"
SUBSTRING("123456789", 2)      -- "23456789"
SUBSTRING("123456789", -4)     -- "123456789"
SUBSTRING("123456789", 0, 999) -- "123456789" 
SUBSTRING("123456789", 1, 5)   -- "12345"
```

### TRIM

 The TRIM function deletes all characters before the first character or after the last character of the specified string. " " is the default character to be deleted.

#### Syntax

```shell
TRIM ( [[LEADING | TRAILING | BOTH remove_chars] FROM] string )
```

> ?
> -  The `string` parameter specifies the string to be manipulated.
> - The `LEADING | TRAILING | BOTH` parameter specifies the extra characters to be deleted, which can be before the string (LEADING), after the string (TRAILING), or both (BOTH).
> - The `remove_chars` parameter specifies the type of extra characters to be deleted. It can be a string containing more than one characters. The TRIM function will delete all extra characters of the corresponding type that are identified by the TRIM function before or after the `string` parameter.

#### Sample

```shell
TRIM('       foobar         ')               -- 'foobar'
TRIM('      \tfoobar\t         ')            -- '\tfoobar\t'
TRIM(LEADING FROM '       foobar         ')  -- 'foobar'
TRIM(TRAILING FROM '       foobar         ') -- 'foobar'
TRIM(BOTH FROM '       foobar         ')     -- 'foobar'
TRIM(BOTH '12' FROM '1112211foobar22211122') -- 'foobar'
```

### UPPER

 The UPPER function converts all lowercase letters to uppercase letters with non-lowercase letters left unchanged.

#### Syntax

```shell
UPPER ( string )
```

> ? The `string` parameter specifies the string to be converted to uppercase letters.

#### Sample

```shell
UPPER('tenCENT') -- 'TENCENT'
```

