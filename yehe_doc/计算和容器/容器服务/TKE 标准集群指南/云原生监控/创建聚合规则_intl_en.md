<dx-alert infotype="alarm" title="Note">
To provide better and more powerful product capabilities, TPS will be merged and upgraded into [Tencent Managed Service for Prometheus (TMP)](https://intl.cloud.tencent.com/document/product/457/46734). The new TMP service supports cross-region and cross-VPC monitoring and connecting a unified Grafana dashboard to multiple TMP instances for data display in one place. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS will be deactivated soon. Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out the recently launched TMP service. TPS no longer supports instance creation, and you can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency; otherwise, higher costs may be incurred.
</dx-alert>

## Overview

This document describes how to configure aggregation rules to improve query efficiency when dealing with complex query scenarios.

## Prerequisites

Before configuring aggregation rules, you need to perform the following operations:
- You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2) and created a self-deployed cluster.
- You have [created a TMP instance](https://intl.cloud.tencent.com/document/product/457/46739) in the VPC of the cluster.

## Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** on the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Aggregation Rule** page, click **Create Aggregation Rule** .
4. In the **Add Aggregation Rule** pop-up window, edit the aggregation rule as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/07bf41b601845cb1ea9705a6ae16c881.png)
6. Click **OK**.
