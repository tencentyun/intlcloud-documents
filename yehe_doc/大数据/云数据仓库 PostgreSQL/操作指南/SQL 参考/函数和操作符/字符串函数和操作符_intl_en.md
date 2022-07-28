
Common string functions are as listed below:

| Function | Return Type | Description | Example | Result |
| --------------------------------------- | ------ | -------------------------- | ----------------------------------------------- | ---------- |
| string \|\| string                        | text   | String concatenation                 | 'Post' \|\| 'greSQL'                            | PostgreSQL |
| string \|\| non-string or non-string \|\| string    | text   | String concatenation with one non-string input | 'Value: ' \|\| 42                               | Value: 42  |
| bit_length(string)               | int    | Number of bits in string              | bit_length('jose')                              | 32         |
| char_length(string) or character_length(string)     | int    | Number of characters in string             | char_length('jose')                             | 4          |
| lower(string)               | text   | Converts string to lower case               | lower('TOM')                                    | tom        |
| octet_length(string)           | int    | Number of bytes in string             | octet_length('jose')                            | 4          |
| overlay(string placing string from int [for int])    | text   | Replaces substring               | overlay('Txxxxas' placing 'hom'   from 2 for 4) | Thomas     |
| position(substring in string)        | int    | Location of specified substring   | position('om' in 'Thomas')                      | 3          |
| substring(string [from int]   [for int])     | text   | Extracts substring               | substring('Thomas' from 2 for 3)                | hom        |
| substring(string from pattern)       | text   | Extracts substring matching regular expression           | substring('Thomas' from '...$')                 | mas        |
| trim([leading \| trailing \| both]   [characters] fromstring) | text   | Removes substring               | trim(both 'x' from 'xTomxx')       | Tom        |
| upper(string)                | text   | Converts string to upper case               | upper('tom')                                    | TOM        |


The database also provides some other string functions for processing strings as listed below:


| Function | Return Type | Description | Example | Result |
| -------------------- | ------ | -------------------------------- | ----------------------- | ------------------------------------------- |
| ascii(string)              | int    | Gets the ASCII code of the first character            | ascii('x')               | 120                     |
| btrim(string text [, characters text])    | text   | Removes the longest string consisting only of characters in characters (a space by default) from the start and end of string | btrim('xyxtrimyyx',   'xy')      | trim                                                       |
| chr(int)     | text   | Converts ASCII code to character              | chr(65)                    | A               |
| convert(string bytea, src_encodingname, dest_encoding name)  | bytea  | Converts encoding by using the specified conversion name | convert('text_in_utf8',   'UTF8', 'LATIN1') | -     |
| convert_from(string bytea,src_encoding name)                 | text   | Converts to the database's default encoding   | convert_from('text_in_utf8',   'UTF8')      | text_in_utf8represented   in the current database encoding |
| convert_to(string text, dest_encodingname)   | bytea  | Converts to data encoded in a certain format  | convert_to('some   text', 'UTF8')      |    -    |
| decode(string text, type text)   | bytea  | Decodes data    | decode('MTIzAAE=',   'base64')              | 123\000\001        |
| encode(data bytea, type text)   | text   | Encodes data         | encode(E'123\\000\\001',   'base64')        | MTIzAAE=             |
| initcap(string)     | text   | Converts the first letter of each word to upper case and the rest to lower case    | initcap('hi   THOMAS')        | Hi   Thomas        |
| length(string)          | int    | Number of characters in string | length('jose')  | 4       |
| length(stringbytea, encoding name )      | int    | Number of characters in string in the specified encoding  | length('jose',   'UTF8')   | 4          |
| ltrim(string text [, characters text])  | text   | Removes the longest string containing only characters from characters (a space by default) from the start of string | ltrim('zzzytrim',   'xyz')    | trim        |
| md5(string)      | text   | Calculates the MD5 hash of string     | md5('abc')        | 900150983cd24fb0   d6963f7d28e17f72         |
| pg_client_encoding()       | name   | Gets client encoding name         | pg_client_encoding()      | SQL_ASCII           |
| regexp_replace(string text, patterntext, replacement text [, flags text]) | text   |       -   | regexp_replace('Thomas',   '.[mN]a.', 'M')  | ThM    |
| repeat(string text, n int)  | text   | Repeats string n times      | repeat('Pg',   4)                           | PgPgPgPg              |
| replace(string text, from text, totext)    | text   | Replaces string  | replace('abcdefabcdef',   'cd', 'XX')       | abXXefabXXef          |
| rtrim(string text [, characters text])     | text   | Removes the longest string containing only characters from characters (a space by default) from the end of string | rtrim('trimxxxx',   'x')    | trim              |
| strpos(string, substring)    | int    | Gets the location of substring      | strpos('high',   'ig')           | 2                           |
| substr(string, from [, count])       | text   | Gets substring         | substr('alphabet',   3, 2)      | ph                     |
| to_ascii(string text [, encodingtext])     | text   | Converts to ASCII code       | to_ascii('Karel')        | Karel              |
| to_hex(number int or bigint)                                 | text   | Converts number to its equivalent hexadecimal representation            | to_hex(2147483647)     | 7fffffff         |

