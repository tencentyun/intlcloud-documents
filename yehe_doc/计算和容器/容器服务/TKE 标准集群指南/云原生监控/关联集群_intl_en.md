

## Overview

This document describes how to associate clusters with TPS instances in the cloud native monitoring. When the association is established, you can edit configurations such as data collection rules. Currently, cloud native monitoring only supports the association of the TPS instance and the TKE self-deployed cluster, managed cluster, and elastic cluster under the same VPC to which the instance belongs.

## Prerequisites
- You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2) and created a self-deployed cluster.
- You have [created a TPS instance](https://intl.cloud.tencent.com/document/product/457/38824) in the VPC of the cluster.

## Directions

### Associating with cluster
>! After the cluster is successfully associated, the monitoring data collection add-on will be installed in the cluster, which will be deleted when the cluster is disassociated.
>
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** on the left sidebar.
2. On the instance list page, select an instance name that needs to associate with the cluster to go to its details page.
3. On **Associate with Cluster** page, click **Associate with Cluster** as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/81e9d2c0fc87d301871b1a9065fb9cb6.png)
4. In the pop up **Associate with Cluster** window, select the cluster to associate with under the current VPC, as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/26fafe0e7e21e259614036623ee2338a.png)
5. Click **OK**.





### Canceling association

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** on the left sidebar.
2. On the instance list page, select an instance name that needs to cancel association to go to its details page.
3. On **Associate with Cluster** page, click **Cancel association** on the right side of the instance as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4b53316a8d1c885f7a21e1afeb40dc7d.png)
4. Click **OK** in the pop up **Disassociate cluster** window.



