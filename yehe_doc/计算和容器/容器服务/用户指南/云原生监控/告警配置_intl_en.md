<dx-alert infotype="alarm" title="Note">
Tencent Prometheus Service (TPS) has been integrated into [TMP](https://intl.cloud.tencent.com/document/product/457/46734), which supports cross-region monitoring in multiple VPCs, and provides a unified Grafana dashboard, allowing for checking of multiple monitoring instances. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS will be discontinued on May 16, 2022,see [Announcements](https://intl.cloud.tencent.com/document/product/457/46999). Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out TMP. TPS instances can no longer be created, but you can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency; otherwise, higher costs may be incurred.
</dx-alert>

## Overview
This document describes how to configure alarm policies in cloud native monitoring.  

## Prerequisites

Before configuring alarm policies, you need to perform the following operations:
- You've [created a TMP instance](https://intl.cloud.tencent.com/document/product/457/46739).
- The cluster to be monitored has been associated with the corresponding instance as instructed in [Associating with Cluster](https://intl.cloud.tencent.com/document/product/457/38825).
- The information that needs to be collected has been added to the [data collection configuration](https://intl.cloud.tencent.com/document/product/457/38826) of the cluster.

## Directions

### Configuring alarm policies

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** in the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Alarm configurations** page, click **Create alarm policy**.
![](https://qcloudimg.tencent-cloud.cn/raw/55759e722ebf326889966a12f70a3e45.png)
4. On the **Create alarm policy** page, add the details of the alarm policy.
![](https://qcloudimg.tencent-cloud.cn/raw/5f053d31a0b7b60cd1154cac4297ba77.png)
 - **Rule name**: Name of alarm rule (up to 40 characters).
 - **PromQL**: Alarm rule statement.
 - **Duration**: When the condition described in the above statement reaches the duration specified here, an alarm will be triggered.
 - **Label**: Prometheus labels of each rule.
 - **Alarm content**: The alarm notifications to be sent to recipients through email and SMS when an alarm is triggered.
 - **Convergence time**: In this specified period, if the alarm condition is met multiple times, only one notification is sent.
 - **Effective time**: Alarm notifications can only be sent during the effective period.
 - **Recipient group**: Notifications will be sent to the specified contact group.
 - **Delivery method**: The delivery channel of alarm notifications.
6. Click **Complete**.
>! The alarm policy will take effect by default once created.

### Pausing alarming
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** in the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Alarm configurations** page, click **More** > **Pause alarming** on the right side of the instance.
![](https://qcloudimg.tencent-cloud.cn/raw/dd258e9e0694384fd12d01dda89b1fb2.png)
4. In the **Disable alarm policy** pop-up window, click **OK**.

