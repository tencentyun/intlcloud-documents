The SQL statistics feature of CLS can analyze the collected logs and display the analysis results using different types of charts, such as line chart, bar chart, and pie chart. You can choose any type as needed.

## Analysis Syntax

>!
>- To use the log analysis feature, you must configure the key-value index for target fields and enable the statistics feature.
>- When you use SQL statements for search and analysis, single quotes ('') indicate strings, and double quotes ("") indicate fields and aliases.
>

An analysis statement is composed of a search rule and SQL statement, which are separated by a vertical bar (|).
```
[Search rule] | [SQL statement]
```
**Example**
```
Calculate the page views (PV) without a search criterion.
* | select count(*) as pv
```
```
Calculate the PV with status code 404 as the search criterion.
status:404 | select count(*) as pv
```
- SQL statements support the `SELECT`, `AS`, `GROUP BY`, `ORDER BY`, `LIMIT`, and `WHERE` syntax and are compatible with SQL-92. For more information, see [SQL syntax](#sql1).
- You don't need to set the `FROM` clause for SQL statements. Data from the current log topic is analyzed by default.
- You don't need to add a semicolon at the end of an SQL statement to indicate the end.
- SQL statements are case-insensitive.



## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, select **Search and Analysis** to go to the search and analysis page.
3. Select the logset and log topic you want to search for.
Set the time range. You can choose the last hour, last 4 hours, last day, or last 3 days, or set a custom a time range. 
4. Enter an analysis statement and click **Search and Analysis** to obtain the analysis result.
For more information about analysis statements, see **[SQL syntax](#sql1)** and **[SQL functions](#sql2)**. 



## Supported SQL Syntax and Functions

CLS supports the following SQL syntax and functions. You can click them to view details.

[](id:sql1)

#### SQL syntax

| Function | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [SELECT](https://intl.cloud.tencent.com/document/product/614/38735) | Selects data from tables. |
| [AS](https://intl.cloud.tencent.com/document/product/614/38731)   | Specifies an alias for a column (KEY). |
| [GROUP BY](https://intl.cloud.tencent.com/document/product/614/38732) | Combines aggregate functions to group results based on one column (KEY) or more. |
| [ORDER BY](https://intl.cloud.tencent.com/document/product/614/38734) | Sorts results according to the specified `KEY`. |
| [LIMIT](https://intl.cloud.tencent.com/document/product/614/38733) | Limits the amount of data returned by the `SELECT` statement. |
| [WHERE](https://intl.cloud.tencent.com/document/product/614/38736) | Extracts the logs that meet the specified criteria. |
| [Nested Subquery](https://intl.cloud.tencent.com/document/product/614/42718) | For some complex query scenarios, single-level SQL queries are insufficient, and nested SQL queries are required. |

[](id:sql2)

####  SQL functions

CLS supports a large number of SQL analytic functions. For all the SQL analytic functions, see [Analytic Function](https://intl.cloud.tencent.com/document/product/614/36745). The following lists some common analytic functions.

| Function | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|  [String Function](https://intl.cloud.tencent.com/document/product/614/41291)               | String concatenation, splitting, length calculation, case conversion, and more  |
|  [Date and Time Function](https://intl.cloud.tencent.com/document/product/614/41989)               | Time format conversion, statistics by time, time interval calculation, and more  |
|  [IP Geographic Function](https://intl.cloud.tencent.com/document/product/614/41991)               | Parsing IPs to obtain geographic information and more  |
|  [URL Function](https://intl.cloud.tencent.com/document/product/614/41992)               | Obtaining domain names and parameters from URLs, encoding/decoding URLs, and more  |
|  [General Aggregate Function](https://intl.cloud.tencent.com/document/product/614/41995)               | Calculating the log count, maximum value, minimum value, average value, and more  |
|  [Estimation Function](https://intl.cloud.tencent.com/document/product/614/41998)               | Calculating the number of unique values, percentile values (e.g., p95/p90), and more  |
|  [Type Conversion Function](https://intl.cloud.tencent.com/document/product/614/41999)               | Variable type conversion; often used in functions that have special requirements on the variable types of parameters  |
|  [Logic Function](https://intl.cloud.tencent.com/document/product/614/42000)               | AND, OR, NOT, and other logical operations  |
|  [Operator](https://intl.cloud.tencent.com/document/product/614/38729)               | Mathematical operators (+, -, \*, /, etc.) and comparison operators (>, <, etc.)  |
|  [Conditional Expression](https://intl.cloud.tencent.com/document/product/614/42001)               | Condition determination expressions such as CASE WHEN and IF  |
|  [Array Function](https://intl.cloud.tencent.com/document/product/614/43565)               | Getting the elements in an array, and more  |
|  [Interval-Valued Comparison and Periodically-Valued Comparison Functions](https://intl.cloud.tencent.com/document/product/614/43575)               | Comparing the calculation result of the current time period with the calculation result of a time period n seconds before  |
|  [ JSON Function](https://intl.cloud.tencent.com/document/product/614/43566)               | Getting JSON objects, converting JSON types, and more  |


## SQL Limits

| Metric | Limit | Remarks |
| ------------ | ------------------------------------- | ------------------------------------------------------------ |
| Number of analysis results | Each analysis returns up to 10,000 results. | Default: 100; maximum: 10,000 |
| Memory usage   | Each analysis can occupy up to 3 GB of server memory. | Usually, this limit can be triggered when `group by`, `distinct()`, or `count(distinct())` is used, because the fields whose statistics are collected have too many values after deduplication via `group by` or `distinct()`. You are advised to optimize the query statement and use fields with fewer values for group statistics, or use `approx_distinct()` instead of `count(distinct())`. |

