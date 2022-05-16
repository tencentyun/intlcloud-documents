<dx-alert infotype="alarm" title="Note">
Tencent Prometheus Service (TPS) has been integrated into [TMP](https://intl.cloud.tencent.com/document/product/457/46734), which supports cross-region monitoring in multiple VPCs, and provides a unified Grafana dashboard, allowing for checking of multiple monitoring instances. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS will be discontinued on May 16, 2022,see [Announcements](https://intl.cloud.tencent.com/document/product/457/46999). Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out TMP. TPS instances can no longer be created, but you can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency; otherwise, higher costs may be incurred.
</dx-alert>

## Overview

This document describes how to query the alarm history in cloud native monitoring.

## Prerequisites

Before querying alarm history, you need to perform the following operations:
- You've [created a TMP instance](https://intl.cloud.tencent.com/document/product/457/46739).
- The cluster to be monitored has been associated with the corresponding instance as instructed in [Associating with Cluster](https://intl.cloud.tencent.com/document/product/457/38825).
- The information that needs to be collected has been added to the [data collection configuration](https://intl.cloud.tencent.com/document/product/457/38826) of the cluster.
- Alarm policies are configured. Refer to [Configuring Alarm Policy](https://intl.cloud.tencent.com/document/product/457/38828).

## Directions


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** in the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Alarm history** page, select a time range to query the alarm history.
![](https://qcloudimg.tencent-cloud.cn/raw/1c00ed84dd12db38b5d7b23b8a0c9d72.png)
