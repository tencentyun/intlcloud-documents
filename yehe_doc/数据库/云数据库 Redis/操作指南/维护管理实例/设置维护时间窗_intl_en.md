## Overview
Maintenance time is a very important concept for TencentDB for Redis. To ensure the stability of your TencentDB for Redis instance, the backend system performs maintenance operations, locates exceptions, and fix failures on the instance during the maintenance time. We highly recommend you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.

In addition, we also recommend you perform operations involving data migration during the maintenance time, such as instance version or architecture upgrade. Taking the database instance version upgrade as an example, as syncing the full and incremental data involves data migration, after the upgrade is completed, a momentary disconnection from the database may occur. When the upgrade is initiated, the **Switch Time** can be selected as **During maintenance time**, so that the instance version switch will be started during the next **maintenance time** after the data sync is completed. Note that when you select **During maintenance time** for **Switch Time**, the switch will not occur immediately after the database version upgrade is completed; instead, the sync will continue till the instance goes into the next **maintenance time**, during which the switch will be performed. Therefore, the overall time it takes to upgrade the instance may be longer.

>?Before maintenance is carried out for TencentDB for Redis during the maintenance time, notifications will be sent to the contacts configured in your Tencent Cloud account through SMS and email.

## Version Requirement
The maintenance time is 03:00–04:00 AM by default, which can be adjusted as needed on all Redis versions.

## Prerequisites
- You have created a [TencentDB for Redis instance](https://intl.cloud.tencent.com/document/product/239/37712).
- The instance is in **Running** status.
- The instance maintenance time needs to be adjusted.

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the target instance ID to enter the **Instance Details** page.
5. In the **Configuration** section on the **Instance Details** page, click **Modify** on the right of **Maintenance Time**.
![](https://qcloudimg.tencent-cloud.cn/raw/109773d5c9dc86c12f524ab92ea78cbb.png)
6. In the **Modify Maintenance Time** window, refer to the table below to set the maintenance time.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e69d9147793118417ed9ba5558f809c8.png"  style="zoom:80%;">
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Maintenance Start Time</td>
<td>Select the start time of the maintenance time in the drop-down list.</td></tr>
<tr>
<td>Maintenance Duration</td>
<td>Select the desired duration of the maintenance time in the drop-down list, which can be 30 minutes, 1 hour, 1.5 hours, 2 hours, or 3 hours.</td></tr>
<tr>
<td>Maintenance Time</td>
<td>The new maintenance time is displayed, which is 03:00–04:00 AM by default.</td></tr>
</tbody></table>   
7. Click **OK**.

## Related APIs

| API | Description |
| ------------------------------------------------------------ | ---------------------- |
| [DescribeMaintenanceWindow](https://intl.cloud.tencent.com/document/product/239/37833) | Queries instance maintenance time |
| [ModifyMaintenanceWindow](https://intl.cloud.tencent.com/document/product/239/37832) | Modifies instance maintenance time |

