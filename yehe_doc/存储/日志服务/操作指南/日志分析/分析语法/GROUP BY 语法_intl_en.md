

The `GROUP BY` statement is used to combine aggregate functions to group results based on one or more columns (KEY).

## GROUP BY Syntax Format

`GROUP BY` supports arbitrary expressions, so you can use columns, aliases, and serial numbers (starting from 1).
`GROUP BY` supports one single column and multiple columns.
`GROUP BY` is often used together with [aggregate functions](https://intl.cloud.tencent.com/document/product/614/38728) such as `MIN`, `MAX`, `AVG`, `SUM`, and `COUNT`.

```sql
SELECT column (KEY), aggregate function
GROUP BY [ column (KEY) | alias | serial number ]
```

## GROUP BY Syntax Sample

#### GROUP BY for one column

Count the number of access requests with different status codes:
```sql
SELECT status, COUNT(status) AS PV GROUP BY status
```

The ISO 8601 time format (2019-09-29T20:24:57+08:00) can be converted to the `TIMESTAMP` type through CAST. Then, the `HISTOGRAM` function can be used to aggregate the time granularity and count the number of requests per minute:

```sql
SELECT HISTOGRAM(CAST(time_iso8601 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, COUNT(1) AS pv GROUP BY dt
```

#### GROUP BY for multiple columns

Count the number of access requests in different types at the 1-minute granularity:
```sql
SELECT HISTOGRAM(CAST(time_iso8601 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, COUNT(1) AS pv, method GROUP BY dt, method
```
