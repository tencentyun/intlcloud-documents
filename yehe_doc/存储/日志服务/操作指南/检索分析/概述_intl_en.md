CLS provides the SQL statistics and compute feature. It supports analyzing the collected log data and graphically displays the analysis results.

## Directions

You can use common SQL statements to analyze the log data collected. Before doing this, make sure the log data has been collected and the fields to analyze have key-value pair index and statistics enabled.

Follow the instructions below:

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Select **Log Search** in the left sidebar to enter the **Log Search** page.
3. Select the time range, logset, and log topic.
   You can choose an option from last 1 hour, last 4 hours, last 1 day, last three days or customize a time range. 
4. Enter the SQL **Analysis Statement**, and click **Search Analysis** to get the result.
   The analysis statement must start with `SELECT`. For more information, see [SQL analysis syntax](#sql1) and [SQL analytic function](#sql2). 

## Result Presentation

You will see the CLS log search and analysis results in charts.

Only the search using **Analysis Statement** (starting with `SELECT`) will return the statistical result in charts.



CLS provides multiple statistical charts including tables, line charts and histograms to meet your analysis requirements. You can choose a type to present the analysis result (table will be used by default).



## SQL Statement Structure

- The analysis statement must start with `SELECT`.
- There is no need to enter the `from` clause. By default, the current log topic will be queried, and the subquery is not supported.
- The supported clauses include `SELECT`, `GROUP BY`, `ORDER BY [ASC,DESC]`, `LIMIT` and `AS`.
- The SQL statement does not necessarily end with a semicolon.
- The SQL statement is case-insensitive.
 Sample:
```sql
SELECT HISTOGRAM(CAST(time_iso8601 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt
     COUNT(1) AS pv, 
     DISTINCT(client_ip)  AS uv
     WHERE http_status < 400
     GROUP BY bucket
     ORDER BY dt
     LIMIT 100
```



## SQL Syntax and Function

CLS supports the following SQL syntax and functions.

<span id="sql1"></span>

#### SQL syntax

| Syntax         | Semantics                                                        |
| ------------ | ----------------------------------------------------------- |
| SELECT   | Selects data from the table.                             |
| AS       | Specifies an alias for KEY.                                    |
| GROUP BY| Combines the aggregate function and groups the result set by the KEY(s). |
| ORDER BY | Sorts the result set by the specified KEY.                         |
| LIMIT   | Limits the data volume returned from the `SELECT` statement.                      |
| WHERE   | Extract logs that meet the specified criteria.                            |


<span id="sql2"></span>

#### SQL functions
- Aggregate functions
- Time functions
- Mathematical functions
- Operators


>!
> - The CLS server classifies your input into analysis statement or search statement. The statement starting with `SELECT` will be considered as SQL analysis statement, otherwise as the search statement.
> - Compared with the standard SQL syntax, CLS analysis statement uses the `topic` field of the analysis API to specify the log topic to analyze, instead of setting the `From` clause.

