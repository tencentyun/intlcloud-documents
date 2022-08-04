DBbrain supports big key analysis for Redis, which can quickly find big keys on instances and dynamically display the statistical analysis results of the top 100 big keys. This helps you locate memory usage by big keys, element information, and expiration time, so as to avoid service performance decline and insufficient memory issues caused by big keys.

> ? Currently, big key inspection is not supported for overlarge Redis clusters or Redis clusters with too many shards. You can perform an additional analysis by creating an **Ad Hoc Analysis of Big Key** task.

## Viewing the big key analysis result
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Memory Analysis** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/4dbead01e236e0b283ba439749dd3ee9.png)
2. Select a data type (based on memory, quantity, or prefix) below. The top 100 big keys of each data type are analyzed.
![](https://qcloudimg.tencent-cloud.cn/raw/49d5a4f72bb00ea3352ddfe982e1178a.png)
3. In the **MEM Utilization (Last 30 Days)** module, drag the timeline to view the big key analysis/memory status in the last 30 days.
      The trend displays the memory usage in the last 30 days. Click a day, and the time column will be fixed. At this time, the big keys on the corresponding day will be displayed in the list below.

## Ad hoc analysis of big key
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Memory Analysis** tab to view the **Ad Hoc Analysis of Big Key** feature.
![](https://qcloudimg.tencent-cloud.cn/raw/c0b74a6341d9f4e5d9f9928ecd4fc807.png)
2. Click **Create Task**, and DBbrain will fetch the last backup of the database for automatic analysis. You can view the analysis progress on the progress bar in the task list.
3. After the analysis is completed, you can view the analysis result in the task list.

