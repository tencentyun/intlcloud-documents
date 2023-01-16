## Overview

This document describes how to create a scheduled SQL analysis task.

## Prerequisites

- The CLS service has been activated, and key-value index has been enabled.
- Make sure that the current account has the permission to configure scheduled SQL analysis. For more information, see [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004).

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. Click **Data Processing** > **Scheduled SQL Task** on the left sidebar and click ![](https://qcloudimg.tencent-cloud.cn/raw/5829c3928eef93b45e7d92b840fc38cc.png) to create a task.

3. On the basic configuration page, configure the following information and click **Next**:

 - Task Name: Enter a custom task name.
 - Source Log Topic: Select the log topic where to run the SQL analysis task.
 - SQL Statement: Enter the SQL statement in **Query Statement**, and the system will return the preview results (up to 100 items).
 - Target Log Topic: Select the target log topic where to save SQL analysis results. 
4. On the scheduling configuration page, configure the following information and click **OK**.

 - Scheduling Range: Set the time range for running the scheduled task. The default value is to start at the current time and last forever, i.e., running continuously.
 - Scheduling Cycle: Set the cycle of the scheduled task, i.e., execution every X minutes. The maximum value is 1,440.
 - SQL Time Window: Set the start and end time of the SQL query log data.
<table>
<thead>
<tr>
<th>Common SQL Time Window Expression (Suppose It's 12:06 Now)</th><th style="width: 15%;">SQL Time Window</th><th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>@m-1h, @m</td>
<td>11:06 - 12:06</td>
<td>`@m` and `-1h` indicate to take the value down to the minute and subtract 1 hour, respectively. </td>
</tr>
<tr>
<td>@h-1h,@h</td>
<td>11:00 - 12:00</td>
<td>`@h` and `-1h` indicate to take the value down to the hour and subtract 1 hour, respectively. </td>
</tr>
<tr>
<td>@m-1h+20m,@h+25m</td>
<td>11:26 - 12:25</td>
<td>`@m`, `-1h`, `+20m`, `@h`, and `+25m` indicate to take the value down to the minute, subtract 1 hour, add 20 minutes, take the value down to the hour, and add 25 minutes, respectively. </td>
</tr>
</tbody></table>

## Example

The following example illustrates the configurations of the scheduling range, scheduling cycle, and SQL time window:
![](https://qcloudimg.tencent-cloud.cn/raw/0fb1e0363e137829a2ee5b020110194b.jpg)
