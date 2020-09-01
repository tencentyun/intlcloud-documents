
##  Syntax Rule

| Reserved Keyword    | Description                                                         |
| :------------ | :----------------------------------------------------------- |
| \_\_SOURCE\_\_    | The operator that specifies the IP address of a source whose logs you want to query, and wildcard is supported, such as `__SOURCE__:"127.0.0.*"` |
| \_\_FILENAME\_\_  | The operator that specifies the file path from which you want to query logs, and wildcard is supported, such as `__FILENAME__:"/var/log/access.*"` |
| AND           | The AND logical operator that displays a record if all the conditions separated by AND are TRUE, such as `level:ERROR AND pid:1234`                |
| OR            | The OR logical operator that displays a record if any of the conditions separated by OR is TRUE, such as `level:ERROR OR level:WARNING`            |
| NOT           | The NOT logical operator that displays a record if the condition(s) is NOT TRUE, such as `level:ERROR NOT pid:1234`                |
| TO            | The range operator that matches results whose field(s) values are between the lower and upper bounds specified, such as `request_time:[0.1 TO 1.0]`            |
| ""            | All characters in the double quotation mark are considered as a general phrase, such as `name:"john Smith"` |
| :             | The operator that specifies the “key:value” search format, such as `level:ERROR`    |
| *             | The wildcard character that replaces zero, single, or multiple random characters, such as `host:www.test*.com` |
| ?             | The wildcard character that replaces a single character at a specific position, such as `host:www.te?t.com` |
| ()            | The parentheses is used to group clauses to form sub queries and control the logic operations, such as `(ERROR OR WARNING) AND pid:1234` |
| >             | The range operator that matches results whose field(s) values are greater than a specified number, such as `status:>400`             |
| >=              | The range operator that matches results whose field(s) values are greater than or equal to a specified number, such as `status:>=400`             |
| <             | The range operator that matches results whose field(s) values are less than a specified number, such as `status:<400`             |
| <=             | The range operator that matches results whose field(s) values are less than or equal to a specified number, such as `status:<=400`             |
| []            | The range query is inclusive of the upper and lower bounds, such as `age:[20 TO 30]`          |
| {}            | The range query is exclusive of the upper and lower bounds, such as `age:{20 TO 30}`          |
| \             | Escape character. An escaped character represents the literal meaning of the character, such as`url:\/images\/favicon.ico"` |
| +             | The "+" logical operator (similar to AND) requires that the term after the "+" symbol exist. The term `+A` means `A` exist, such as `+level:ERROR +pid:1234` |
| -             | The "-" logical operator (similar to NOT) excludes the object that contains the term after the "-" symbol. The term `-A` means `A` does not exist, such as `+level:ERROR -pid:1234 |
| \|\|          | A valid substitute for the logical operator OR, such as `level:ERROR \|\| level:WARNING`          |
| &&            | A valid substitute for the logical operator AND, such as `level:ERROR && pid:1234`              |
| !             | A valid substitute for the logical operator NOT, such as `level:ERROR !pid:1234`                |
| /             | A regular expression identifier in the format of/${regExp}/. For example, use `/[mb]oat/` to obtain search results containing `moat` or `boat` |
| \_exists\_    | The operator that returns a result whose key value exists. For example, use `_exists_:userAgent` to obtain search results whose `userAgent` field has a value |
| ~             | Fuzzy search. For example, use `level:errro~` to obtain search results whose `level` field contains `error` |

>?
>
> - The syntax operators are case-sensitive. Use the logical operators in all caps (such as AND, OR), otherwise they will be regarded as ordinary phrases.
> - If you connect multiple search statements with a space, the OR logic will be used. For example, enter `warning error` to obtain results containing `warning` or `error`.
> - All strings in the syntax are reserved. These reserved characters in the search keyword need to be escaped.
> - Before performing a “key:value” search, make sure the key is successfully configured in the index configuration of the log topic.



## Search Statement Examples

| Expected Search Result                                                    | Search Statement                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Logs containing `ERROR`                              | `ERROR`                                                      |
| Failed logs (with a status code larger than 400)                             | `status:>400`                                                |
| Failed logs in the `GET` request (with a status code larger than 400)                 | `method:GET AND status:>400`                                 |
| Logs at `ERROR` or `WARNING` level                       | `level:ERROR OR level:WARNING`                               |
| Logs except those at `INFO` level                                  | `NOT level:INFO`                                             |
| Logs from `192.168.10.10` but except those at `INFO` level           | `__SOURCE__:192.168.10.10 NOT level:INFO`                    |
| Logs from the `/var/log/access.log` file on `192.168.10.10` but except those at `INFO` | `(__SOURCE__:192.168.10.10 AND __FILENAME__:"/var/log/access.*") NOT level:INFO` |
| Logs from `192.168.10.10` and at `ERROR` or `WARNING` level  | `__SOURCE__:192.168.10.10 AND (level:ERROR OR level:WARNING)` |
| Logs with a status code of `4XX`                                      | `status:[400 TO 500}`                                        |
| Logs with the container name as `nginx` in the metadata                         | `__TAG__.container_name:nginx`                               |
| Logs with the container name as `nginx` in the metadata, and request latency of longer than 1 second       | `__TAG__.container_name:nginx AND request_time:>1`           |
| Logs that contain the `message` field, or whose `message` field has a value  | `message:*` or `_exists_:message`                          |
| Logs that do not contain the `message` field                             | `NOT _exists_:message`                                       |
| Logs whose `message` field is empty                              | `message:""`                                                 |

