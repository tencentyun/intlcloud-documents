CLS supports a datetime function that you can use to convert format, group and aggregate the log time for statistical analysis. Each CLS log comes with a long timestamp collection time in milliseconds, such as `__TIMESTAMP__` (1597807109000).

## Datetime Conversion Function cast

| Function Name                          | Description                                                        | Sample                                                         |
| :------------------------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| `cast(date_string as timestamp)` | Converts a long or text timestamp into `TIMESTAMP`, which can be used in [time grouping function histogram](https://intl.cloud.tencent.com/document/product/614/36746) and time display  | cast(1597807109000 as timestamp)<br/>Result: 2020-08-19T03:18:29.000Z |

#### Parameter limits

1. Only the long timestamp in milliseconds (such as 1597807109000) can be converted. The long timestamp in seconds or microseconds needs to first undergo a base conversion.
2. Only the text timestamp in the ISO 8601 datetime format (such as 2019-12-25T16:17:01+08:00) can be converted.

## Scenarios

1. Convert the CLS log collection time `__TIMESTAMP__` to `TIMESTAMP`.

```plaintext
* | select cast(__TIMESTAMP__ as timestamp)
```

2. Covert the log’s long timestamp in seconds (such as `time:1597807109`) to `TIMESTAMP`.

```
* | select cast(time*1000 as timestamp)
```



## Time Grouping Function histogram

CLS supports a histogram function that you can use to group and aggregate the log data at a given interval. For example, you can use it to count page views (PV) every five minutes.

#### Function syntax

```
`histogram(date_expression,date_interval)`
```

#### Parameter description

- date_expression: in the `TIMESTAMP` format. You can use the cast function to convert a time string in the ISO 8601 or UNIX datetime format to `TIMESTAMP`.
- date_interval: refer to the table below for valid values.

| date_interval | Sample Value                                                   |
| :------------ | :----------------------------------------------------------- |
| MINUTE        | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 MINUTE) |
| HOUR          | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 HOUR) |
| DAY           | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 DAY) |
| MONTH         | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 MONTH) |
| YEAR          | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 YEAR) |

#### Samples

Count the PV value every five minutes.

```
* | select histogram( cast(__TIMESTAMP__ as timestamp),INTERVAL 5 MINUTE) AS dt, count(*) as PV  group by dt order by dt
```

>!The minimum granularity of the histogram function is minute. If you need a finer granularity, we recommend using the modulus operation.

```
* | select cast((__TIMESTAMP__-__TIMESTAMP__%60000) as timestamp) as dt, count(1) as PV,count (distinct(remote_addr)) as UV group by dt order by dt
```

Where, `%60000` in the above formula indicates an aggregation by 60 seconds.
