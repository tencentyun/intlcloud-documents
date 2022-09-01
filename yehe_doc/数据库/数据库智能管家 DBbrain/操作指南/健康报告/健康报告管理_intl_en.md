## Feature Description

The health report feature can routinely perform health checks on database instances and output the corresponding health reports for the specified time range, which helps you gain in-depth insights into the database instance health, failures, and potential risks and provides professional optimization suggestions for your reference.
>?Currently, the health report feature is supported for TencentDB for MySQL (excluding basic single-node instances), TDSQL-C for MySQL, self-built MySQL, TencentDB for Redis, and TencentDB for MongoDB.
>
## Creating a Health Report
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Health Report** tab. You can view the health score trends and the problem overview for the specified time range.
- Click **Create Health Report** to create a task. After the task is completed, you can view or download the health report for the specified time range. For more information on how to send health reports to a recipient via email, see [Health Report Email Push](https://intl.cloud.tencent.com/document/product/1035/39371).
>?The time range of the health report is the same as that selected on the left.
- Click **Regular Generation Settings** to configure the time range for automatically generating health reports. For more information on how to send health reports to a recipient via email, see [Health Report Email Push](https://intl.cloud.tencent.com/document/product/1035/39371).
![](https://main.qcloudimg.com/raw/60420696f50da3e8d4b2bd7de0a69065.png)

## Generating Health Reports in Batches

DBbrain supports batch health report settings for multiple instances. This makes it easier for you to manage multiple instances under your account in a unified manner.

1. On the **Instance Management** page, select multiple instances for which to generate health reports and click **Health Report**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e2071f51a5c270d5a919934a5f434101.png)
2. In the pop-up window, set the **Report Generation Time**, **Sending Time**, **Recipient**, and **Overwrite Original Configuration** and click **OK**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b928f51676bc077b3d4a7a0664074912.png)

## Configuring a Health Report

Select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, select the **Report Settings** tab, and customize regular health report sending/receiving as needed.
![](https://main.qcloudimg.com/raw/700a3524ee26396d3a199f2af064f8b8.png)
- Currently, TencentDB for MySQL, TDSQL-C for MySQL, and TencentDB for Redis support performance optimization reports and kill operation reports, while self-built MySQL and TencentDB for MongoDB support performance optimization reports only.
![](https://qcloudimg.tencent-cloud.cn/raw/84a14acaa23196bf6614ded7a6b12024.png)
- When enabling the regular health report for the first time, you need to configure the **Generation Lifecycle**, **Recipient**, and **Security Level** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/59c687ba5a5bc429594b0e3e21b06919.png)

## Viewing/Downloading a Health Report

In the **Score Details** section on the **Health Report** page, you can view instance score details for database availability, maintainability, performance, and reliability. For more information, see [Exception Alarm](https://intl.cloud.tencent.com/document/product/1035/37177).

- In the task list, the **Type**, **Health Level**, **Creation Time**, **Time Range**, **Progress**, and **Operation** of each health report task are displayed.
 - The **Type** column displays how the report is generated, including **Database Inspection**, **Manual Trigger**, and **Scheduled**.
 - The **Health Level** column displays the health level obtained through diagnosis, including **Healthy**, **Sub-healthy**, **Dangerous**, and **High-risk**.
- Click **View** in the **Operation** column to view the health report details and download the report as a PDF file.
- Click **Email** in the **Operation** column or click **Batch Send** after selecting multiple health report records to email the health reports to the specified recipient. For more information, see [Health Report Email Push](https://intl.cloud.tencent.com/document/product/1035/39371).
- Click **More** > **Deduction Details** in the **Operation** column to view the reason for the deduction of health report task scores.
- Select **More** > **Delete** in the **Operation** column to delete the health report task.

## Reading a Health Report
A health report displays DBbrain's evaluation of the overall operation conditions of the selected database instance in the specified time range. Items in the report includes the database's existing problems, an analysis of existing problems, and corresponding suggestions, helping you gain a comprehensive understanding of the overall operation status of the selected instance and coordinate relevant personnel to troubleshoot issues.

A report mainly contains the following sections: overview, basic information, health, instance status, exception diagnosis, slow SQL analysis, big table analysis, big key analysis, and performance curve.
![](https://main.qcloudimg.com/raw/7b72c424b10c1abd1572c0f6ee64f2de.png)

#### Appendix
#### Definitions of reported exception levels
| No. | Type | Description |
| ---- | ---- | ------ |
| 1 | Critical | The value is 1 |
| 2 | Serious | The value is 2 |
| 3 | Alarm | The value is 3 |
| 4 | Note | The value is 4 |
| 5 | Healthy | The value is 5 |

#### Definitions of reported health levels
| No. | Type | Description |
| ---- | ------ | --------------------- |
| 1 | Healthy | Score ≥ 95 |
| 2 | Sub-healthy |80 ≤ score < 95 |
| 3    | Dangerous   | 60 ≤ score < 80 |
| 4 | High-risk | Score < 60 |

