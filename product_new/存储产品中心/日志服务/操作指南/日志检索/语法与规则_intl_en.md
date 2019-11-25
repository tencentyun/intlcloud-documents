CLS provides a variety of search features. You can search for logs in real time by search syntax and rules, and get results within seconds. CLS gives you insights into your business operations.

## Starting a search

Log search is an important CLS feature. You can define the search criteria to search for 100-million-level log data within seconds. Specific steps are as follows:

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Select **Log Search** in the left sidebar to enter the Log Search page.
3. Select the time range, logset, and log topic.
4. Enter keywords, and click **Search** to get results.

## Search syntax
The following search syntax can be used in searches:

| Syntax | Meaning |
|--|--|
|key:value| The "key-value" search format. You need to enable the index. For details, see [Enabling Index](https://intl.cloud.tencent.com/document/product/614/16981). The value supports fuzzy search by `?` or `*`. If the key or value contains key characters such as spaces or colons, you need to include them in quotation marks, for example, "error level":high.|
|A and B| "AND" logic. The intersection of A and B is returned. If several keywords are separated by commas, semicolons, or spaces, the "AND" logic is used by default. |
| A or B | "OR" logic. The union of A or B is returned. |
| not B | "NOT" logic. The results that do not include B are returned. |
| A not B | "MINUS" logic. The results that match A but not B are returned, i.e. A-B. |
|'a'| The character "a" is regarded as a normal character instead of a syntax keyword.|
| "A" | All the keywords in "A" are regarded as normal characters instead of syntax keywords. |
|\ |An escape character. The escaped character represents the symbol itself, such as escaped quote `\"` and escaped colon `\:`. |
|* |A keyword for fuzzy search, which can contain zero, one, or multiple characters. Starting with `*` is not supported for fuzzy search. For example, if you enter `abc*`, all the logs starting with `abc` are returned.|
| ?|A keyword for fuzzy search, indicating that only one character can be placed at a specific location. For example, if you enter `ab?c`, all the logs that start with `ab` and end with `c` are returned, with only one character in between.|
| > | Greater than, used for numeric fields. |
| >= | Greater than or equal to, used for numeric fields. |
| < | Less than, used for numeric fields. |
| <= | Less than or equal to, used for numeric fields. |
|=| Equal to, used for numeric fields or text. (Fuzzy search is not supported. To use fuzzy search, use the key:value syntax.)|
| in | Searches in a numeric range. `[]` indicates a closed interval. `()` indicates an open interval. For example, `(0 100]` indicates an interval >0 and <=100. |
| \_source_ |Searches for the logs of a source, for example, `\_source_:127.0.0.1`.|

>
>- The operators' precedence is sorted in descending order `:` > `"` > `()` > `and` > `not` > `or`.
>- Numeric fields must be set to a double or long type before you search for a range; otherwise, you may get different results than expected.
>- If b is text, the difference between `a=b` and `a:b` is that the former means a equals b, and the latter means a includes b (they are processed by word delimiting logic, and fuzzy search is supported).
>- Syntax keywords are case-insensitive.



## Search rules
Time range, logset, and log topic are required for log search. The default time range is the current day. You can select the logset and log topic as needed. The search box can be left empty, which means no filter conditions, and all valid log data will be returned.

### Full-text search
Log data of log topics with full-text index enabled is split into multiple phrases with word delimiters, so that you can search for the log by specific keywords.

For example, to search for log data containing the keyword `error`, enter `error` in the search box and search for it.

### Key-value search
Log data of the log topics with key-value index enabled is managed based on the specified key-value pairs. You can search for the log by specifying a key field.

For example, to search for log data with `error` as `status`, enter `status:error` in the search box and search for it.

### Fuzzy keyword search
CLS provides fuzzy search, which allows you to search for logs by special fuzzy keywords. Details are described below:

| Metacharacter | Description |
|-----|:-----|
| * | A keyword for fuzzy search, which can contain zero, one, or multiple characters. For example, if you enter `abc*`, all the logs starting with `abc` are returned.|
| ? |A keyword for fuzzy search, indicating that only one character can be placed at a specific location. For example, if you enter `ab?c`, all the logs that start with `ab` and end with `c` are returned, with only one character in between.|

### Cross-topic search
Log search allows you to select only one logset but multiple log topics under the logset, which means that you can search in multiple log topics under one logset at the same time, making it easier to perform troubleshooting.

## Notes
1. Before performing a log search, make sure index is enabled for the relevant log topics. Otherwise, no valid logs will be found.
2. Before performing a key-value search, make sure the index field for searching is successfully configured in the index configuration of the log topic.
3. The results are displayed in reverse order by default.
