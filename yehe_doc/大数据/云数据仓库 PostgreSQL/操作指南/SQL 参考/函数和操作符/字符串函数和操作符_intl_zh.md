
这一部分主要是讲字符串的一些操作函数，具体见下列表格。

| 函数                                        | 返回值 | 描述                       | 示例                                            | 结果       |
| --------------------------------------- | ------ | -------------------------- | ----------------------------------------------- | ---------- |
| string \|\| string                        | text   | 字符串连接                 | 'Post' \|\| 'greSQL'                            | PostgreSQL |
| string \|\| non-string or non-string \|\| string    | text   | 字符串和非字符串之间的连接 | 'Value: ' \|\| 42                               | Value: 42  |
| bit_length(string)               | int    | 字符串的 bit 数              | bit_length('jose')                              | 32         |
| char_length(string) or character_length(string)     | int    | 字符串的字符数             | char_length('jose')                             | 4          |
| lower(string)               | text   | 转为小写字符               | lower('TOM')                                    | tom        |
| octet_length(string)           | int    | 字符串的字节数             | octet_length('jose')                            | 4          |
| overlay(string placing string from int [for int])    | text   | 替换子字符串               | overlay('Txxxxas' placing 'hom'   from 2 for 4) | Thomas     |
| position(substring in string)        | int    | 子字符串在字符串中的位置   | position('om' in 'Thomas')                      | 3          |
| substring(string [from int]   [for int])     | text   | 截取子字符串               | substring('Thomas' from 2 for 3)                | hom        |
| substring(string from pattern)       | text   | 正则匹配子字符串           | substring('Thomas' from '...$')                 | mas        |
| trim([leading \| trailing \| both]   [characters] fromstring) | text   | 移除子字符串               | trim(both 'x' from 'xTomxx')       | Tom        |
| upper(string)                | text   | 转为大写字母               | upper('tom')                                    | TOM        |


数据库还提供一些其他的字符串函数，用于支持对字符串的处理，见下面的表格。


| 函数                                | 返回值 | 功能                                | 示例                         | 结果                              |
| -------------------- | ------ | -------------------------------- | ----------------------- | ------------------------------------------- |
| ascii(string)              | int    | 获取第一个字符的 ASCII 码            | ascii('x')               | 120                     |
| btrim(string text [, characters text])    | text   | 从 string 开头和结尾（而非中间）删除只包含在 characters 里（缺省是空白）的字符的最长字符串 | btrim('xyxtrimyyx',   'xy')      | trim                                                       |
| chr(int)     | text   | ASCII 码转字符              | chr(65)                    | A               |
| convert(string bytea, src_encodingname, dest_encoding name)  | bytea  | 使用指定的转换名字改变编码 | convert('text_in_utf8',   'UTF8', 'LATIN1') | -     |
| convert_from(string bytea,src_encoding name)                 | text   | 转换为数据库默认的编码格式   | convert_from('text_in_utf8',   'UTF8')      | text_in_utf8represented   in the current database encoding |
| convert_to(string text, dest_encodingname)   | bytea  | 转换为编码为某种格式的数据  | convert_to('some   text', 'UTF8')      |    -    |
| decode(string text, type text)   | bytea  | 解码函数    | decode('MTIzAAE=',   'base64')              | 123\000\001        |
| encode(data bytea, type text)   | text   | 编码函数         | encode(E'123\\000\\001',   'base64')        | MTIzAAE=             |
| initcap(string)     | text   | 每个单词的第一个字母大小，其余小写    | initcap('hi   THOMAS')        | Hi   Thomas        |
| length(string)          | int    | 字符串长度| length('jose')  | 4       |
| length(stringbytea, encoding name )      | int    | 指定编码格式的字符串长度  | length('jose',   'UTF8')   | 4          |
| ltrim(string text [, characters text])  | text   | 从 string 开头（而非中间）删除只包含在 characters 里（缺省是空白）的字符的最长字符串 | ltrim('zzzytrim',   'xyz')    | trim        |
| md5(string)      | text   | 计算字符串的 MD5 值     | md5('abc')        | 900150983cd24fb0   d6963f7d28e17f72         |
| pg_client_encoding()       | name   | 获取客户端的编码格式         | pg_client_encoding()      | SQL_ASCII           |
| regexp_replace(string text, patterntext, replacement text [, flags text]) | text   |       -   | regexp_replace('Thomas',   '.[mN]a.', 'M')  | ThM    |
| repeat(string text, n int)  | text   | 重复 n 次字符串      | repeat('Pg',   4)                           | PgPgPgPg              |
| replace(string text, from text, totext)    | text   | 替换字符串  | replace('abcdefabcdef',   'cd', 'XX')       | abXXefabXXef          |
| rtrim(string text [, characters text])     | text   | 从 string 结尾（而非中间）删除只包含在 characters 里（缺省是空白）的字符的最长字符串 | rtrim('trimxxxx',   'x')    | trim              |
| strpos(string, substring)    | int    | 获取子串的位置      | strpos('high',   'ig')           | 2                           |
| substr(string, from [, count])       | text   | 获取子串         | substr('alphabet',   3, 2)      | ph                     |
| to_ascii(string text [, encodingtext])     | text   | 转为 ASCII 码格式       | to_ascii('Karel')        | Karel              |
| to_hex(number int or bigint)                                 | text   | 将数字转为16进制            | to_hex(2147483647)     | 7fffffff         |

