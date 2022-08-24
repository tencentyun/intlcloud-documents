Scheduled purge/prefetch tasks can be triggered through SCF. Such tasks are included in the daily purge/prefetch quota and may fail to be executed if the quota is exceeded.

## Configuration Guide

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Plugin Center** on the sidebar, click the scheduled purge/prefetch plugin feature block, and enable scheduled purge/prefetch to enter the task configuration page. After this feature is enabled, you can also click **Basic Configuration** at the bottom of the block to enter the scheduled purge/prefetch task list page for configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/b9280a8a6abff68fcd732651482e4aeb.png)

On the **Create Scheduled Task** page, select the desired task type, set the cron scheduling expression (see the example), enter the corresponding purge/prefetch URLs, and perform SCF authorization. Then, the system can automatically generate the corresponding SCF function and trigger the task as scheduled.
![](https://qcloudimg.tencent-cloud.cn/raw/f3ebd58524dbe4c0892c3a587c05b1f1.png)

>!Do not delete this function in the SCF console.

On the task status page, you can view the last execution of the scheduled task.
![](https://qcloudimg.tencent-cloud.cn/raw/80c812e712164b648b3cb57da98a8e51.png)

## Cron Expression

A cron expression contains seven values separated by spaces.

<table>
<thead>
<tr>
<th style="width:100px">Value</th>
<th>Field</th>
<th>Value Range</th>
<th>Wildcard</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>Second</td>
<td>An integer between 0 and 59</td>
<td>,  - * /</td>
</tr>
<tr>
<td>2</td>
<td>Minute</td>
<td>An integer between 0 and 59</td>
<td>,  - * /</td>
</tr>
<tr>
<td>3</td>
<td>Hour</td>
<td>An integer between 0 and 23</td>
<td>,  - * /</td>
</tr>
<tr>
<td>4</td>
<td>Day</td>
<td>An integer between 1 and 31 (the number of days in the month needs to be considered)</td>
<td>,  - * /</td>
</tr>
<tr>
<td>5</td>
<td>Month</td>
<td>An integer between 1 and 12 or JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, or DEC</td>
<td>,  - * /</td>
</tr>
<tr>
<td>6</td>
<td>Day of week</td>
<td>An integer between 0 and 6 or MON, TUE, WED, THU, FRI, SAT, or SUN, where 0 means Monday, 1 means Tuesday, and so on</td>
<td>,  - * /</td>
</tr>
<tr>
<td>7</td>
<td>Year</td>
<td>An integer between 1970–2099</td>
<td>,  - * /</td>
</tr>
</tbody></table>

Wildcards have the following meanings:

<table>
<thead>
<tr>
<th align="left" style="width:120px">Wildcard</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">, (comma)</td>
<td align="left">It represents the union of characters separated by comma; for example, 1, 2, 3 in the "Hour" field means 1:00, 2:00 and 3:00</td>
</tr>
<tr>
<td align="left">- (hyphen)</td>
<td align="left">It contains all values in the specified range; for example, in the "Day" field, 1-15 contains the 1st to the 15th day of the specified month</td>
</tr>
<tr>
<td align="left">* (asterisk)</td>
<td align="left">It means all values; for example, in the "Hour" field, * means every o'clock</td>
</tr>
<tr>
<td align="left">/ (forward slash)</td>
<td align="left">It specifies the increment; for example, in the "Minute" field, you can enter 1/10 to specify repeating every ten minutes from the first minute on (e.g., at the 11th minute, the 21st minute, the 31st minute, and so on)</td>
</tr>
</tbody></table>


>!When both the "Day" and "Week" fields in a cron expression are specified, they are in an "or" relationship, i.e., the conditions of both are effective separately.


### Sample

**One-Time task**

- `33 22 11 6 7 * 2021` means triggering the task at 11:22:33 on July 6, 2021.
- `00 00 20 25 10 * 2021` means triggering the task at 20:00:00 on October 25, 2021.

**Periodic task**

- `*/5 * * * * * *` means triggering the task once every 5 seconds.
- `0 0 2 1 * * *` means triggering the task once at 2 AM on the 1st day of every month.
- `0 15 10 * * MON-FRI *` means triggering the task once every day at 10:15 AM Monday through Friday.
- `0 0 10,14,16 * * * *` means triggering the task once every day at 10 AM, 2 PM, and 4 PM.
- `0 */30 9-17 * * * *` means triggering the task once every half hour from 9 AM to 5 PM every day.
- `0 0 12 * * WED *` means triggering the task once at 12:00 noon every Wednesday.

## Billing

The scheduled purge/prefetch feature is free of charge. However, it will call SCF to create scheduled tasks, which will incur SCF fees. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
