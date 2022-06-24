## Feature Description

Based on the metric data collected by smart monitoring, the exception diagnosis feature diagnoses and analyzes database exceptions around the clock. For database performance problems, it leverages the analysis results of the SQL optimization, performance analysis, and rule engines to present the current and historical instance health scores and risk levels, with regard to specification configuration, SQL analysis, business logic, and usage rationality. This gives you a visual, clear, and quick picture of the running status of your database instances.


## Viewing Performance Optimization
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and select **Performance Optimization** on the left sidebar.
2. On the **Performance Optimization** page of **DBbrain**, select **Exception Diagnosis** to view the exception diagnosis details.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f67a45c7e72f96c4314dae83c9e1120e.png" style="zoom: 80%;" />

## Overview

In the **Overview** section, the TencentDB for Redis instance's health score trend and risk level as diagnosed through health inspection in the last hour are displayed by default. Click **Historical** in the top-right corner and select a past time period to view the specific health score and inspection diagnosis result.
![](https://qcloudimg.tencent-cloud.cn/raw/6b7d94a75bd4521aadb4ed17edb3a2d8.png)
Below the **Overview** section, your instance's health score and node alarms and exceptions at the current time point are displayed.

- Your database instance's current health score and the statistics of the current resource monitoring metrics are displayed, including the utilizations of CPU, memory, connection, inbound traffic, and outbound traffic, as well as read request hit rate, so you can quickly check the database resource usage. Click **Details** below **Health Score** to enter the **Health Report** tab, where you can view the health score details.
- In addition, your database's system distribution architecture diagram is displayed. You can view the proxy, master, and replica nodes and the numbers of their respective alarms and exceptions. You can also hover over a node to view the monitoring data of its key metrics. For more information on monitoring metrics, see [Performance Trends](https://intl.cloud.tencent.com/document/product/239/47579).
![](https://qcloudimg.tencent-cloud.cn/raw/4450e26a49944047883da86279987b71.png)

## Diagnosis Prompt

In the **Diagnosis Prompt** section, the diagnosis data of the database health inspection in the last 3 hours is displayed as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/880dda4f271e0a6168a3bfa602ea02b6.png" style="zoom:60%;" />

- **Risk Distribution**: The proportions of the risk levels as diagnosed through the database health inspection in the last 3 hours are displayed from high to low, including **Critical**, **Serious**, **Alarm**, and **Note**. If the proportions of all risk levels are 0%, the database is **Healthy**.
- **Diagnosis Details**: The details of the database risk level are collected once every 10 minutes. You can hover over any exception alarm to view, ignore, or unignore alarms of the same type.
<table>
<thead>
<tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Level</td>
<td>Diagnosed risk level, including **Critical**, **Serious**, **Alarm**, **Note**, and **Healthy**, from high to low.</td></tr>
<tr>
<td>Start Time</td>
<td>Start time of the health inspection. A health inspection is initiated once every 10 minutes.</td></tr>
<tr>
<td>Item</td>
<td>Diagnosis type of the risk level, such as health inspection and incorrect command.</td></tr>
<tr>
<td>Duration</td>
<td>Duration of the risk level.</td></tr>
<tr>
<td>View</td>
<td>Click <strong>View</strong> to view the details of exceptions identified during the health inspection as shown below:</td></tr>
<tr>
<td>Ignore</td>
<td>Click <strong>Ignore</strong> and then click <strong>OK</strong> in the <strong>confirmation</strong> window, and exception alarms triggered by the same cause will be ignored.</td></tr>
<tr>
<td>Unignore</td>
<td>Click <strong>Display Ignored Items</strong> in the top-right corner of the <strong>Diagnosis Details</strong> section. In the diagnosis details list, hover over an ignored item and click <strong>Cancel</strong>, and all exception alarms triggered by the same cause will be unignored.</td></tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/f40247a603b74b3aa7480e85ec89dd28.png"  style="zoom:80%;">


