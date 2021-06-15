
## Syntax (Lucene)

| Reserved Keyword | Description |
| :------------ | :----------------------------------------------------------- |
| \_\_SOURCE\_\_ | It is used to search for logs from a specified source, and wildcard is supported, such as `__SOURCE__:"127.0.0.*"`. |
| \_\_FILENAME\_\_ | It is used to search for logs from a specified file, and wildcard is supported, such as:<ul  style="margin: 0;"><li>Full match: <code>\_\_FILENAME\_\_:"/var/log/access.*"</code></li><li>Fuzzy match: <code>\_\_FILENAME\_\_:/var/log/access.*</code></li></ul> |
| AND | Logical AND operator, such as `level:ERROR AND pid:1234`. |
| OR | Logical OR operator, such as `level:ERROR OR level:WARNING`. |
| NOT | Logical NOT operator, such as `level:ERROR NOT pid:1234`. |
| TO | Logical TO operator, such as `request_time:[0.1 TO 1.0]`. |
| "" | Double quotation marks, which quote a phrase, such as `name:"john Smith"`. |
| : | Colon, which is used for key-value search, such as `level:ERROR`. |
| * | Wildcard, which can match zero, one, or multiple characters, such as `host:www.test*.com`. |
| ? | Wildcard, which can match one single character, such as `host:www.te?t.com`. |
| () | Grouping operator, which controls the precedence of logical operations, such as `(ERROR OR WARNING) AND pid:1234`. |
| > | Range operator, which indicates the left operand is greater than the right operand, such as `status:>400`. |
| >= | Range operator, which indicates the left operand is greater than or equal to the right operand, such as `status:>=400`. |
| < | Range operator, which indicates the left operand is less than the right operand, such as `status:<400`. |
| <= | Range operator, which indicates the left operand is less than or equal to the right operand, such as `status:<=400`. |
| [] | Range operator, which includes the upper and lower boundary values, such as `age:[20 TO 30]`. |
| {} | Range operator, which excludes the upper and lower boundary values, such as `age:{20 TO 30}`. |
| \  | Escape character. An escaped character represents the literal meaning of the character, such as `url:\/images\/favicon.ico"`. |
| + | Logical operator (similar to AND). The term `+A` indicates `A` must exist, such as `+level:ERROR +pid:1234`. |
| - | Logical operator (similar to NOT). The term `-A` indicates `A` must not exist, such as `+level:ERROR -pid:1234. |
| \|\| | Logical operator (similar to OR), such as `level:ERROR \|\| level:WARNING`. |
| && | Logical operator (similar to AND), such as `level:ERROR && pid:1234`. |
| ! | Logical operator (similar to NOT), such as `level:ERROR !pid:1234`. |
| / | Regular expression identifier in the format of `/${regExp}/`. For example, `/[mb]oat/` means to return results containing `moat` or `boat`. |
| \_exists\_ | `\_exists\_:key` returns results where the `key` value is not empty. For example, `_exists_:userAgent` means to return results where the `userAgent` value is not empty. |
| ~ | Fuzzy search. For example, `level:errro~` means to return results where `level` contains `error`. |

>?
>
> - The syntactic operators are case-sensitive. For example, `AND` and `OR` represent logical search operators, while `and` and `or` are regarded as common words.
> - When multiple search statements are connected with spaces, they are regarded as in the `OR` logic. For example, `warning error` indicates to return results containing the `warning` keyword or `error` keyword.
> - All the characters in the syntax are reserved characters. If a search keyword contains these syntactically reserved characters, they need to be escaped.
> - Before performing a `key:value` search, make sure the key is configured in the index configuration of the log topic.



## Sample Search Statements

| Expected Search Result  | Search Statement |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Logs containing `ERROR`  | `ERROR` |
| Failed logs (with a status code greater than 400) | `status:>400` |
| Failed logs in the `GET` request (with a status code greater than 400) | `method:GET AND status:>400` |
| Logs at `ERROR` or `WARNING` level | `level:ERROR OR level:WARNING` |
| Logs except those at `INFO` level | `NOT level:INFO` |
| Logs from `192.168.10.10` but except those at `INFO` level | `__SOURCE__:192.168.10.10 NOT level:INFO` |
| Logs from the `/var/log/access.log` file on `192.168.10.10` but except those at `INFO` level | `(__SOURCE__:192.168.10.10 AND __FILENAME__:"/var/log/access.*") NOT level:INFO` |
| Logs from `192.168.10.10` and at `ERROR` or `WARNING` level | `__SOURCE__:192.168.10.10 AND (level:ERROR OR level:WARNING)` |
| Logs with a status code of `4XX`  | `status:[400 TO 500}` |
| Logs with the container name `nginx` in the metadata | `__TAG__.container_name:nginx` |
| Logs with the container name `nginx` in the metadata, and request latency greater than 1s | `__TAG__.container_name:nginx AND request_time:>1` |
| Logs that contain the `message` field, or whose `message` field has a value | `message:*` or `_exists_:message` |
| Logs that do not contain the `message` field  | `NOT _exists_:message` |
| Logs whose `message` field is empty | `message:""` |


## Fuzzy Search

When you use CLS Lucene syntax for fuzzy search, you need to add wildcards in the middle or end of a field. You can use an asterisk (*) to match zero, one, or multiple characters, or use a question mark (?) to match one character.

Example:
- `addr*` means searching for all fields starting with `addr` and returning logs contains such fields.
- `host:www.te?t.com` means searching for fields that start with `host:www.te`, end with `t.com` and contain one character between the two, and returning logs contains such fields. 

>? 
> - You cannot put an asterisk (*) or question mark (?) in the beginning of the field, meaning CLS does not support match by prefix.
> - Data of `long` or `double` type does not support asterisk (*) or question mark (?) for fuzzy search, yet supports value range for fuzzy search, such as `status:[400 TO 500}`.
> 

