CLS provides a wide variety of search features. You can search for logs in real time by search syntax and rules and get results within seconds, gaining insights into your business operations.

## Starting Search

Log search is an important CLS feature. You can define the search criteria to search for hundreds of millions of log data rows. The steps are as follows:

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Select **Log Search** on the left sidebar to enter the log search page.
3. Select the time range, logset, and log topic.
4. Enter keywords and click **Search** to get results.

## Search Syntax

The following search syntax can be used in searches:

| Syntax          | Semantics                                                         |
| ------------- | ------------------------------------------------------------ |
|key:value| This refers to the "key-value" search format. You need to enable the [key-value index](https://intl.cloud.tencent.com/document/product/614/16981). The value supports fuzzy search by `?` or `*`.|
|A and B| "AND" logic that returns the intersection of A and B. If multiple keywords are used for search at a time, the default logic will be "AND" if they are separated by spaces. |
| A or B | "OR" logic that returns the union of A or B. |
| not B | "NOT" logic that returns the results excluding B. |
| A not B | "MINUS" logic that returns the results including A but excluding B, i.e., A-B. |
| 'a' | The character `a` will be considered as a regular character and will not be processed as a syntax keyword. |
| "A" | All characters in A will be considered as regular ones and will not be processed as syntax keywords. |
|\ |Escape character. An escaped character represents the literal meaning of the character, such as \" for quotation mark or \: for colon. |
|* |Fuzzy query of keywords that can match zero, single, or multiple random characters. `*` cannot be used as the first character. For example, if you enter `abc*`, all logs beginning with `abc` will be returned.|
| ? |Fuzzy query of keywords that can match a single character at a specific position. For example, if you enter `ab?c`, logs that begin with `ab`, end with `c`, and contain only one character between `ab` and `c` will be returned.|
| > | "GREATER THAN" logic, which is used for numeric fields. |
| >= | "GREATER THAN OR EQUAL TO" logic, which is used for numeric fields. |
| < | "LESS THAN" logic, which is used for numeric fields. |
| <= | "LESS THAN OR EQUAL TO" logic, which is used for numeric fields. |
|=| "EQUAL TO" logic, which can be used for numeric or text fields. (Fuzzy search is not supported. If you need fuzzy search, please see the key-value search `key:value`.)|
| `__SOURCE__`   | It is used to search for the logs from a specified source, and wildcard is supported, such as `__SOURCE__:127.0.0.*`. |
| `__FILENAME__` | It is used to search for the logs from a specified file, and wildcard is supported, such as `__FILENAME__:/var/log/access.*`. |

>
> - Numeric fields must be set to a double or long type before you can search for a range; otherwise, you may get different results than expected.
> - If b is text, then, the difference between `a=b` and `a:b` lies in that a equals b in the former, while a contains b in the latter (the search is processed based on the word segmentation logic and fuzzy search is supported).



## Search Rule

Time range, logset, and log topic are required for log search. The default time range is the current day. You can select the logset and log topic as needed. The search box can be left empty, which means no filter conditions, and all valid log data will be returned.

### Full-text search

Log data of log topics with full-text index enabled is split into multiple phrases with word delimiters, so that you can search for the log by specific keywords.

For example, to search for log data containing the keyword `error`, enter `error` in the search box and search.

### Key-value search

Log data of the log topics with key-value index enabled is managed based on the specified key-value pairs. You can search for the log by specifying a key field.

For example, to search for log data with `error` as the `status` field, enter `status:error` in the search box and search.

### Fuzzy keyword search

CLS supports fuzzy search, which allows you to search for logs by special fuzzy keywords as described below:

| Metacharacter | Description                                                         |
| ------ | :----------------------------------------------------------- |
| * | Fuzzy query of keywords that can match zero, single, or multiple random characters. For example, if you enter `abc*`, all logs beginning with `abc` will be returned.|
| ? |Fuzzy query of keywords that can match a single character at a specific position. For example, if you enter `ab?c`, logs that begin with `ab`, end with `c`, and contain only one character between `ab` and `c` will be returned.|


## Notes

1. Before performing a log search, make sure index is enabled for the relevant log topics. Otherwise, no valid logs will be found.
2. Before performing a key-value search, make sure the index field for searching is successfully configured in the index configuration of the log topic.
3. The results are displayed in reverse order by default.
