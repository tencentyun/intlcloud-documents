The names and features of string operation functions are as follows:

| Function Name | Feature Description |
| ----- | ----- |
| string1 &#124;  &#124;  string2 | Connects two strings. |
| CHAR_LENGTH(string) | Returns the length of a string. |
| CHARACTER_LENGTH(string)  | Returns the length of a string. |
| UPPER(string) | Returns the string in uppercase. |
| LOWER(string) | Returns the string in lowercase. |
| POSITION(string1 IN string2)  | Queries string1's first occurrence position in string2. |
| TRIM( { BOTH &#124; LEADING &#124; TRAILING } string1 FROM string2)| Removes string1 from the beginning and/or end of string2. By default, spaces at both ends are removed. |
| OVERLAY(string1 PLACING string2 FROM start_pos [ FOR length ])  | Replaces the string1's substring starting from start_pos with string2. You can specify the length of the substring to be replaced. |
| SUBSTRING(string from pos) [ FOR length]  | Queries the substring starting from pos. You can specify the length of the substring by using "FOR". The default query length is from pos to the end of the original string. |
| INITCAP(string) | Converts the initial letter of a string to uppercase, and the rest of letters to lowercase. Words are separated by non-alphanumeric characters. |
| CONCAT(string1, string2 ...)  | Connects multiple strings. If any string is null, the result is null. |
| CONCAT_WS(separator, string1, string2, ...) | Connects multiple strings using the specified separator. If Separator is null, the result is null. "NULL" strings are skipped, while empty strings are not. For example, if the function is CONCAT_WS("~", "AA","BB", "", "CC"), AA~BB~\~CC is returned. |
| LPAD(text, length, padding) | Populates the "text" string using a string specified by "padding" from the left to a specified length. If "text" exceeds the specified length, it is truncated to this length. |
| RPAD(text, length, padding) | Populates the "text" string using a string specified by "padding" from the right to a specified length. If "text" exceeds the specified length, it is truncated to this length. |
| UNBASE64(string) | Decodes the Base64 encoded string into a byte array Byte[]. To decode it to a string, nest it with DECODE() method, or use the UNBASE64_TO_STRING() function shown below. |
| UNBASE64_TO_STRING(string) or UNBASE64_TO_STRING(string, charset) | Decodes the Base64 encoded string (i.e. "string" in the function) into an actual string, just like DECODE(UNBASE64(string), charset).<br>**Note:** If the character set "charset" is not explicitly specified, it is UTF-8 encoding by default. |
| BASE64(binary) | Encodes a byte array Byte[] (i.e. "binary" in the function) into a Base64 encoded string. |
| BASE64_FROM_STRING(string) or BASE64_FROM_STRING(string, charset) | Encodes the string in Base64, just like BASE64(ENCODE(string, charset)).<br>**Note:** If the character set "charset" is not explicitly specified, it is UTF-8 encoding by default. |
| ENCODE(string) or ENCODE(string, charset) | Encodes a string into a Byte[] array using the character set specified by "charset". For example, ENCODE(st, 'GBK').<br>**Note:** If the character set "charset" is not explicitly specified, it is UTF-8 encoding by default. |
| DECODE(string) or DECODE(binary, charset) | Decodes a byte array Byte[] (i.e. "binary" in the function) with the character set specified by "charset". For example, DECODE(binary_field, 'GB2312').<br>**Note:** If the character set "charset" is not explicitly specified, it is UTF-8 encoding by default. |
| SPLIT_INDEX(string, separator, index)  | Split the string with specified separators, and gets the index-th element. index counts from 0. |


