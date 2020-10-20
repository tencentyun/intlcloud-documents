The health report feature can routinely perform health checks on database instances and output the corresponding health reports for the specified time period, helping you gain in-depth insights into the health, failures, and risks of the database instance and providing you with professional optimization suggestions.

>?Currently, health report is supported only for TencentDB for MySQL (excluding the Basic Edition).

## Creating a Health Report
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Diagnosis and Optimization** on the left sidebar, and select **Health Report** at the top. You can view the health score trends and the problem overview for the specified time period.
- Click **Create Health Report** to create a task. After the task is completed, you can view or download the health report for the specified time period.
>?The time period of the health report is the same as that selected on the left.
- Click **Regular Generation Settings** to configure the time period for automatically generating health reports.
![](https://main.qcloudimg.com/raw/60420696f50da3e8d4b2bd7de0a69065.png)

## Viewing/Downloading a Health Report
- In the task list, the creation time, start and end times, health level, progress, and operations of each health report task are displayed.
- You can click **View/Download PDF Report** in the **Operation** column to view the health report details and download the report as a PDF file.
- You can click **Delete** in the **Operation** column to delete the health report task.
![](https://main.qcloudimg.com/raw/e533edfaf0b274b1d28921b323444de3.png)

## Interpreting a Health Report
A health report displays DBbrain's evaluation of the overall operation conditions of the selected database instance in the specified time period. Items in the report includes the database's existing problems, an analysis of existing problems, and corresponding suggestions, helping you gain a comprehensive understanding of the overall operation status of the selected instance and coordinate relevant personnel to troubleshoot issues.

A report contains the following sections: overview, basic information, health, instance status, exception diagnosis, slow SQL analysis, big table analysis, and performance curve.
![](https://main.qcloudimg.com/raw/0c9c419181dbd916fef71d1a23ec33fb.png)

#### Appendix
#### Reported exception level definitions

| No. | Type | Description |
| ---- | ---- | ------ |
| 1 | Fatal | The value is 1 |
| 2 | Severe | The value is 2 |
| 3 | Warning | The value is 3 |
| 4 | Notice | The value is 4 |
| 5 | Healthy | The value is 5 |

#### Reported health level definitions
| No. | Type | Description |
| ---- | ------ | --------------------- |
| 1    | Healthy   | Score ≥ 95         |
| 2    | Suboptimal |80 ≤ score < 95 |
| 3    | Risky   | 60 ≤ score < 80 |
| 4    |  Critical  | Score < 60         |

