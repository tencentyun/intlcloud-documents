>? The histogram function cannot be used together with other analytic functions such as IP geographic functions and estimation functions. If the "Unknown function[Function name]" error is reported, use [Time Completion Function](https://intl.cloud.tencent.com/document/product/614/41989) to replace the function that causes the error.
>

CLS provides time functions to help convert time formats and group and aggregate the date and time values in logs for statistical analysis.

## Time Conversion Function cast

| Function Name                          | Description                                                        | Sample                                                         |
| :------------------------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| `cast(date_string as timestamp)` | Converts a long or text timestamp into `TIMESTAMP`, which can be used in [time grouping function histogram](#histogram_time) and time display  | cast(1597807109000 as timestamp)<br/>Result: 2020-08-19T03:18:29.000Z |

### Parameter limits

1. Only the long-type timestamp in milliseconds (such as 1597807109000) can be converted. The timestamp in seconds or microseconds needs to first have a base conversion.
2. Only the text timestamp in the ISO 8601 time format (such as 2019-12-25T16:17:01+08:00) can be converted.

### Examples

1. Convert the CLS log collection time `__TIMESTAMP__` to `TIMESTAMP`.
```plaintext
* | select cast(__TIMESTAMP__ as timestamp)
```
2. Covert the long-type timestamp in seconds (such as `time:1597807109`) of logs to `TIMESTAMP`.
```
* | select cast(time*1000 as timestamp)
```


<span id="histogram_time"></span>
## Time Grouping Function histogram

CLS supports a histogram function that you can use to group and aggregate the log data at a given interval. For example, you can use it to count page views (PV) every 5 minutes.

### Syntax format

```
histogram(__TIMESTAMP__, interval)
```

>?
>- The value of `\_\_TIMESTAMP\_\_` can be the value of `long` in milliseconds or a value in TIMESTAMP format. You can convert a time string in the ISO 8601 or UNIX time format to the TIMESTAMP format.
>- The value of `interval` supports the following time units: SECOND, MINUTE, HOUR, DAY, MONTH, and YEAR. For example, `INTERVAL 5 MINUTE` indicates an interval of 5 minutes.
>- The histogram function also supports the following syntax, where `long` is a timestamp in milliseconds, equivalent to the `\_\_TIMESTAMP\_\_`.
>```
histogram(long, interval)
>```



### Example

Count the PV value every 5 minutes:

```
* | select histogram(cast(__TIMESTAMP__ as timestamp),INTERVAL 5 MINUTE) AS dt, count(*) as PV group by dt order by dt limit 1000
```



  

