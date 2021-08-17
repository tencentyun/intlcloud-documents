This document describes how to modify the computing specification and storage capacity of a TencentDB for PostgreSQL instance.

## Overview
When the current performance or storage capacity of an instance cannot meet the needs of business changes, the instance configuration can be adjusted to sustain the business growth.

>!Currently, instance configuration can be upgraded but not downgraded.

## Directions
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres), select the target instance in the instance list, and click **Adjust Configurations** in the **Operation** column.
2. In the pop-up window, select the instance configuration and storage capacity you want to adjust to. The specific configuration adjustment price will be displayed below. After confirming the price, click **Submit**.
>?
>- As the instance configuration adjustment involves instance data migration, the adjustment process will be completed with a primary/secondary switch, which will cause an instantaneous disconnection and slightly affect business access to the database instance. Therefore, we recommend you set the switch time within off-peak hours.
>- If you need to control the switch time, please select **Specify Time** in **Switch Time**. Then, you can select a time range. After the instance data is migrated, the system will automatically check whether it is within the switch time range, and if not, the instance will enter the **Waiting for Switch** status until the time falls in the time range and then complete the switch.
>- The time range is calculated at the granularity of one day. If the time window on the current day is missed, switch will be performed in the time window on the next day.
>- When the instance is in the **Waiting for Switch** status, you can click **Switch Now** in the instance list to switch immediately.
>
![](https://main.qcloudimg.com/raw/f1eb34eb4857723873f6fd1d4ca002c0.png)
