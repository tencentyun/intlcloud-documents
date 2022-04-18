The `HAVING` syntax is used to filter grouped and aggregated data. The difference between `HAVING` and [WHERE](https://intl.cloud.tencent.com/document/product/614/38736) is that `HAVING` is executed on data after grouping (`GROUP BY`) and before ordering (`ORDER BY`) while `WHERE` is executed on the original data before aggregation.

## Syntax Format

```
* | SELECT column, aggregate function GROUP BY [ column name | alias | serial number ] HAVING aggregate function operator value
```

The operator can be `=`, `<>`, `>`, `<`, `>=`, `<=`, `BETWEEN`, `IN`, or `LIKE`.

## Syntax Example

Get URLs whose average response time is greater than 1,000 ms in descending order:
```
* | 
select 
  avg(responseTime) as time_avg, 
  URL 
group by 
  URL 
having 
  avg(responseTime)> 1000 
order by 
  avg(responseTime) desc 
limit 
  10000
```

The filter condition is the average response time of each URL, which is the aggregate result, and therefore, [WHERE](https://intl.cloud.tencent.com/document/product/614/38736) cannot be used for data filtering.

