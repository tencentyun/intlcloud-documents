This document describes how to create an alarm silence rule.


## Directions
1. Log in to the CM console and go to the [Silence Alarm](https://console.cloud.tencent.com/monitor/alarm2/shield) page.
2. Click **Create Silence Rule** and configure the following in the pop-up window:

| Configuration item                    | Description                                                         |
| :------------------------ | :----------------------------------------------------------- |
| Name                      | The custom silence rule name.                                           |
| Monitoring Type                  | Currently, only **Tencent Cloud services** is supported.                                         |
| Policy Type                  | Select a policy type for alarm silencing as needed.                                     |
| Silence Object                  | Enter the ID(s) of the instance(s) you want to silence and separate them by comma, such as “ins-abc0zj4z,ins-abckwosm”. |
| Metric                      | The metric of a specified instance of a specified Tencent Cloud service. <li>If you don’t select any metrics, the alarm silence rule will take effect for all metrics. </li><li>If you select a metric, the silence rule will only take effect for that metric. |
| Validity Period - “Permanently”     | If you select “Permanently”, you will not receive any alarm notifications for the specified metric of a specified Tencent Cloud service’s instance, as long as the silence rule is enabled. |
| Validity Period - “Specified time range” | If you select “Specified time range”, the alarm silence rule will take effect in the time range you specify. <li>Absolute time range: The silence rule only takes effect in the specified time range (in “YYYY-MM-DD HH:mm:ss” format). <li>Relative time range (loop every day): By default, the silence rule takes effect in the specified time range (in “HH:mm:ss” format) every day. You can also select the “Loop date” option to specify the date range. For example, if you select a time range of 10:00-11:00 and a date range of 2022-06-01 - 2022-06-30, the silence rule will take effect in 10:00-11:00 every day between June 1, 2022 and June 30, 2022. |

![](https://qcloudimg.tencent-cloud.cn/raw/9d8d682ba71f23e7281e748dce042c0e.png)
