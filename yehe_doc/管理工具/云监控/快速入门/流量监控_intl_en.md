## Overview


In order to prevent access traffic surges from affecting your business, you need to monitor the public network outbound bandwidth of CVM in real time. This document describes the traffic monitoring feature and how to use it.



## Directions

> ?Traffic monitoring displays the aggregated data of the public network outbound bandwidth of all CVM instances. Currently, data cannot be filtered by instance or region. If you want to view the public network outbound bandwidth monitoring data of individual instances, please see [Tencent Cloud Product Monitoring](https://intl.cloud.tencent.com/document/product/248/35284).

1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Data Usage Monitoring** on the left sidebar to access the traffic monitoring page.
The real-time traffic monitoring data is displayed by default, and you can view the public network outbound bandwidth monitoring data in real time, in the last 24 hours, in the last 7 days, and using a custom time period. You can also move your cursor in the monitoring chart to view the monitoring data of a certain moment.
![](https://main.qcloudimg.com/raw/27aa4a17dc0e9c388775a73cb495557c.png)
**Table showing the correspondence between the time range and the monitoring data granularity:**
<table>
<thead>
<tr>
<th>Time Range</th>
<th>Granularity</th>
</tr>
</thead>
<tbody><tr>
<td>&lt; 1 day</td>
<td>1 minute</td>
</tr>
<tr>
<td>2–3 days</td>
<td>5 minutes</td>
</tr>
<tr>
<td>3–62 days</td>
<td>1 hour</td>
</tr>
<tr>
<td>&gt;= 62 days</td>
<td>1 day</td>
</tr>
</tbody></table>

## Data Comparison

Traffic monitoring supports monitoring data comparison. If you select **real time** or **last 24 hours**, the comparison will be made against the data at the same time yesterday by default. If you select **last 7 days**, the comparison will be made against the data at the same time last week by default. You can also customize the start time to be compared with the monitoring data in real-time, in the last 24 hours, or in the last 7 days, as shown below.
![](https://main.qcloudimg.com/raw/c3b56a841f06c1942e92c02504cb4dc9.png)

>? For more information on bill-by-bandwidth rules, please see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).

