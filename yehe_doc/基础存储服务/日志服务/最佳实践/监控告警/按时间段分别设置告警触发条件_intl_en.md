## Overview

For business nature reasons, different alarm trigger conditions need to be set for different time periods. For example, an alarm should be triggered when the number of logs containing errors exceeds 100 during work hours (9:00 AM to 6:00 PM) or when this number exceeds 10 during off hours (7:00 PM to 8:00 AM).

## Configuration method

When [configuring an alarm policy](https://intl.cloud.tencent.com/document/product/614/39574), enter the following query statements and trigger conditions:



**Query statement 1:**
```
error | select count(*) as error_count
```
Count logs containing errors

**Query statement 2:**
```
* | select hour(now()) as hour limit 1
```
Use [date and time functions](https://intl.cloud.tencent.com/document/product/614/41989) to get the alarm hour, i.e., at which hour the alarm is triggered.

**Trigger conditions:**
```
($1.error_count>100 && $2.hour>=9 && $2.hour<=18 ) || ($1.error_count>10 && ($2.hour<9 || $2.hour>18))
```

Use the [trigger condition expression](https://intl.cloud.tencent.com/document/product/614/39576) to specify a trigger condition and threshold. Here, `$1.error_count>100 && $2.hour>=9 && $2.hour<=18` indicates to trigger an alarm when `error_count` exceeds 100 between 9:00 AM and 6:00 PM, while `$1.error_count>10 && ($2.hour<9 || $2.hour>18)` indicates to trigger an alarm when `error_count` exceeds 10 between 7:00 PM and 8:00 AM.
