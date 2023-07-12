This document introduces the basic syntax and examples of nested subqueries.

## Syntax Format

In some complex statistical analysis scenarios, you need to perform statistical analysis on the original data first and then perform secondary statistical analysis on the analysis results. In this case, you need to nest a `SELECT` statement into another `SELECT` statement. This query method is called nested subquery.

```
* | SELECT key FROM (subquery)
```

- subquery: subquery, which needs to be enclosed in parentheses
- key: fields that need to be obtained from a subquery for secondary statistical analysis
- Two or more levels of nesting is supported.


## Syntax Example

Calculate the ratio of the page views (PVs) of the current hour to the PVs of the same time period the day before:
Set the time range for search and analysis to 1 hour and execute the following search and analysis statement, where `86400` indicates the current time minus 86400 seconds (1 day).

**Search and analysis statement**

```
* | SELECT compare(PV, 86400) FROM (SELECT count(*) AS PV)
```
- `SELECT count(*) AS PV` is level-1 statistical analysis: analyze the website PV based on raw logs.
- `SELECT compare(PV, 86400) FROM` is level-2 statistical analysis: perform secondary statistical analysis based on the PV result of the level-1 statistical analysis. Use the [compare](https://intl.cloud.tencent.com/document/product/614/43575) function to obtain the website PV of the day before.

**Search and analysis result**


- 1860: indicates the PVs of the current 1 hour.
- 1656: indicates the PVs of the same time period the day before.
- 1.1231884057971016: indicates the ratio of the PVs of the current hour to the PVs of the same time period the day before.



To display the search and analysis result in multiple columns, perform a further nested search:

**Search and analysis statement**

```
* | 
SELECT compare[1] AS today, compare[2] AS yesterday, compare[3] AS ratio
FROM (
    SELECT compare(PV, 86400) AS compare
    FROM (
        SELECT COUNT(*) AS PV
    )
)
```
`SELECT compare[1] AS today, compare[2] AS yesterday, compare[3] AS ratio FROM` is to get the value of a specified position in the result of the `compare` function based on the array subscript.

**Search and analysis result**
