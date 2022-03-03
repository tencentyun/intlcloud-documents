## Time Grouping Function histogram

CLS supports a histogram function that you can use to group and aggregate the log data at a given interval. For example, you can use it to count page views (PV) every 5 minutes.

#### Function syntax

```
`histogram(date_expression,date_interval)`
```

#### Parameter description

- date_expression: in the `TIMESTAMP` format. You can use the cast function to convert a time string in the ISO 8601 or UNIX datetime format to `TIMESTAMP`.
- date_interval: valid values are as follows:

| date_interval | Sample Value                                                   |
| :------------ | :----------------------------------------------------------- |
| MINUTE        | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 MINUTE) |
| HOUR          | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 HOUR) |
| DAY           | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 DAY) |
| MONTH         | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 MONTH) |
| YEAR          | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 YEAR) |

#### Example

Count the PV value every 5 minutes:

```
* | select histogram( cast(__TIMESTAMP__ as timestamp),INTERVAL 5 MINUTE) AS dt, count(*) as PV  group by dt order by dt
```

>! The minimum granularity of the histogram function is minute. If you need a finer granularity, we recommend using the modulus operation.
>

```
* | select cast((__TIMESTAMP__-__TIMESTAMP__%60000) as timestamp) as dt, count(1) as PV,count (distinct(remote_addr)) as UV group by dt order by dt
```

Where, `%60000` in the above formula refers to the aggregation by 60 seconds.
