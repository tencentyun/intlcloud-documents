CLS supports using a datetime function for log statistics and analysis. The datetime function converts format, groups and aggregates the log collection time of each log with a long-type timestamp format in microseconds, such as `__TIMESTAMP_US__` (1597807109000000).

## Datetime Conversion Function cast

| Function Name                          | Description                                                        | Sample                                                         |
| :------------------------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| `cast(date_string as timestamp)` | Converts a long- or text-type timestamp to `TIMESTAMP`, which can be used in [time grouping function histogram](https://intl.cloud.tencent.com/document/product/614/36746#.E6.97.B6.E9.97.B4.E5.88.86.E7.BB.84.E5.87.BD.E6.95.B0-histogram) and time display | cast(1597807109000 as timestamp)<br />Result: 2020-08-19T03:18:29.000Z |

#### Parameter limits

1. Only the long-type timestamp in milliseconds (such as 1597807109000) can be converted. The timestamp in seconds or microseconds needs to first has a base conversion.
2. Only the text-type timestamp in ISO 8601 datetime format (such as 2019-12-25T16:17:01+08:00) can be converted.

#### Samples

1. Convert the CLS log collection time `__TIMESTAMP_US__` to `TIMESTAMP`.

```plaintext
* | select cast(__TIMESTAMP_US__/1000 as timestamp)
```

2. Covert log’s long-type timestamp in seconds (such as `time:1597807109`) to `TIMESTAMP`.

```
* | select cast(time*1000 as timestamp)
```



## Time Grouping Function histogram

CLS supports using the histogram function to group and aggregate log data according to a given interval. For example, you can use it to count page views every five minutes.

#### Function syntax

```
`histogram(date_expression,date_interval)`
```

#### Parameter description

- date_expression: in the `TIMESTAMP` format. You can use the cast function to convert a time string in ISO 8601 or UNIX datetime format to `TIMESTAMP`.
- date_interval: valid values are as follows:

| date_interval | Sample Value                                                   |
| :------------ | :----------------------------------------------------------- |
| MINUTE        | histogram( cast(\_\_TIMESTAMP\_US\_\_/1000 as timestamp),INTERVAL 1 MINUTE) |
| HOUR          | histogram( cast(\_\_TIMESTAMP\_US\_\_/1000 as timestamp),INTERVAL 1 HOUR) |
| DAY           | histogram( cast(\_\_TIMESTAMP\_US\_\_/1000 as timestamp),INTERVAL 1 DAY) |
| MONTH         | histogram( cast(\_\_TIMESTAMP\_US\_\_/1000 as timestamp),INTERVAL 1 MONTH) |
| YEAR          | histogram( cast(\_\_TIMESTAMP\_US\_\_/1000 as timestamp),INTERVAL 1 YEAR) |

#### Samples

Count the PV value every five minutes.

```
* | select histogram( cast(__TIMESTAMP_US__/1000 as timestamp),INTERVAL 5 MINUTE) AS time , count(*) as PV  group by time order by time
```

>!The minimum granularity of the histogram function is minute. If you need a fine granularity, we recommend using modulus operation.

```
* | select cast((__TIMESTAMP_US__ /1000-__TIMESTAMP_US__ /1000%60000) as timestamp) as time, count(1) as PV,count (distinct(remote_addr)) as UV group by time order by time
```

Where, `%60000` in the above formula refers to the aggregation by 60 seconds.

