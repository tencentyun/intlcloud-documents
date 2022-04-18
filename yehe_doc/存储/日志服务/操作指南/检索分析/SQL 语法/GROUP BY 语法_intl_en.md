The `GROUP BY` syntax, together with an [aggregate function](https://intl.cloud.tencent.com/document/product/614/41995), is used to group analysis results by one or more columns.

## Syntax Format

```
* | SELECT column, aggregate function GROUP BY [ column name | alias | serial number ]
```

>! When executing a `SELECT` statement containing the `GROUP BY` syntax, you can select only the `GROUP BY` column or an aggregate calculation function, but not a non-GROUP BY column. For example, `* | SELECT status, request_time, COUNT(*) AS PV GROUP BY status` is an invalid analysis statement because **request_time** is not a `GROUP BY` column.
>

The `GROUP BY` syntax supports grouping by column name, alias, or serial number, as described in the following table:

| Parameter | Description |
| -------- | ------------------------------------------------------------ |
| Column name     | Group data by log field name or aggregate function calculation result column. The syntax supports grouping data by one or multiple columns.             |
| Alias     | Group data by alias of the log field name or aggregate function calculation result.                 |
| Serial number     | Serial number (starting from 1) of a column in the `SELECT` statement.<br>For example, the serial number of the `status` column is 1, and therefore the following statements are equivalent:<ul  style="margin: 0;"><li>`* |SELECT status, count(*) AS PV GROUP BY status`</li><li>`* |SELECT status, count(*) AS PV GROUP BY 1` </li></ul>|
| Aggregate function | The `GROUP BY` syntax is usually used together with aggregate functions such as `MIN`, `MAX`, `AVG`, `SUM`, and `COUNT`. For more information, please see [Aggregate Function](https://intl.cloud.tencent.com/document/product/614/41995). |

## Syntax Example

- Count the number of access requests with different status codes:
```
* | SELECT status, count(*) AS pv GROUP BY status
```

- Calculate PV by the time granularity of 1 minute:
```
* | 
SELECT 
  date_trunc(
    'minute', 
    cast(__TIMESTAMP__ as timestamp)
  ) AS dt, 
  count(*) AS pv 
GROUP BY 
  dt 
ORDER BY 
  dt 
limit 
  10
```
The `\_\_TIMESTAMP\_\_` field is the reserved field in CLS and indicates the time column. **dt** is the alias of `date_trunc('minute', cast(\_\_TIMESTAMP\_\_ as timestamp))`. For more information on the date_trunc() function, see [Time Truncation Function](https://intl.cloud.tencent.com/document/product/614/41989).

>?
> - `limit 10` indicates up to 10 rows of results are obtained. If the `LIMIT` syntax is not used, CLS obtains 100 rows of results by default.
> - If you enable the statistics feature for any field during index configuration, CLS will automatically enable the statistics feature for the `\_\_TIMESTAMP\_\_` field.
>
- Calculate PV and UV by the time granularity of 5 minutes:
The date_trunc() function collects statistics only at fixed time intervals. You can use the histogram function to collect statistics at custom time intervals.
```
* | 
SELECT 
  histogram(
    cast(__TIMESTAMP__ as timestamp), 
    interval 5 minute
  ) as dt, 
  count(*) as pv, 
  count(
    distinct(remote_addr)
  ) as uv 
group by 
  dt 
order by 
  dt
```


