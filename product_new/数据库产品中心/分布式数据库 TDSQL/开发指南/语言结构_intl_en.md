
> If you want to view or download the full set of development documents, see [Development Guide for TDSQL](https://intl.cloud.tencent.com/document/product/1042/33352).

### Language Structure

**TDSQL supports all literal formats used by MySQL. The following examples are just for illustration and do not mean that the ones supported by TDSQL are different from those supported by MySQL.**
```
	String Literals
	Numeric Literals
	Date and Time Literals
	Hexadecimal Literals
	Bit-Value Literals
	Boolean Literals
	NULL Values
```
#### String Literals

A string literal is a sequence of bytes or characters surrounded by single quotation mark (') or double quotation mark ("). Currently, TDSQL does not support ANSI_QUOTES SQL MODE. Things surrounded by double quotation marks (") are always considered string literals instead of identifiers.
character set introducer is not supported, i.e., the format of `[_charset_name]'string' [COLLATE collation_name]`
Supported escape characters are as follows:
```
	\0: ASCII NUL (X’00’) character
	\': single quotation mark
	\": double quotation mark
	\b: Backspace character
	\n: Link break
	\r: Carriage return
	\t: Tab
	\z: ASCII 26 (Ctrl + Z)
	\\: backslash\
	\%: \%
	\_: _
```

#### Numeric Literals

Numeric literals include integers, decimal-point numbers, and floating-point numbers.
An integer may include a decimal separator "." and begin with a plus sign "+" or a minus sign "-" to indicate whether it is a positive or negative number.
The exact numeric literal can be expressed as follows: 1, .2, 3.4, -5, -6.78, +9.10.
Scientific notation: 1.2E3, 1.2E-3, -1.2E3, -1.2E-3.

#### Date and Time Literals

Supported DATE formats are as follows:
```
	'YYYY-MM-DD' or 'YY-MM-DD'
	'YYYYMMDD' or 'YYMMDD'
	YYYYMMDD or YYMMDD
```
Examples: '2012-12-31', '2012/12/31', '2012^12^31',  '2012@12@31'  '20070523', '070523'

Supported DATETIME and TIMESTAMP formats are as follows:
```
	'YYYY-MM-DD HH:MM:SS' or 'YY-MM-DD HH:MM:SS'
	'YYYYMMDDHHMMSS' or 'YYMMDDHHMMSS'
	YYYYMMDDHHMMSS or YYMMDDHHMMSS
```
Examples, '2012-12-31 11:30:45', '2012^12^31 11+30+45', '2012/12/31 11*30*45', '2012@12@31 11^30^45', 19830905132800

#### Hexadecimal Literals

Supported formats are as follows:
```
	X'01AF'
	X'01af'
	x'01AF'
	x'01af'
	0x01AF
	0x01af
```
#### Bit-Value Literals

Supported formats are as follows:
```
	b'01'
	B'01'
	0b01
```
#### Boolean Literals

Constants `TRUE` and `FALSE` are equal to 1 and 0 respectively, which are case-insensitive.
```
	mysql>  SELECT TRUE, true, FALSE, false;
	+------+------+-------+-------+
	| TRUE | TRUE | FALSE | FALSE |
	+------+------+-------+-------+
	|    1 |    1 |     0 |     0 |
	+------+------+-------+-------+
	1 row in set (0.03 sec)
```
#### NULL Values

Null is an absence of a value. It is case-insensitive and has the same meaning as \N (case-sensitive).
Note that NULL is not the same as 0 or the empty string ('').
