
## Overview
This document describes how to configure alarm policies in cloud native monitoring.

## Prerequisites

Before configuring alarm policies, you need to perform the following operations:
- You've created a TPS instance as instructed in [Creating TPS Instance](https://intl.cloud.tencent.com/document/product/457/38824).
- The cluster to be monitored has been associated with the corresponding instance. For more information, see [Associating with cluster](https://intl.cloud.tencent.com/document/product/457/38825).
- The information that needs to be collected has been added to the [data collection configuration](https://intl.cloud.tencent.com/document/product/457/38826) of the cluster.

## Directions

### Configuring alarm policies

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** on the left sidebar.
2. On the instance list page, select an instance name that needs to configure alarm policies to go to its details page.
3. On **Alarm Configurations** page, click **Create Alarm Policy** as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/55759e722ebf326889966a12f70a3e45.png)
4. On **Create Alarm Policy** window, add the details of the alarm policy as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/5f053d31a0b7b60cd1154cac4297ba77.png)
 - **Rule Name**: name of alarm policy (up to 40 characters)
 - **PromQL**: alarm policy statement
 - **Duration**: when the condition described in the above statement reaches the duration specified here, an alarm will be triggered.
 - **Label**: Prometheus labels of each rule
 - **Alarm Content**: the alarm notifications to be sent to recipients through email and SMS when an alarm rule is triggered.
 - **Convergence Time**: in this specified period, if the alarm condition is met multiple times, only one notification is sent.
 - **Effective Time**: alarm notifications can only be sent during the effective period.
 - **Recipient Group**: notifications will be sent to the specified contact group.
 - **Delivery Method**: the delivery channel of alarm notifications.
6. Click **Complete**.
>! The alarm policy will take effect by default once created.

### Pausing alarming
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** on the left sidebar.
2. On the instance list page, select an instance name that needs to pause alarming to go to its details page.
3. On **Alarm Configurations** page, click **More** > **Pause alarming** on the right side of the instance as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/dd258e9e0694384fd12d01dda89b1fb2.png)
4. In the pop up **Disable Alarm Policy** window, click **OK**.

