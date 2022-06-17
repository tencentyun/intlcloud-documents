This document introduces the basic syntax and examples of interval-valued comparison and periodicity-valued comparison functions.

CLS supports the interval-valued comparison and periodicity-valued comparison functions listed in the table below.

<table>
	<tr><th>Function</th><th>Syntax</th><th>Description</th></tr>
	<tr><td rowspan =2><a href="#compare">compare</a></td><td>compare(x,n)</td><td>Compares the calculation result of the current time period with the calculation result of a time period n seconds before.</td></tr>
	<tr><td>compare(x,n1,n2,n3...)</td><td>Compares the calculation result of the current time period with the calculation results of time periods n1, n2, and n3 seconds before.</td></tr>
</table>

<span id="compare"></span>
## compare

The `compare` function is used to compare the calculation result of the current time period with the calculation result of a time period n seconds before.

### Syntax

- Compare the calculation result of the current time period with the calculation result of a time period n seconds before:
```
compare (x, n)
```
- Compare the calculation result of the current time period with the calculation results of time periods n1, n2, and n3 seconds before:
```
compare (x, n1, n2, n3...)
```

### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------------------------ |
| x    | The parameter value is of the double or long type.                           |
| n    | Time window. Unit: seconds. Example: 3600 (1 hour), 86400 (1 day), 604800 (1 week), or 31622400 (1 year). |

### Return value type

JSON array in the following format: [the current calculation result, the calculation result n seconds before, the ratio of the current calculation result to the calculation result of n seconds before].

### Example

#### Example 1. Calculate the ratio of the page views (PVs) of the current hour to the PVs of the same time period the day before.

Set the time range for query and analysis to 1 hour and execute the following query and analysis statement, where `86400` indicates the current time minus 86400 seconds (1 day).

- Query and analysis statement
```
* | SELECT compare(PV, 86400) FROM (SELECT count(*) AS PV)
```
- Query and analysis result

 - 1860: indicates the PVs of the current 1 hour.
 - 1656: indicates the PVs of the same time period the day before.
 - 1.1231884057971016: indicates the ratio of the PVs of the current hour to the PVs of the same time period the day before.
- To display the query and analysis result in multiple columns, execute the following query and analysis statement:
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
- Query and analysis result


#### Example 2. Calculate the trend of the PVs of every 5 minutes today to the trend of the PVs of the same time period the day before.

Set the time range for query and analysis to Today and execute the following query statement. `86400` indicates the current time minus 86400 seconds (1 day), and `current_date` indicates the date of the current day.

>! The time range cannot span days. The reason is as follows: in this example, the log time is truncated to `%H:%i:%s`, which contains only the hour, minute, and second but does not contain the date. If the time range spans days, data statistics errors will occur.
>

- Query and analysis statement
```
* | 
select concat(cast(current_date as varchar),' ',time) as time,compare[1] as today,compare[2] as yesterday from (
    select time,compare(pv, 86400) as compare from (
        select time_series(__TIMESTAMP__, '5m', '%H:%i:%s', '0')  as time, count(*) as pv group by time limit 1000) 
    limit 1000)
order by time limit 1000
```
- Query and analysis result




