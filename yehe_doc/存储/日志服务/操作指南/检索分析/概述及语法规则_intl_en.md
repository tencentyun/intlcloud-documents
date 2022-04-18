## Overview

CLS provides log search and analysis capabilities. You can use search and analysis statements to search for logs that match specific conditions, or use SQL to analyze matched logs to obtain statistical results such as the number of logs, average response time, and error log percentage.

A search and analysis statement is composed of two parts, search condition and SQL statement, which are separated by a vertical bar (|).
```
[Search condition] | [SQL statement]
```

- Search condition: specifies the condition for log search. Only logs that meet the condition are returned. For example, you can use `status:404` to search for application request logs with response status code 404. For the corresponding syntax rules, see [Search Condition Syntax Rules](#RetrievesConditionalRules).
- SQL statement: performs statistical analysis on logs that meet the search condition and returns the statistical analysis result. For example, you can use `status:404 | select count(*) as logCounts` to count the number of application request logs with response status code 404. SQL statements must comply with SQL-92. For the corresponding syntax rules, see [SQL Statement Syntax Rules](#SQLRules).

>?
>- To search for logs only without statistical analysis, omit the vertical bar `|` and SQL statement.
>- If the search and analysis statement is empty, all logs in the specified time range are searched for.
>

A search condition can be used for full-text search or key-value search, depending on whether a log field is specified:
- Full-text search: no field name needs to be specified. If the value of any field in a log meets the search condition, the log is matched. For example, you can use `error` to search for all logs that contain `error`.
- Key-value search: a field name needs to be specified. If the value of a specified field in a log meets the search condition, the log is matched. For example, you can use `level:error` to search for logs whose log level is error.

## Prerequisite

- **Using a search condition**:
 - Full-text search: full-text index is enabled in index configuration.
 - Key-value search:
   - Log fields have been extracted ([Log Structuring](https://intl.cloud.tencent.com/document/product/614/31652)) during log collection.
   - Key-value index is enabled for the field to search for during [index configuration](https://intl.cloud.tencent.com/document/product/614/39594).
- **Using an SQL statement**:
 - Log fields have been extracted ([Log Structuring](https://intl.cloud.tencent.com/document/product/614/31652)) during log collection.
 - Key-value index and **statistics** are enabled for the field to search for during [index configuration](https://intl.cloud.tencent.com/document/product/614/39594).



## Search Condition Syntax Rules

### Syntax Rules

| Syntax | Description |
| :--------- | :----------------------------------------------------------- |
| AND | Logical AND operator, such as `level:ERROR AND pid:1234`. |
| OR | Logical OR operator, such as `level:ERROR OR level:WARNING`. |
| NOT | Logical NOT operator, such as `level:ERROR NOT pid:1234`. |
| () | Grouping operator, which controls the precedence of logical operations, such as `(ERROR OR WARNING) AND pid:1234`. |
| : | Colon, which is used for key-value search, such as `level:ERROR`. |
| "" | Double quotation marks, which quote a phrase to match logs that contain all the words in the phrase and in the same sequence, such as `name:"john Smith"`. |
| * | Wildcard, which is used to replace zero, one, or more characters, such as `host:www.test*.com`. </br>Prefix fuzzy queries are not supported. For more information, please see [Fuzzy Search](#.E6.A8.A1.E7.B3.8A.E6.A3.80.E7.B4.A2). </br>You can also use `key:*` to query logs where the specified field (`key`) exists. `key:*` is equivalent to `_exists_:key`. |
| ? | Wildcard, which can match one single character, such as `host:www.te?t.com`. </br>Similar to `*`, it does not support prefix fuzzy queries. |
| > | Range operator, which indicates the left operand is greater than the right operand, such as `status:>400`. |
| >= | Range operator, which indicates the left operand is greater than or equal to the right operand, such as `status:>=400`. |
| < | Range operator, which indicates the left operand is less than the right operand, such as `status:<400`. |
| <= | Range operator, which indicates the left operand is less than or equal to the right operand, such as `status:<=400`. |
| TO | Logical TO operator, such as `request_time:[0.1 TO 1.0]`. |
| [] | Range operator, which includes the upper and lower boundary values, such as `age:[20 TO 30]`. |
| {} | Range operator, which excludes the upper and lower boundary values, such as `age:{20 TO 30}`. |
| \ | Escape character. An escaped character represents the literal meaning of the character, such as `url:\/images\/favicon.ico`.</br>You can also use `""` to wrap special characters as a whole, e.g., `url:"/images/favicon.ico"`. Note that the characters in the double quotation marks are considered as a phrase to match logs that contain all the words in the phrase and in the same sequence. |
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
| Logs from the `/var/log/access.log` file on `192.168.10.10` but except those at `INFO` level | `(__SOURCE__:192.168.10.10 AND __FILENAME__:"/var/log/access.log.*") NOT level:INFO` |
| Logs from `192.168.10.10` and at `ERROR` or `WARNING` level | `__SOURCE__:192.168.10.10 AND (level:ERROR OR level:WARNING)` |
| Logs with a status code of `4XX` | `status:[400 TO 500}` |
| Logs with the container name `nginx` in the metadata | `__TAG__.container_name:nginx` |
| Logs with the container name `nginx` in the metadata, and request latency greater than 1s | `__TAG__.container_name:nginx AND request_time:>1` |
| Logs that contain the `message` field | `message:*` or `_exists_:message` |
| Logs that do not contain the `message` field  | `NOT _exists_:message` |


### Fuzzy Search

To perform a fuzzy search via CLS, you need to add wildcards to the middle or end of words, either by using the asterisk `*` to match zero, single, or multiple characters, or using the question mark `?` to match a single character. The following are examples:

- `IP:192.168.1.*` means searching for logs whose IP starts with `192. 168.1`, e.g. `192. 168.1.1`, `192. 168.1.34`.
- `host:www.te?t.com` means searching for logs whose host name starts with `www.te`, ends with `t.com` and contains 1 character in the middle, e.g. `www.test.com`, `www.telt.com`.

>!
>
>- The asterisk `*` or question mark `?` cannot be used at the beginning of a word, i.e. prefix fuzzy searches are not supported.
>- Data of `long` or `double` type does not support an asterisk `*` or question mark `?` for fuzzy search, but it supports a value range for fuzzy search, such as `status:[400 TO 500}`.
>

If you need to use fuzzy search with prefix specified, you can use the following methods.
- Adding a prefix: for example, if the logs are `host:www.test.com`, `host:m.test.com`, and you need to query logs containing `test` in the middle, you can add the prefix `. ` to search for logs with `host:test`.
- Using the `LIKE` syntax: for example, you can use `* | select * where host like '%test%'`. However, this method delivers lower performance than the search condition method and is not suitable for scenarios with large volume of log data.



## SQL Statement Syntax Rules

### Syntax Rules

| Syntax | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [SELECT](https://intl.cloud.tencent.com/document/product/614/38735) | Selects data from a table. It selects eligible data from the current log topic by default. Example: `level:ERROR | select *`. The `from` clause is not required for non-nested subqueries. |
| [AS](https://intl.cloud.tencent.com/document/product/614/38731) | Specifies an alias for a column (KEY). Example: `level:ERROR | select level as log_level` |
| [GROUP BY](https://intl.cloud.tencent.com/document/product/614/38732) | Combines aggregate functions to group results based on one column (KEY) or more. Example: `level:* | select count(*) as logCounts,level group by level ` |
| [ORDER BY](https://intl.cloud.tencent.com/document/product/614/38734) | Sorts results according to the specified `KEY`. Example: `level:* | select count(*) as logCounts,level group by level order by logCounts desc ` |
| [LIMIT](https://intl.cloud.tencent.com/document/product/614/38733) | Limits the amount of data returned by the `SELECT` statement. Example: `level:* | select count(*) as logCounts,level group by level order by logCounts desc limit 5 ` </br>Note: `limit` defaults to 100 and supports up to 10000. |
| [WHERE](https://intl.cloud.tencent.com/document/product/614/38736) | Filters the original data found. Example: `level:ERROR | select * where host like '%test%'` </br>Note:</br>1. In SQL, search conditions deliver higher performance than filters. You are advised to use search conditions to meet data filtering requirements. For example, you can use `status:>400 | select count(*) as logCounts` instead of `* | select count(*) as logCounts where status>400` to get the statistical result faster. </br>2. The `WHERE` statement does not allow the `AS` clause. For example, if `level:* | select level as log_level where log_level='ERROR'` is run, an error will be reported because the statement does not comply with the SQL-92 specifications. |
| [HAVING](https://intl.cloud.tencent.com/document/product/614/45884) | Filters grouped and aggregated data. The difference between `HAVING` and `WHERE` is that `HAVING` is executed on data after grouping (`GROUP BY`) and before ordering (`ORDER BY`) while `WHERE` is executed on the original data before aggregate. Example: `level:* | select count(*) as logCounts,level group by level having count(*) > 100` |
| [Nested Subquery](https://intl.cloud.tencent.com/document/product/614/42718) | In some complex statistical analysis scenarios, you need to perform statistical analysis on the original data first and then perform secondary statistical analysis on the analysis results. In this case, you need to nest a `SELECT` statement into another `SELECT` statement. This query method is called nested subquery. Example: `* | select compare(PV, 86400) from (select count(*) as PV)` |

>!
>- SQL statements are case insensitive, so `SELECT` is equivalent to `select`.
>- Single quotes ('') indicate strings, and double quotes ("") indicate fields and aliases.
>- You don't need to add a semicolon at the end of a SQL statement to indicate the end.


### SQL functions

CLS supports a large number of SQL functions. For all the SQL functions, see [SQL Functions](https://intl.cloud.tencent.com/document/product/614/36745). The following lists some common SQL functions.

| Syntax | Description |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
|  [String Function](https://intl.cloud.tencent.com/document/product/614/41291)               | String concatenation, splitting, length calculation, case conversion, and more  |
|  [Date and Time Function](https://intl.cloud.tencent.com/document/product/614/41989)               | Time format conversion, statistics by time, time interval calculation, and more  |
|  [IP Geographic Function](https://intl.cloud.tencent.com/document/product/614/41991)               | Parsing IPs to obtain geographic information and more  |
|  [URL Function](https://intl.cloud.tencent.com/document/product/614/41992)               | Obtaining domain names and parameters from URLs, encoding/decoding URLs, and more  |
|  [General Aggregate Function](https://intl.cloud.tencent.com/document/product/614/41995)               | Calculating the log count, maximum value, minimum value, average value, and more  |
|  [Estimation Function](https://intl.cloud.tencent.com/document/product/614/41998)               | Calculating the number of unique values, percentile values (e.g., p95/p90), and more  |
|  [Type Conversion Function](https://intl.cloud.tencent.com/document/product/614/41999)               | Variable type conversion; often used in functions that have special requirements on the variable types of parameters  |
|  [Logical Function](https://intl.cloud.tencent.com/document/product/614/42000)               | AND, OR, NOT, and other logical operations  |
|  [Operator](https://intl.cloud.tencent.com/document/product/614/38729)               | Mathematical operators (+, -, \*, /, etc.) and comparison operators (>, <, etc.)  |
|  [Conditional Expression](https://intl.cloud.tencent.com/document/product/614/42001)               | Condition determination expressions such as CASE WHEN and IF  |
|  [Array Function](https://intl.cloud.tencent.com/document/product/614/43565)               | Getting the elements in an array, and more  |
|  [Interval-Valued Comparison and Periodically-Valued Comparison Functions](https://intl.cloud.tencent.com/document/product/614/43575)               | Comparing the calculation result of the current time period with the calculation result of a time period n seconds before  |
|  [ JSON Function](https://intl.cloud.tencent.com/document/product/614/43566)               | Getting JSON objects, converting JSON types, and more  |


### Example

| Expected Search Result | Statement |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| Number of logs of failed `GET` requests (with a status code greater than 400) | `method:GET AND status:>400 | select count(*) as logCounts` |
| Number of logs of failed `GET` requests (with a status code greater than 400) per minute | `method:GET AND status:>400 | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as analytic_time, count(*) as log_count group by analytic_time order by analytic_time limit 1000` |
| Top 5 URLs with the largest number of requests | `* | select count(*) as PV,URL group by URL order by count(*) desc limit 5 ` |
| URLs whose average response time is greater than 1,000 ms in descending order | `* | select avg(responseTime) as time_avg,URL group by URL having avg(responseTime)>1000 order by avg(responseTime) desc limit 10000` |
| Percentage of failed requests | `* | select count_if(status>400)*100.00/count(*) as "Percentage of failed requests"` |
| Percentage of failed requests of each URL in descending order | `* | select count_if(status>400)*100.00/count(*) as "Percentage of failed requests",URL group by URL order by count_if(status>400)*100.00/count(*) desc limit 10000` </br>Or</br>`* | select "Percentage of failed requests",URL from (select count_if(status>400)*100.00/count(*) as "Percentage of failed requests",URL group by URL) order by "Percentage of failed requests" desc limit 10000` |
| Number of requests of each province | `* | select ip_to_province(ip) as province, count(*) as PV group by province order by PV desc limit 100` |



### Restrictions

| Metric | Limit | Remarks |
| ----------- | -------------------------------------- | ------------------------------------------------------------ |
| Number of SQL results | Each SQL execution can return up to 10,000 results. | The default value is 100. You can adjust the limit by using the [LIMIT](https://intl.cloud.tencent.com/document/product/614/38733) syntax. |
| Memory usage | Each SQL execution can occupy up to 3 GB of server memory. | Usually, this limit can be triggered when `group by`, `distinct()`, or `count(distinct())` is used, because the fields whose statistics are collected have too many values after deduplication via `group by` or `distinct()`. You are advised to optimize the query statement and use fields with fewer values for group statistics, or use `approx_distinct()` instead of `count(distinct())`. |


## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, select **Search and Analysis** to go to the search and analysis page.
3. Select the **logset** and **log topic** for log search.
4. Enter a **search and analysis statement** and select a **time range** (choose the last hour, last 4 hours, last day, or last 3 days, or set a custom a time range).
5. Click **Search and Analysis**.
- If the search and analysis statement **contains only search conditions**, you can view the logs found on the **Raw Data** tab page. The logs are sorted in descending order based on the log time by default.
- If the search and analysis statement **contains SQL statements**, you can view the analysis result on the **Chart Analysis** tab page and change the chart type as needed to view the statistical result more intuitively. You can compare the analysis result and the raw log by switching between the **Chart Analysis** and **Raw Data** tab pages.

>?
>- On the **Chart Analysis** tab page, you can click **Add to Dashboard** to add the current chart to a new or existing dashboard.
>- When entering a search and analysis statement in the input box, you can click the **Favorites** and **Add Alarm** icons on the right of the input box to save the current statement and add an alarm policy respectively.
>


## FAQs

- [Log Search Failure](https://intl.cloud.tencent.com/document/product/614/38446)
- [Search Criteria Do Not Take Effect](https://intl.cloud.tencent.com/document/product/614/45244)
- [Inaccurate Search Results](https://intl.cloud.tencent.com/document/product/614/42754)
- [Search Analysis Error](https://intl.cloud.tencent.com/document/product/614/44224)
