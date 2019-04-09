CLS provides various search functionalities. You can query logs in real time by querying syntax and search rules, and get results in seconds. CLS gives you insights into your business operations.

## Starting Search

Log search is an important CLS function.  You can define the query conditions to query 100 million-level log data within seconds. Specific steps are as follows:

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Select **Log Search** in the left navigation pane to enter the Log Search page.
3. Select the time range, logset, and log topic.
4. Enter keywords, and click **Search** to get results.

## Query Syntax
The following query syntax can be used in search:

| Syntax | Meaning |
|--|--|
| A and B | "AND" logic. The intersection of A and B is returned. If several keywords are separated by commas, semicolons or spaces, the "AND" logic is used by default. |
| A or B | "OR" logic. The union of A or B is returned. |
| not B | "NOT" logic. The results that do not include B are returned. |
| A not B | "MINUS" logic. The results that match A but not B are returned, i.e. A-B. |
| (A, B) | Multiple queries are combined into one query to control the operator precedence. |
| A:B | The "key-value" query format. If the key or value contains key characters such as spaces or colons, you need to include them in quotation marks, for example "error level":high. |
| 'a' | The character "a" is regarded as a normal character, instead of a syntax keyword. |
| "A" | All the keywords in "A" are regarded as normal characters instead of syntax keywords. |
| \ | An escape character. The escaped character represents the symbol itself, such as escaped quote `\"` and escaped colon `\:`. |
| * | A keyword for fuzzy query, which can contain zero, one, or multiple characters. Starting with "\*" is not supported for fuzzy query. For example, entering `abc*` will return all the logs starting with `abc`. |
| ? | A keyword for fuzzy query, indicating that only one character can be placed at a specific location. For example, entering `ab?c` will return all the logs that start with `ab` and end with `c`, with only one character in between. |
| > | Greater than, used for numeric fields. |
| >= | Greater than or equal to, used for numeric fields. |
| < | Less than, used for numeric fields. |
| <= | Less than or equal to, used for numeric fields. |
| = | Equal to, used for numeric fields or texts. |
| in | Queries a numeric range. `[]` indicates a closed interval. `()` indicates an open interval. For example, `(0 100]` indicates an interval > 0 and <= 100. |
| \_source_ | Queries the logs of a source, for example \_source_: 127.0.0.1. |

>!
>- The operators' precedence is sorted in descending order: `:` > `"` > `()` > `and` > `not` > `or`.
>- The numeric fields must be set to double or long type before you search a range; otherwise, you may get different results than expected.
>- If b is text, the difference between `a=b` and `a:b` is that the former means a equals to b, and the latter means a includes b (they are processed by word segmentation logic and fuzzy search is supported).
>- Syntax keywords are case-insensitive.



## Search Rules
The time range, logset, and log topic are required for log index. The default time range is the current day. You can select the logset and log topic as needed. The search box can be left empty, which means no filter conditions, and all valid log data will be returned.

### Full-text index
Log data of the log topic that enables full-text index is split into multiple phrases with word separators, so that you can search the log by specific keywords.

For example, to search for log data containing the keyword `error`, enter `error` in the search box and search for it.

### Key value search
Log data of the log topic that enables key value index is managed based on the specified key value pairs. You can search the log by specifying a key field.

For example, to search for log data with `error` as `status`, enter `status:error` in the search box and search for it.

### Fuzzy keyword search
CLS provides fuzzy query that allows you to search logs by special fuzzy keywords. Details are described below:

| Metacharacter | Description |
|-----|:-----|
| * | A keyword for fuzzy query, which can contain zero, one, or multiple characters. For example, entering `abc*` will return all the logs starting with `abc`. |
| ? | A keyword for fuzzy query, indicating that only one character can be placed at a specific location. For example, entering `ab? C` will return all the logs that start with `ab` and end with `c`, with only one character in between. |

### Cross-topic search
Log search allows you to select only one logset but multiple log topics under the logset, which means that you can search in multiple log topics under one logset at the same time, making it easier for troubleshooting.

## Notes
1. Before performing log search, make sure the index is enabled for relevant log topics. Otherwise, no valid logs will be found.
2. Before performing key value search, make sure the index field to query is successfully configured in the index configuration of log topic.
3. The found results are displayed in descending order by default.

