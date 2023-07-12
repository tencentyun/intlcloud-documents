CLS provides a variety of search features. You can search for logs in real time by search syntax and rules, and get results within seconds. CLS gives you insights into your business operations.

## Starting Search

Log search is an important CLS feature. You can define the search criteria for billions of log data and obtain results within seconds. Specific steps are as follows:

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Log Search** in the left sidebar to enter the **Search Analysis** page.
3. Select the time range, logset, and log topic.
4. Enter the keyword, and click **Search Analysis** to obtain the query result.

## Search Syntax

The following query statements are supported:

| Syntax          | Semantics                                                         |
| ------------- | ------------------------------------------------------------ |
|key:value | The "key-value" search format. You need to [enable the key-value index](https://intl.cloud.tencent.com/document/product/614/16981). The `value` supports fuzzy search by `?` or `*`|
|A and B| The "AND" logic that returns the intersection of A and B. If several keywords are separated by spaces, the "AND" logic is used by default |
| A or B | The "OR" logic that returns the union of A or B |
| not B | The "NOT" logic that returns the results excluding B |
| A not B | The "MINUS" logic that returns the results including A but excluding B, i.e., `A - B` |
| 'a' | The character `a` will be considered as a regular character and will not be processed as a syntax keyword |
| "A" | All characters in `A` will be considered as regular characters and will not be processed as syntax keywords |
| \ | Escape character. An escaped character represents the literal meaning of the character, such as `\"` for quotation mark or `\:` for colon |
| * | Fuzzy query of keywords that can match zero, single, or multiple random characters. But the search cannot start with `*`. For example, enter `abc*` to search for all logs beginning with `abc` |
| ? | Fuzzy query of keywords that can match a single character at a specific position. For example, enter `ab?c` to search for logs that begin with `ab`, end with `c`, and contain only one character between `ab` and `c` |
| > | "GREATER THAN" logic, which is used for numeric fields |
| >= | "GREATER THAN OR EQUAL TO" logic, which is used for numeric fields |
| < | "LESS THAN" logic, which is used for numeric fields |
| <= | "LESS THAN OR EQUAL TO" logic, which is used for numeric fields |
| = | "EQUAL TO" logic, which can be used for numeric or text fields (Fuzzy search is not supported. If you need fuzzy search, please see the key-value search `key:value`)|
| `__SOURCE__`   | The operator that specifies the IP address of a source whose logs you want to query, and wildcard is supported, such as `__SOURCE__:127.0.0.*` |
| `__FILENAME__` | The operator that specifies the file path from which you want to query logs, and wildcard is supported, such as `__FILENAME__:/var/log/access.*` |

> !
>- Before using the range search, set the numeric fields to a double or long type; otherwise, you may have unexpected results.
>- If **b** is text, the difference between `a=b` and `a:b` lies in that **a** equals **b** in the former, while **a** contains **b** in the latter (the search is processed based on the segment logic and fuzzy search is supported).




## Search Rules

Time range, logset, and log topic are required for log search. The default time range is the current day, while the logset and log topic are at your discretion. You can search for all logs without entering anything in the search box.

### Full-text search

Log data of log topics with full-text index enabled is split into segments by delimiter, so you can execute keyword query based on the segments.

For example, enter `error` in the search box to search for log data containing the keyword `error`.

### Key-value search

Log data of the log topics with key-value index enabled is managed based on the specified key-value pairs. You can search for the log by specifying a key field.

For example, enter `status:error` in the search box to search for log data whose `status` field is `error`.

### Fuzzy keyword search

CLS supports fuzzy search by special keywords as shown below:

| Metacharacter | Description                                                         |
| ------ | :----------------------------------------------------------- |
| * | Fuzzy query of keywords that can match zero, single, or multiple random characters. For example, enter `abc*` to search for all logs beginning with `abc` |
| ? | Fuzzy query of keywords that can match a single character at a specific position. For example, enter `ab?c` to search for logs that begin with `ab`, end with `c`, and contain only one character between `ab` and `c` |

## Notes

1. Before performing a log search, make sure the log topic has index enabled. Otherwise, no valid logs will be found.
2. Before performing a key-value search, make sure the index field for searching is successfully configured in the index configuration of the log topic.
3. The results are displayed in reverse order by default.
