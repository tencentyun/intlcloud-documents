CLS provides the SQL statistics feature for analyzing the collected log data and graphically displaying the analysis results. It offers a range of statistical charts including line chart, histogram, and pie chart to suit your needs.

>!This feature is currently in allowlist beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.



## Analysis Syntax

>!To use the CLS analysis feature, the key-value index of statistical fields must be configured, with statistics enabled.

The analysis statement is composed of search criterion and SQL statement, which are separated by vertical bar (|).
```
[Search criterion] | [SQL statement]
```
**Examples**
```
Calculate the page view (PV) value without a search criterion
* | select count(*) as pv
```
```
Calculate the PV value with the search criterion of status code 404
status:404 | select count(*) as pv
```
- The SQL statement currently supports syntax including `select`, `as`, `group by`, `order by`, `limit` and `where`. For more information, see [SQL syntax](#sql1).
- You don’t need to set the `from` clause for a SQL statement to analyze data of the current log topic by default.
- The SQL statement does not necessarily end with a semicolon.
- The SQL statement is case-insensitive.



## Directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Select **Log Search** on the left sidebar to enter the **Search Analysis** page.
3. Select the logset and log topic you want to search.
   Set the time range. You can choose an option from last 1 hour, last 4 hours, last 1 day, last 3 days or customize a time range. 
4. Enter an analysis statement and click **Search Analysis** to get the result.
   Refer to [SQL syntax](#sql1) and [SQL analytic function](#sql2) for more information about the analysis statement. 




## SQL Syntax and Function

CLS supports the following SQL syntax and functions.

<span id="sql1"></span>

#### SQL syntax

| Syntax                                                         | Semantics                                                       |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| SELECT | Selects data from the table.                             |
| AS       | Specifies an alias for KEY.                                    |
| GROUP BY | Combines the aggregate function and groups the result set by the KEY(s). |
| ORDER BY | Sorts the result set by the specified KEY.                         |
| LIMIT | Limits the data volume returned from the `SELECT` statement.                      |
| WHERE   | Collects logs that meet the specified criterion.                            |


<span id="sql2"></span>

#### SQL function

- Aggregate function
  Support avg, count, max, min and sum functions
- Mathematical function
  Support abs, sqrt, power, round, floor, log and log10 functions
- [Datetime function](https://intl.cloud.tencent.com/document/product/614/36746)
  Support cast and histogram functions
- Operator
  Support mathematics (+, -, *, /, %), comparison (=, number comparison, in, like, etc.) and logic (and, or, or) operators

## SQL Limits

| Metric | Limit | Remarks                                                       |
| ---------------------------------------- | ------------------------------------------------------------ | --------------------------- |
| Maximum length of a single statistical field (Value)          | The maximum length of a single statistical field (Value) is 32 KB. Any statement exceeding this limit will be truncated.                              | -                           |
| Number of non-cluster analysis results (excluding GROUP BY clause) | Each analysis returns up to 1,000 results.                              | Default: 100; Maximum: 1,000                                 |
| Number of cluster analysis results (including GROUP BY clause) | Each analysis returns up to 100 results.                              | Default: 100; Maximum: 1,000                                 |
| ORDER BY clause limit                        | The ORDER BY operation is not supported for fields that have been computed using one of the functions `round`, `sqrt`, `abs`, `power`, and `floor`, or the four arithmetic operators. |                                         -                     |
