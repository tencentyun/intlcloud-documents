##  Syntax Rules

>!
> - The operators are case-sensitive. For example, `AND` and `OR` represent logical search operators, while `and` and `or` are regarded as common words.
> - When multiple search statements are connected with spaces, they are regarded as in the `OR` logic. For example, `warning error` indicates to return results containing the `warning` keyword or `error` keyword.
> - The following special characters must be escaped: +, -, &&, ||, !, ( ), { }, [ ], ^, ", ~, *, ?, :, \
> - Before performing a `key:value` search, make sure the key is configured in the index configuration of the log topic.
> - Use () to group search conditions and clarify the precedency when using the "AND" and "OR" operators, such as `(ERROR OR WARNING) AND pid:1234`.
> 

| Operator  | Description                                                        |
| :------------ | :----------------------------------------------------------- |
| AND | Logical AND operator, such as `level:ERROR AND pid:1234`. |
| OR | Logical OR operator, such as `level:ERROR OR level:WARNING`. |
| NOT | Logical NOT operator, such as `level:ERROR NOT pid:1234`. |
| TO | Logical TO operator, such as `request_time:[0.1 TO 1.0]`. |
| "" | Double quotation marks, which quote a phrase, such as `name:"john Smith"`. |
| : | Colon, which is used for key-value search, such as `level:ERROR`. |
| *             | Wildcard, which is used to replace zero, one, or more characters, such as `host:www.test*.com`. Prefix fuzzy queries are not supported. For more information, please see [Fuzzy Search](https://intl.cloud.tencent.com/document/product/614/30439). </br>You can also use `key:*` to query logs where the specified field (`key`) exists. `key:*` is equivalent to `_exists_:key`. |
| ? | Wildcard, which can match one single character, such as `host:www.te?t.com`. |
| () | Grouping operator, which controls the precedence of logical operations, such as `(ERROR OR WARNING) AND pid:1234`. |
| > | Range operator, which indicates the left operand is greater than the right operand, such as <code>status:>400`</code> |
| >= | Range operator, which indicates the left operand is greater than or equal to the right operand, such as </code>status:>=400</code> |
| < | Range operator, which indicates the left operand is less than the right operand, such as <code>status:<400</code> |
| <= | Range operator, which indicates the left operand is less than or equal to the right operand, such as </code>status:<=400`</code> |
| [] | Range operator, which includes the upper and lower boundary values, such as `age:[20 TO 30]`. |
| {} | Range operator, which excludes the upper and lower boundary values, such as `age:{20 TO 30}`. |
| \             | Escape character. An escaped character represents the literal meaning of the character, such as `url:\/images\/favicon.ico`. You can also use `""` to wrap special characters as a whole, e.g., `url:"/images/favicon.ico"`. For details about the difference between these two search methods, see [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594").|
| + | Logical operator (similar to AND). The term `+A` indicates `A` must exist, such as `+level:ERROR +pid:1234`. |
| - | Logical operator (similar to NOT). The term `-A` indicates `A` must not exist, such as `+level:ERROR -pid:1234` |
| && | Logical operator (similar to AND), such as <code>level:ERROR && pid:1234</code> |
| ! | Logical operator (similar to NOT), such as `level:ERROR !pid:1234`. |
| /             | Regular expression identifier in the format of `/${regExp}/`. For example, `/[mb]oat/` means to return results containing `moat` or `boat`.</br>Note: With a delimiter, the regular expression matches the single word following the delimiter, not the entire log or field. |
| \_exists\_ | `\_exists\_:key` returns logs that contains `key`. For example, `_exists_:userAgent` means to return logs that contains the `userAgent` field. |
| ~ | Fuzzy search. For example, `level:error~` means to return results where `level` contains `error`. |



## Sample Search Statements

| Expected Search Result  | Search Statement |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Logs of a specified `SOURCE`                                     | `__SOURCE__:127.0.0.1` or  `__SOURCE__:192.168.0.*`             |
| Logs from a specified file:                                       | `__FILENAME__:"/var/log/access.log"`or`__FILENAME__:\/var\/log\/*.log` |
| Logs containing `ERROR`  | `ERROR` |
| Searching-failed logs (Status code > 400)                            | <code>status:>400</code>                                                |
| Failed logs in the `GET` request (with a status code greater than 400) | <code>method:GET AND status:>400</code> |
| Logs at `ERROR` or `WARNING` level | `level:ERROR OR level:WARNING` |
| Logs except those at `INFO` level | `NOT level:INFO` |
| Logs from `192.168.10.10` but except those at `INFO` level | `__SOURCE__:192.168.10.10 NOT level:INFO` |
| Logs from the `/var/log/access.log` file on `192.168.10.10` but except those at `INFO` level | `(__SOURCE__:192.168.10.10 AND __FILENAME__:"/var/log/access.log.*") NOT level:INFO` |
| Logs from `192.168.10.10` and at `ERROR` or `WARNING` level | `__SOURCE__:192.168.10.10 AND (level:ERROR OR level:WARNING)` |
| Logs with a status code of `4XX`  | `status:[400 TO 500}` |
| Logs with the container name `nginx` in the metadata | `__TAG__.container_name:nginx` |
| Logs with the container name `nginx` in the metadata, and request latency greater than 1s | <code>\_\_TAG\_\_.container_name:nginx AND request_time:>1</code> |
| Logs that contain the `message` field, or whose `message` field has a value | `message:*` or `_exists_:message` |
| Logs that do not contain the `message` field  | `NOT _exists_:message` |



## Fuzzy Search

To perform a fuzzy query via CLS, you need to add wildcards to the middle or end of words, either by using the asterisk `*` to match zero, single, or multiple characters, or using the question mark `? ` to match a single character.

>!
> - The asterisk `*` or question mark `? ` cannot be used at the beginning of a word, i.e. prefix fuzzy queries are not supported.
> - Data of `long` or `double` type does not support an asterisk (*) or question mark (?) for fuzzy search, yet supports a value range for fuzzy search, such as `status:[400 TO 500}`.

Sample:
- `IP:192.168.1.*` means searching for logs whose IP starts with `192. 168.1`, e.g. `192. 168.1.1`, `192. 168.1.34`.
- `host:www.te?t.com` means searching for logs whose host name starts with `www.te`, ends with `t.com` and contains 1 character in the middle, e.g. `www.test.com`, `www.telt.com`.


If you need to use fuzzy search with prefix specified, you can use the following methods.

- Adding a prefix: for example, if the logs are `host:www.test.com`, `host:m.test.com`, and you need to query logs containing `test` in the middle, you can add the prefix `. ` to search for logs with `host:test`.
- Using the LIKE operator: e.g. `* | SELECT * where host like '%test%'`.

