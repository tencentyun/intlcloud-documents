## Overview

CLS provides log search and analysis capabilities. You can use search statements to search for logs that match specific conditions, or use SQL statements to analyze matched logs to obtain statistical results such as the number of logs, average response time, and error log percentage.

A search statement consists of two parts: search condition and SQL statement, which are separated by a vertical bar (`|`).
```
[Search condition] | [SQL statement]
```

- Search condition: Specifies the condition for log search. Only logs that meet the condition will be returned. For example, you can use `status:404` to search for application request logs with response status code 404. For the corresponding syntax rules, see [Search Condition Syntax Rules](#RetrievesConditionalRules).
- SQL statement: Performs statistical analysis on logs that meet the search condition and returns the statistical analysis result. For example, you can use `status:404 | select count(*) as logCounts` to count the number of application request logs with response status code 404. SQL statements must comply with SQL-92. For the corresponding syntax rules, see [SQL Statement Syntax Rules](#SQLRules).

>?
>- To search for logs only without statistical analysis, omit the vertical bar `|` and SQL statement.
>- If the search statement is empty, all logs in the specified time range will be searched for.
>

A search condition can be used for full-text search or key-value search, depending on whether a log field is specified:
- Full-text search: No field name needs to be specified. If the value of any field in a log meets the search condition, the log will be matched. For example, you can use `error` to search for all logs that contain `error`.
- Key-value search: A field name needs to be specified. If the value of a specified field in a log meets the search condition, the log will be matched. For example, you can use `level:error` to search for logs at the `error` log level.

## Prerequisites

- **Using a search condition**:
 - Full-text search: Full-text index is enabled in index configuration.
 - Key-value search:
   - Log fields have been extracted as described in [Collection Overview](https://intl.cloud.tencent.com/document/product/614/31652) during log collection.
   - Key-value index is enabled for the field to be searched for during [index configuration](https://intl.cloud.tencent.com/document/product/614/39594).
- **Using a SQL statement**:
 - Log fields have been extracted as described in [Collection Overview](https://intl.cloud.tencent.com/document/product/614/31652) during log collection.
 - Key-value index and **statistics** are enabled for the field to be searched for during [index configuration](https://intl.cloud.tencent.com/document/product/614/39594).


<span id="RetrievesConditionalRules"></span>
## Search Condition Syntax Rules

### Syntax rules

| Syntax | Description |
| :--------- | :----------------------------------------------------------- |
| AND | Logical AND operator, such as `level:ERROR AND pid:1234`. |
| OR | Logical OR operator, such as `level:ERROR OR level:WARNING`. |
| NOT | Logical NOT operator, such as `level:ERROR NOT pid:1234`. |
| () | Grouping operator, which controls the precedence of logical operations, such as `(ERROR OR WARNING) AND pid:1234`. |
| : | Colon, which is used for key-value search, such as `level:ERROR`. |
| "" | Double quotation marks, which quote a phrase to match logs that contain all the words in the phrase and in the same sequence, such as `name:"john Smith"`. |
| * | Wildcard, which is used to replace zero, one, or more characters, such as `host:www.test*.com`. </br>Prefix fuzzy queries are not supported. For more information, see [Fuzzy Search](#.E6.A8.A1.E7.B3.8A.E6.A3.80.E7.B4.A2). </br>You can also use `key:*` to query logs where the specified field (`key`) exists. `key:*` is equivalent to `_exists_:key`. |
| ? | Wildcard, which can match one single character, such as `host:www.te?t.com`. </br>Similar to `*`, it does not support prefix fuzzy queries. |
| > | Range operator, which indicates the left operand is greater than the right operand, such as `status:>400`. |
| >= | Range operator, which indicates the left operand is greater than or equal to the right operand, such as `status:>=400`. |
| < | Range operator, which indicates the left operand is less than the right operand, such as `status:<400`. |
| <= | Range operator, which indicates the left operand is less than or equal to the right operand, such as `status:<=400`. |
| TO | Logical TO operator, such as `request_time:[0.1 TO 1.0]`. |
| [] | Range operator, which includes the upper and lower boundary values, such as `age:[20 TO 30]`. |
| {} | Range operator, which excludes the upper and lower boundary values, such as `age:{20 TO 30}`. |
| \ | Escape character. An escaped character represents the literal meaning of the character, such as `url:\/images\/favicon.ico`.</br>You can also use `""` to wrap special characters as a whole, such as `url:"/images/favicon.ico"`. Note that the characters in the double quotation marks are considered as a phrase to match logs that contain all the words in the phrase and in the same sequence. |
| \_exists\_ | `\_exists\_:key` returns logs that contains `key`. For example, `_exists_:userAgent` means to return logs that contains the `userAgent` field. |

>!
>- The syntax is case-sensitive. For example, `AND` and `OR` represent logical search operators, while `and` and `or` are regarded as common text.
>- When multiple search conditions are connected with spaces, they are regarded as in the `OR` logic. For example, `warning error` is equivalent to `warning OR error`.
>- The following special characters must be escaped: +, -, &&, ||, !, ( ), { }, [ ], ^, ", ~, *, ?, :, \
>- Use `()` to group search conditions and clarify the precedency when using the "AND" and "OR" operators, such as `(ERROR OR WARNING) AND pid:1234`.
>

### Example

| Expected Search Result | Statement |
| ------------------------------------------------------ | ------------------------------------------------------ |
| Logs of a specified server | `__SOURCE__:127.0.0.1` or `__SOURCE__:192.168.0.*` |
| Logs from a specified file | `__FILENAME__:"/var/log/access.log"` or `__FILENAME__:\/var\/log\/*.log` |
| Logs containing `ERROR` | `ERROR` |
| Searching-failed logs (Status code > 400) | `status:>400` |
| Failed logs in the `GET` request (with a status code greater than 400) | `method:GET AND status:>400` |
| Logs at `ERROR` or `WARNING` level | `level:ERROR OR level:WARNING` |
| Logs except those at the `INFO` level | `NOT level:INFO` |
| Logs from `192.168.10.10` but except those at `INFO` level | `__SOURCE__:192.168.10.10 NOT level:INFO` |
| Logs from the `/var/log/access.log` file on `192.168.10.10` but except those at `INFO` level | `(__SOURCE__:192.168.10.10 AND __FILENAME__:"/var/log/access.log") NOT level:INFO` |
| Logs from `192.168.10.10` and at `ERROR` or `WARNING` level | `__SOURCE__:192.168.10.10 AND (level:ERROR OR level:WARNING)` |
| Logs with a status code of `4XX` | `status:[400 TO 500}` |
| Logs with the container name `nginx` in the metadata | `__TAG__.container_name:nginx` |
| Logs with the container name `nginx` in the metadata, and request latency greater than 1s | `__TAG__.container_name:nginx AND request_time:>1` |
| Logs that contain the `message` field | `message:*` or `_exists_:message` |
| Logs that do not contain the `message` field  | `NOT _exists_:message` |


### Fuzzy Search

To perform a fuzzy search through CLS, you need to add wildcards to the middle or end of words, either by using the asterisk `*` to match zero, single, or multiple characters, or using the question mark `?` to match a single character. The following are examples:

- `IP:192.168.1.*` means to search for logs with an IP that starts with `192. 168.1`, such as `192. 168.1.1` and `192. 168.1.34`.
- `host:www.te?t.com` means to search for logs with a host name that starts with `www.te`, ends with `t.com`, and contains one character in the middle, such as `www.test.com` and `www.telt.com`.

>!
>
>- The asterisk `*` or question mark `?` cannot be used at the beginning of a word, that is, prefix fuzzy searches are not supported.
>- Data of `long` or `double` type does not support an asterisk `*` or question mark `?` for fuzzy search, but it supports a value range for fuzzy search, such as `status:[400 TO 500}`.
>

If you need to use prefix fuzzy search, you can use the following methods.
- Adding a delimiter: For example, if the logs are `host:www.test.com` and `host:m.test.com`, and you need to query logs containing `test` in the middle, you can add the delimiter `.` to search for logs with `host:test`.
- Using the `LIKE` syntax: For example, you can use `* | select * where host like '%test%'`. However, this method has a lower performance than the search condition method and is not suitable for scenarios with a large volume of log data.


<span id="SQLRules"></span>
## SQL Statement Syntax Rules

### Syntax rules

| Syntax | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [SELECT](https://intl.cloud.tencent.com/document/product/614/38735) | Selects data from a table. It selects eligible data from the current log topic by default. Example: `level:ERROR | select *`. The `from` clause is not required for non-nested subqueries. |
| [AS](https://intl.cloud.tencent.com/document/product/614/38731) | Specifies an alias for a column (KEY). Example: `level:ERROR | select level as log_level`. |
| [GROUP BY](https://intl.cloud.tencent.com/document/product/614/38732) | Combines aggregate functions to group results based on one column (KEY) or more. Example: `level:* | select count(*) as logCounts,level group by level `. |
| [ORDER BY](https://intl.cloud.tencent.com/document/product/614/38734) | Sorts results according to the specified `KEY`. Example: `level:* | select count(*) as logCounts,level group by level order by logCounts desc `. |
| [LIMIT](https://intl.cloud.tencent.com/document/product/614/38733) | Limits the amount of data returned by the `SELECT` statement. Example: `level:* | select count(*) as logCounts,level group by level order by logCounts desc limit 5 `. </br>Note: `limit` is 100 by default and can be up to 10000. |
| [WHERE](https://intl.cloud.tencent.com/document/product/614/38736) | Filters the raw data found. Example: `level:ERROR | select * where host like '%test%'`. </br>Note:</br>1. In SQL, search conditions deliver a higher performance than filters. We recommend you use search conditions to meet data filtering requirements. For example, you can use `status:>400 | select count(*) as logCounts` instead of `* | select count(*) as logCounts where status>400` to get the statistical result faster. </br>2. The `WHERE` statement does not allow the `AS` clause. For example, if `level:* | select level as log_level where log_level='ERROR'` is run, an error will be reported because the statement does not comply with the SQL-92 specifications. |
| [HAVING](https://intl.cloud.tencent.com/document/product/614/45884) | Filters grouped and aggregated data. The difference between `HAVING` and `WHERE` is that `HAVING` is executed on data after grouping (`GROUP BY`) and before ordering (`ORDER BY`) while `WHERE` is executed on the raw data before aggregate. Example: `level:* | select count(*) as logCounts,level group by level having count(*) > 100`. |
| [Nested subquery](https://intl.cloud.tencent.com/document/product/614/42718) | In some complex statistical analysis scenarios, you need to perform statistical analysis on the raw data first and then perform secondary statistical analysis on the analysis results. In this case, you need to nest a `SELECT` statement into another `SELECT` statement. This query method is called nested subquery. Example: `* | select compare(PV, 86400) from (select count(*) as PV)`. |

>!
> - SQL statements are case insensitive, so `SELECT` is equivalent to `select`.
> - Strings must be included in single quotation marks `''`, while characters that are unsigned or included in double quotation marks `""` indicate field or column names. For example, `'status'` indicates the string `status`, while `status` or `"status"` indicates the log field `status`.
> - When a string contains a single quotation mark `'`, you need to use `''` (two single quotation marks) to represent the single quotation mark itself. For example `'{''version'': ''1.0''}'` indicates the raw string {'version': '1.0'}. No special processing is required if the string itself contains a double quotation mark `"`.
> - You don't need to add a semicolon at the end of a SQL statement to indicate the end.
> 



### SQL functions

CLS supports a large number of SQL functions. For all the SQL functions, see [Analytic Functions](https://www.tencentcloud.com/document/product/614/36745). The following lists some common functions.

| Syntax | Description |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
|  [String function](https://intl.cloud.tencent.com/document/product/614/41291)               | String concatenation, splitting, length calculation, case conversion, and more  |
|  [Date and time functions](https://intl.cloud.tencent.com/document/product/614/41989)               | Time format conversion, statistics by time, time interval calculation, and more  |
|  [IP geographic function](https://intl.cloud.tencent.com/document/product/614/41991)               | Parsing IPs to obtain geographic information and more  |
|  [URL function](https://intl.cloud.tencent.com/document/product/614/41992)               | Obtaining domain names and parameters from URLs, encoding/decoding URLs, and more  |
|  [General aggregate function](https://intl.cloud.tencent.com/document/product/614/41995)               | Calculating the log count, maximum value, minimum value, average value, and more  |
|  [Estimation function](https://intl.cloud.tencent.com/document/product/614/41998)               | Calculating the number of unique values, percentile values (e.g., p95/p90), and more  |
|  [Type conversion function](https://intl.cloud.tencent.com/document/product/614/41999)               | Variable type conversion; often used in functions that have special requirements on the variable types of parameters  |
|  [Logical function](https://intl.cloud.tencent.com/document/product/614/42000)               | AND, OR, NOT, and other logical operations  |
|  [Operator](https://intl.cloud.tencent.com/document/product/614/38729)               | Mathematical operators (+, -, \*, /, etc.) and comparison operators (>, <, etc.)  |
|  [Conditional expression](https://intl.cloud.tencent.com/document/product/614/42001)               | Condition determination expressions such as CASE WHEN and IF  |
|  [Array function](https://intl.cloud.tencent.com/document/product/614/43565)               | Getting the elements in an array, and more  |
|  [Interval-valued comparison and periodically-valued comparison functions](https://intl.cloud.tencent.com/document/product/614/43575)               | Comparing the calculation result of the current time period with the calculation result of a time period n seconds before  |
|  [ JSON function](https://intl.cloud.tencent.com/document/product/614/43566)               | Getting JSON objects, converting JSON types, and more  |


### Example

| Expected Search Result | Statement |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| Number of logs of failed `GET` requests (with a status code greater than 400) | `method:GET AND status:>400 | select count(*) as logCounts` |
| Number of logs of failed `GET` requests (with a status code greater than 400) per minute | `method:GET AND status:>400 | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as analytic_time, count(*) as log_count group by analytic_time order by analytic_time limit 1000` |
| Top 5 URLs with the largest number of requests | `* | select count(*) as PV,URL group by URL order by count(*) desc limit 5 ` |
| URLs with an average response time greater than 1,000 ms in descending order | `* | select avg(responseTime) as time_avg,URL group by URL having avg(responseTime)>1000 order by avg(responseTime) desc limit 10000` |
| Percentage of failed requests | `* | select count_if(status>400)*100.00/count(*) as "Percentage of failed requests"` |
| Percentage of failed requests of each URL in descending order | `* | select count_if(status>400)*100.00/count(*) as "Percentage of failed requests",URL group by URL order by count_if(status>400)*100.00/count(*) desc limit 10000` </br>Or</br>`* | select "Percentage of failed requests",URL from (select count_if(status>400)*100.00/count(*) as "Percentage of failed requests",URL group by URL) order by "Percentage of failed requests" desc limit 10000` |
| Number of requests of each province | `* | select ip_to_province(ip) as province, count(*) as PV group by province order by PV desc limit 100` |



### Use limits

| Metric | Limit | Remarks |
| ----------- | -------------------------------------- | ------------------------------------------------------------ |
| Number of SQL results | Each SQL execution can return up to 10,000 results. | The default value is 100. You can adjust the limit by using the [LIMIT](https://intl.cloud.tencent.com/document/product/614/38733) syntax. |
| Memory usage | Each SQL execution can occupy up to 3 GB of server memory. | Usually, this limit can be triggered when `group by`, `distinct()`, or `count(distinct())` is used, because the fields with statistics collected have too many values after deduplication via `group by` or `distinct()`. We recommend you optimize the query statement and use fields with fewer values for group statistics, or use `approx_distinct()` instead of `count(distinct())`. |


## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, select **Search and Analysis** to enter the search and analysis page.
3. Select the **logset** and **log topic** for log search.
4. Enter a **search statement** and select a **time range** (choose the last hour, last 4 hours, last day, or last 3 days, or set a custom a time range).
5. Click **Search and Analysis**.
- If the search statement **contains only search conditions**, you can view the logs on the **Raw Data** tab. The logs are sorted in descending order by log time by default.
- If the search statement **contains SQL statements**, you can view the analysis result on the **Chart Analysis** tab and change the chart type as needed to view the statistical result more intuitively. You can compare the analysis result and the raw log by switching between the **Chart Analysis** and **Raw Data** tabs.

>?
>- On the **Chart Analysis** tab page, you can click **Add to Dashboard** to add the current chart to a new or existing dashboard.
>- When entering a search statement in the input box, you can click the **Favorites** and **Add Alarm Policy** icons on the right of the input box to save the current statement and add an alarm policy respectively.
>


## FAQs

- [Log Search Failure](https://intl.cloud.tencent.com/document/product/614/38446)
- [Search Criteria Do Not Take Effect](https://intl.cloud.tencent.com/document/product/614/45244)
- [Log Search Failure](https://intl.cloud.tencent.com/document/product/614/38446)
- [Search Analysis Error](https://intl.cloud.tencent.com/document/product/614/44224)
