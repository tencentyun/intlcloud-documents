## Overview

Setting an alarm trigger condition usually involves interval-valued comparison of metrics due to business characteristics. For example, you can set to trigger an alarm when API response time is over 50% longer than that in the same time period yesterday.





## Configuration method

When [configuring an alarm policy](https://intl.cloud.tencent.com/document/product/614/39574), enter the following query statements and trigger conditions:

**Query statements:**

```
* | select 
  round(compare[3], 4) as ratio, 
  compare[1] as current_avg_request_time, 
  compare[2] as yesterday_avg_request_time 
from 
  (
    select compare(avg_request_time, 86400) as compare 
    from 
      (
        select avg("request_time") as avg_request_time
      )
  )
```
In the execution result of the above statements:

* `ratio` indicates the ratio of the current average API response time to the value yesterday (86,400 seconds earlier).
* `current_avg_request_time` indicates the current average API response time.
* `yesterday_avg_request_time` indicates the average API response time in the same period yesterday.

The `compare` function is used in the above statement. For more information, see [Interval-Valued Comparison and Periodicity-Valued Comparison Functions](https://intl.cloud.tencent.com/document/product/614/43575).



**Trigger conditions:**

```
$1.ratio > 1.5
```

An alarm will be triggered if `ratio` exceeds `1.5`, that is, the time is over 50% longer than that yesterday.
