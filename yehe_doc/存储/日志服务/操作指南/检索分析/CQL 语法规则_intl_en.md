## Overview

CLS provides log search and analysis capabilities. You can use search and analysis statements to search for logs that match specific conditions, or use SQL to analyze matched logs to obtain statistical results such as the number of logs, average response time, and error log percentage.

A search and analysis statement is composed of two parts, search condition and SQL statement, which are separated by a vertical bar (|).

```
[Search condition] | [SQL statement]
```

**Two syntax rules are supported in search conditions:**
- **Lucene syntax**: The legacy search syntax of CLS, which adopts the [open-source Lucene syntax](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html) and is available to all regions and log topics. As it is not designed for log search, it has many restrictions on special symbols, case sensitivity, and wildcards, which tend to cause syntax errors.
- **CQL syntax**: CLS query language, which is designed for log search in CLS. We recommend you use it for its ease to learn and use.
> !
> - Currently, CQL is provided to certain users through an allowlist. You can view whether it is supported for your current log topic in the settings section in the top-right corner of the search statement input box.
> - Currently, CQL is not supported for log downloads or scheduled SQL tasks.


## CQL Strengths

* CQL logical operators are case-insensitive. For example, `level:ERROR AND pid:1234` is equivalent to `level:ERROR and pid:1234`.
* CQL has few special symbols that need to be escaped. For example, you can directly use `url:/book/user/login/` for search, which will cause an error in Lucene if not escaped to `url:\/book\/user\/login\/`.
* When strings containing segments are searched for, the relationships between segments are "AND" in CQL but "OR" in Lucene. For example, if the delimiter is `/`, `url:/book/user/login/` is equivalent to `url:book AND url:user AND url:login` in CQL, while `url:\/book\/user\/login\/` is equivalent to `url:book OR url:user OR url:login` in Lucene.
* In phrase searches, wildcards are supported in CQL but not in Lucene. For example, if the delimiter is `/`, `url:"/book/user/log*/"` can find `/book/user/login/` and `/book/user/logout/` in CQL.



## CQL Syntax Rules

### Syntax rules

| Syntax      | Description                                                         |
| :-------- | :----------------------------------------------------------- |
| key:value | Key-value search, which indicates to query logs with a `key` field whose value contains the `value`, such as `level:ERROR`. |
| value     | Full-text search, which indicates to query logs with the full text containing the `value`, such as `ERROR`.         |
| AND       | Logical AND operator, which is case-insensitive, such as `level:ERROR AND pid:1234`. |
| OR        | Logical OR operator, which is case-insensitive, such as `level:ERROR OR level:WARNING`. |
| NOT       | Logical NOT operator, which is case-insensitive, such as `level:ERROR NOT pid:1234`. |
| ()        | Parentheses, which control the priority of logical operations, such as `level:(ERROR OR WARNING) AND pid:1234`. |
| "  "      | [Phrase search](#pharseQuery), which encloses a string in double quotation marks to match logs that contain all the words in the string in the same sequence, such as `name:"john Smith"`.<br />A phrase search has no logical operators, and the phrase used is equivalent to the query character, such as `name:"and"`. |
| '  '      | [Phrase search](#pharseQuery), which encloses a string in single quotation marks and is equivalent to `""`. When the phrase to be searched for contains double quotation marks, single quotation marks can be used to enclose the phrase to avoid syntax errors, such as `body:'user_name:"bob"'`. |
| *         | [Fuzzy search](#wildcardQuery), which is used to match zero, one, or multiple characters, such as `host:www.test*.com`. Fuzzy prefix search is not supported. |
| >         | Range operator, which indicates the left operand is greater than the right operand, such as `status>400`.              |
| >=        | Range operator, which indicates the left operand is greater than or equal to the right operand, such as `status>=400`.         |
| <         | Range operator, which indicates the left operand is less than the right operand, such as `status<400`.              |
| <=        | Range operator, which indicates the left operand is less than or equal to the right operand, such as `status<=400`.         |
| =         | Range operator, which indicates the left operand is equal to the right operand, such as `status=400`.              |
| \         | Escape symbol. An escaped character represents the literal meaning of the character. If the value searched for contains spaces, `:`, `"`, `'`, or `*`, it needs to be escaped, such as `body:user_name\:bob`.<br />If single or double quotation marks are used for a phrase search, you only need to escape `*` and `'` or `"` respectively. <br />`*` that is not escaped represents a fuzzy search. |
| key:*     | Queries logs with a `key` field, no matter whether its value is null or not, such as `url:*`.       |
| key:""    | Queries logs with a `key` field whose value is null (a value is also null if it contains only delimiters), such as `url:""`. |



### Examples

| Scenario                                         | Statement                                               |
| -------------------------------------------- | -------------------------------------------------- |
| Logs from a specified server                     | `__SOURCE__:127.0.0.1` or `__SOURCE__:192.168.0.*` |
| Logs from a specified file                     | `__FILENAME__:"/var/log/access.log"`               |
| Logs containing `ERROR`                      | `ERROR`                                            |
| Failed logs (with a status code greater than 400)               | `status>400`                                       |
| Failed logs in the `GET` request (with a status code greater than 400) | `method:GET AND status>400`                        |
| Logs at `ERROR` or `WARNING` level         | `level:(ERROR OR WARNING)`                         |
| Logs except those at `INFO` level                    | `NOT level:INFO`                                   |



### Phrase search

<span id="pharseQuery"></span>

A string is enclosed in double or single quotation marks for search, such as `name:"john Smith"` and `__FILENAME__:"/var/log/access.log"`. Compared with searches without quotation marks, a phrase search means that the matched logs should contain all the words in the string and in the same sequence as required in the search condition.

Below are two sample logs with the delimiter of `/`:

```
#1 __FILENAME__:"/var/log/access.log"
#2 __FILENAME__:"/log/var/access.log"
```

* When you use `__FILENAME__:/var/log/access.log` for search, the above two logs will be matched, as it does not involve the sequence of words.
* When you use `__FILENAME__:"/var/log/access.log"` for search, only the first log will be matched.

Phrase searches have stricter search conditions and are recommended when long strings are searched for.

Phrase searches support wildcards such as `__FILENAME__:"/var/log/access_*.log"` but not in the beginning of words such as `__FILENAME__:"/var/log/*.log"`. In addition, wildcards in phrase searches can only match the first 128 words meeting the search condition and return all logs containing these 128 words. The more specific the words, the more accurate the results. This restriction is not applicable to non-phrase searches.



### Fuzzy search

<span id="wildcardQuery"></span>

To perform a fuzzy search in CLS, you need to add wildcards to the middle or end of words. You can use the asterisk `*` to match zero, one, or multiple characters, for example:

- `IP:192.168.1.*` means searching for logs whose IP starts with `192. 168.1`, e.g. `192. 168.1.1`, `192. 168.1.34`.
- `host:www.te*t.com` means searching for logs whose `host` starts with `www.te` and ends with `t.com`, such as `www.test.com` and `www.telt.com`.

>!
>- The asterisk `*` cannot be used at the beginning of a word; that is, fuzzy prefix search is not supported.
>- Data of the `long` or `double` type supports a value range but not the asterisk `*` for a fuzzy search, such as `status>400 and status<500`.

If you need to use fuzzy search with prefix specified, you can use the following methods.
- Adding a prefix: For example, if the logs are `host:www.test.com`, `host:m.test.com`, and you need to query logs containing `test` in the middle, you can add the prefix `. ` to search for logs with `host:test`.
- Using the `LIKE` syntax: For example, you can use `* | select * where host like '%test%'`. However, this method delivers lower performance than the search condition method and is not suitable for scenarios with large volume of log data.

Phrase searches support wildcards such as `__FILENAME__:"/var/log/access_*.log"` but not in the beginning of words such as `__FILENAME__:"/var/log/*.log"`. In addition, wildcards in phrase searches can only match the first 128 words meeting the search condition and return all logs containing these 128 words. The more specific the words, the more accurate the results. This restriction is not applicable to non-phrase searches.
