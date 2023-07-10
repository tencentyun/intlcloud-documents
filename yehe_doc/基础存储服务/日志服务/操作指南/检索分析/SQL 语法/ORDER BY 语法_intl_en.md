The `ORDER BY` syntax is used to sort analysis results by a specified column name.

## Syntax Format

```
ORDER BY column name [DESC | ASC]
```

>?
> - You can specify multiple column names to sort analysis results in different sorting modes, for example, `ORDER BY column name 1[DESC | ASC], column name 2[DESC | ASC]`.
> - If you do not specify the keyword `DESC` or `ASC`, the system sorts the analysis results in ascending order.
> - If the target column for sorting contains duplicated values, the sorting result may be different each time. If you want the sorting result to remain the same in each sorting, you can specify multiple columns for sorting.
>

Parameter descriptions:

| Parameter | Description |
| ---- | ---------------------------------------- |
| Column name | Group data by log field name or aggregate function calculation result column. |
| DESC | Sort data in descending order.                                                   |
| ASC  | Sort data in ascending order.                                                   |

## Syntax Example

- Count the number of requests in different states and sort them in descending order by the number of requests:
```
* | 
SELECT 
  status, 
  count(*) AS pv 
GROUP BY 
  status 
ORDER BY 
  pv DESC
```
- Calculate the average request time for each server and sort them in ascending order:
```
* | 
SELECT 
  remote_addr, 
  avg(request_time) as request_time 
group by 
  remote_addr 
order by 
  request_time ASC 
LIMIT 
  10
```

