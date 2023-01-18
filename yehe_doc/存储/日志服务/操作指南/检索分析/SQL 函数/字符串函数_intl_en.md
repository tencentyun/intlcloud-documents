This document introduces the basic syntax and examples of string functions.

>!
> - Strings must be included in single quotation marks `''`, while characters that are unsigned or included in double quotation marks `""` indicate field or column names. For example, `'status'` indicates the string `status`, while `status` or `"status"` indicates the log field `status`.
> - When a string contains a single quotation mark `'`, you need to use `''` (two single quotation marks) to represent the single quotation mark itself. For example `'{''version'': ''1.0''}'` indicates the raw string {'version': '1.0'}. No special processing is required if the string itself contains a double quotation mark `"`.
> - In the following functions, all the `key` parameters indicate log field names.
> 


| Function                             | Description                                                         | Example                                                         |
| ------------------------------------ | ------------------------------------------- | ------------------------------------------ |
| chr(number) [](id:chr)                         |Returns characters that match the ASCII code point (bit) specified by the input parameter. The return value is of the VARCHAR type. | Return characters that match ASCII code bit 77:</br> `* \| SELECT chr(77)`   |
| codepoint(string)[](id:codepoint)                    |Converts ASCII field values to BIGINT values. The return value is of the integer type. | Convert character values in ASCII code to their corresponding positions:</br> `* \| SELECT codepoint('M')` |
| concat(key1, ..., keyN)[](id:concat)              |Concatenates strings key1, key2, ...keyN. The concatenation effect is consistent with that of the \|\| connectors. The return value is of the VARCHAR type. Note that when the random string is `null`, the return value is `null`. To skip `null`, use `concat_ws`. | Concatenate multiple strings into one:</br> `* \| SELECT concat(remote_addr, host, time_local)` |
| concat_ws(split_string,key0, ..., keyN)[](id:concat_ws_1)|Concatenates strings key1, key2, ...keyN using `split_string` as the separator. `split_string` can be a string or variable. If `split_string` is null, null values in key1, key2, ...keyN are skipped. The return result is of the VARCHAR type. | Concatenate multiple strings using / as the separator:</br>`* \| SELECT concat_ws('/', remote_addr,host,time_local)` |
| concat_ws(split_string, array(varchar))[](id:concat_ws_2) |Concatenates elements in an array into a string using `split_string` as the separator. If `split_string` is `null`, the result is null and null values in the array are skipped. The return result is of the VARCHAR type.</br> Note: In this function, the `array(varchar)` parameter is an array, not a string. | Concatenate elements in an array into a string using # as the separator: (in this example, the output of the `split` function is an array)</br>`* \| select concat_ws('#',split('cloud.tencent.com/product/cls', '/'))` |
| format(format，args...)[](id:format)              |Formats the output of the `args` parameter using the `format` format. The return value is of the VARCHAR type. | Format the output of the `remote_addr` and `host` parameters using the format of `IP address: %s, Domain name: %s`:</br> `* \| SELECT format('IP address: %s, Domain name: %s', remote_addr, host)  ` |
| hamming_distance(key1, key2)[](id:hamming_distance)|Returns the Hamming distance between the `key1` and `key2` strings. Note that the two strings must have the same length. The return value is of the BIGINT type. | Return the Hamming distance between the `remote_addr` and `remote_addr` strings:</br> `* \| SELECT hamming_distance(remote_addr, remote_addr)     ` |
| length(key) [](id:length)                         |Returns the length of a string. The return value is of the BIGINT type. | Return the length of the `http_user_agent` string:</br> `* \| SELECT length(http_user_agent)      ` |
| levenshtein_distance(key1, key2)[](id:levenshtein_distance)|Returns the Levenshtein distance between the `key1` and `key2` strings. The return value is of the BIGINT type.       | Return the Levenshtein distance between the `remote_addr` and `http_protocol` strings:</br> `* \| SELECT levenshtein_distance(remote_addr, http_protocol)            ` |
| lower(key)[](id:lower)                           |Converts a string to lowercase. The return value is of the VARCHAR type in lowercase.   | Convert the `http_protocol` string to lowercase:</br> `* \| SELECT lower(http_protocol)            ` |
| lpad(key, size, padstring)[](id:lpad)           |Left pads `padString` to a string to `size` characters. If `size` is less than the length of `key`, the result is truncated to `size` characters. `size` must be non-negative, and `padstring` must be non-empty. The return value is of the VARCHAR type. | Left pad the '0' to the `remote_addr` string to 32 characters:</br> `* \| SELECT lpad(remote_addr, 32, '0')            ` |
| ltrim(key)[](id:ltrim)                           |Removes all leading whitespace characters from a string. The return value is of the VARCHAR type.            |  Remove all leading whitespace characters from the `http_user_agent` string:</br> `* \| SELECT ltrim(http_user_agent)            ` |
| position(substring IN key)[](id:position)           |Returns the position of `substring` in a string. Positions start with 1. If the position is not found, `0` is returned. This function takes the special syntax `IN` as a parameter. For other information, see strpos(). The return value is of the BIGINT type. | Return the position of the 'G' characters in `http_method`:</br> `* \| select position('G' IN http_method)      ` |
| replace(key, substring) [](id:replace_1)             |Removes all `substring` from the `key` string. The return value is of the VARCHAR type.     | Remove all 'Oct' from the `time_local` string:</br> `* \| select replace(time_local, 'Oct')            ` |
| replace(key, substring, replace)[](id:replace_2)     |Replaces all `substring` in a string with the `replace` string. The return value is of the VARCHAR type. | Replace all 'Oct' in the `time_local` string with '10':</br> `* \| select replace(time_local,'Oct','10')            ` |
| reverse(key)[](id:reverse)                         |Reverses the `key` string. The return value is of the VARCHAR type.                       | Reverse the `host` string: </br> `* \| select reverse(host)            ` |
| rpad(key, size, padstring) [](id:rpad)          |**Right** pads `padstring` to a string to `size` characters. If `size` is less than the length of `key`, the result is truncated to `size` characters. `size` must be non-negative, and `padstring` must be non-empty. The return value is of the VARCHAR type. | Right pad '0' to the `remote_addr` string to 32 characters:</br> `* \| select rpad(remote_addr, 32, '0')            ` |
| rtrim(key) [](id:rtrim)                          |Removes all trailing whitespace characters from a string. The return value is of the VARCHAR type.          | Remove all trailing whitespace characters from the `http_user_agent` string:</br> `* \| select rtrim(http_user_agent)            ` |
| split(key, delimiter)[](id:split_1)                |Splits a string using a specified delimiter and returns a string array.             | Split the `http_user_agent` string using the '/' delimiter and return a string array:</br> `* \| SELECT split(http_user_agent, '/')            ` |
| split(key, delimiter, limit)[](id:split_2)         |Splits a string using a specified delimiter and returns a string array with the maximum length specified by `limit`. The last element in the string array always contains all the remaining part of `key`. `limit` must be a positive integer. | Split the `http_user_agent` string using the '/' delimiter and return a string array with the length of 10 characters:</br> `* \| SELECT split(http_user_agent, '/', 10)            ` |
| split_part(key, delimiter, index)[](id:split_part)    |Splits a string using a specified delimiter and returns the string at the `index` position in the array. Indexes start with 1. If the value of `index` is greater than the length of the array, `null` is returned. The return value is of the VARCHAR type. | Split the `http_user_agent` string using the '/' delimiter and return the string at position 1:</br> `* \| SELECT split_part(http_user_agent, '/', 1)` |
| strpos(key, substring) [](id:strpos_1)              |Returns the position of `substring` in a string. Positions start with 1. If the position is not found, `0` is returned. The return value is of the BIGINT type. | Return the position of 'org' in the `host` string:</br> `* \| SELECT strpos(host, 'org')            ` |
| strpos(key, substring, instance)[](id:strpos_2)     |Returns the position of the N-th `instance` of `substring` in the string. If `instance` is a negative number, the position is counted starting from the end of the string. Positions start with 1. If the position is not found, `0` is returned. The return value is of the BIGINT type. | Return the position of the first instance of 'g' in the `host` string:</br> `* \| SELECT strpos(host, 'g', 1)            ` |
| substr(key, start) [](id:substr_1)                  |Returns the rest of a string from the starting position `start`. Positions start with 1. A negative starting position is interpreted as being relative to the end of the string, for example, [...]. The return value is of the VARCHAR type. | Return the rest of the `remote_user` string from the second character:</br> `* \| SELECT substr(remote_user, 2)            ` |
| substr(key, start,  length)[](id:substr_2)          |Returns a substring from a string of `length` length from the starting position `start`. Positions start with 1. A negative starting position is interpreted as being relative to the end of the string. The return value is of the VARCHAR type. | Return the 2nd to 5th characters of the `remote_user` string:</br> `* \| SELECT substr(remote_user, 2, 5)            ` |
| translate(key, from, to)[](id:translate)             |Replaces all characters in `key` that appear in `from` with characters at the corresponding position in `to`. If `from` contains repeated characters, only the first character is counted. If the characters in `from` do not exist in the source, the source is copied directly. If the length of `from` is greater than that of `to`, the corresponding characters will be deleted. The return value is of the VARCHAR type. | Replace the '123' characters in the `remote` string with the 'ABC' characters:</br> `* \| SELECT translate(remote_user, '123', 'ABC')            ` |
| trim(key) [](id:trim)                           |Removes leading and trailing whitespace characters from a string. The return value is of the VARCHAR type.          | Remove leading and trailing whitespace characters from the `http_cookies` string:</br> `* \| SELECT trim(http_cookies)            ` |
| upper(key)[](id:upper)                           |Converts a string to uppercase. The return value is of the VARCHAR type in uppercase.   | Convert the lowercase characters in the `host` string to uppercase characters:</br> `* \| SELECT upper(host)            ` |
| word_stem(word)[](id:word_stem_1)                      |Returns the stem of `word` in the English language. The return value is of the VARCHAR type.                  | Return the English word of 'Mozilla':</br> `* \| SELECT word_stem('Mozilla')      ` |
| word_stem(word, lang) [](id:word_stem_2)|Returns the stem of `word` in the `lang` language. The return value is of the VARCHAR type.              | Return the stem of `selects` in English:</br> `* \| SELECT word_stem('selects', 'en')            ` |

#### Unicode functions

| Function                   | Description                                                         |
| -------------------------- | ------------------------------------------------------------ |
| normalize(string)[](id:normalize_1)          | Converts a string to the NFC standard format. The return value is of the VARCHAR type.             |
| normalize(string, form) [](id:normalize_2)    | Converts `string` to the `form` format. The `form` parameter must be keywords (NFD, NFC, NFKD, or NFKC) instead of a string. The return value is of the VARCHAR type. |
| to_utf8(string)  [](id:to_utf8)            | Converts `string` to a UTF-8 binary string varbinary. The return value is of the VARCHAR type. |
| from_utf8(binary)  [](id:from_utf8_1)         | Converts a binary string to a UTF-8 string. Invalid UTF-8 characters will be replaced with "U+FFFD". The return value is of the VARCHAR type. |
| from_utf8(binary, replace)[](id:from_utf8_2) | Converts a binary string to a UTF-8 string. Invalid UTF-8 characters will be replaced with `replace`. The return value is of the VARCHAR type. |


#### Examples

This section provides samples of the query and analysis statements based on the following log example.
Raw log data sample:
```
10.135.46.111 - - [05/Oct/2015:21:14:30 +0800] "GET /my/course/1 HTTP/1.1" 127.0.0.1 200 782 9703 "http://127.0.0.1/course/explore?filter%5Btype%5D=all&filter%5Bprice%5D=all&filter%5BcurrentLevelId%5D=all&orderBy=studentNum" "Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0"  0.354 0.354
```
After configuring the "Single-line - Full regular expression" collection mode, custom key names are as follows:
```
body_bytes_sent: 9703
http_host: 127.0.0.1
http_protocol: HTTP/1.1
http_referer: http://127.0.0.1/course/explore?filter%5Btype%5D=all&filter%5Bprice%5D=all&filter%5BcurrentLevelId%5D=all&orderBy=studentNum
http_user_agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0
remote_addr: 10.135.46.111
request_length: 782
request_method: GET
request_time: 0.354
request_url: /my/course/1
status: 200
time_local: [05/Oct/2015:21:14:30 +0800]
upstream_response_time: 0.354
```

Analysis statement sample:
- Split the value of the **request_url** field using the question mark (?), return the first string (the file path part), and then count the number of requests corresponding to different paths:
```
* | SELECT count(*) AS pv, split_part(request_url, '?', 1) AS Path GROUP BY Path ORDER BY pv DESC LIMIT 3
```

- Extract the first 4 characters (the HTTP part) of the value of the **http_protocol** field, and then count the number of requests corresponding to the HTTP protocol:
```
* | SELECT substr(http_protocol,1,4) AS http_protocol, count(*) AS count group by http_protocol
```

- Replace the '123' characters in the **remote_user** string with the `ABC` characters and return a result of the VARCHAR type:
```
 * | SELECT translate(remote_user, '123', 'ABC')
```

- Extract the 2nd to 5th characters from the value of the **remote_user** field:
```
* | SELECT substr(remote_user, 2, 5)
```

- Return the position of the 'H' letter in the value of the **http_protocol** field:
```
* | SELECT strpos(http_protocol, 'H')
```

- Split the value of the **http_protocol** field into 2 substrings using a slash (/) and return the collection of the substrings:
```
* | SELECT split(http_protocol, '/', 2)
```

- Replace 'Oct' in the value of the **time_local** field with '10':
```
* | select replace(time_local, 'Oct', '10')
```



