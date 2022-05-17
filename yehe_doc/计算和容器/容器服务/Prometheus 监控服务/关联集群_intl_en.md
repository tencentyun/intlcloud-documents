

## Overview

This document describes how to associate clusters with TMP instances. When the association is established, you can edit configurations such as data collection rules. Currently, the service supports cross-VPC associations, allowing you to monitor clusters in multiple VPCs in different regions within the same TMP instance.

## Prerequisites
- You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2) and created a cluster.
- You have created a [TMP instance](https://intl.cloud.tencent.com/document/product/457/46739).

## Directions

### Associating with cluster
>! After the cluster is successfully associated, the monitoring data collection add-on will be installed in the cluster, which will be deleted when the cluster is disassociated.
>
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **TMP** in the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Cluster monitoring** page, click **Associate with Cluster**.   
![](https://qcloudimg.tencent-cloud.cn/raw/14e095f64ec2eef9da766de22b6bef09.png)
4. In the **Associate with cluster** pop-up window, select the target cluster.
    ![](https://qcloudimg.tencent-cloud.cn/raw/cc7e64c6569e1021a634e63c77ff3401.png)
  - **Cluster type**: TKE general clusters, elastic clusters, edge clusters, and registered clusters are supported.
  - **Cross-VPC association**: When it is enabled, you can monitor clusters in multiple VPCs in different regions within the same TMP instance.
        - Public CLB: You don't need to create a public CLB instance if your monitoring instance's VPC is connected to the VPC of the cluster you want to associate with; if not, you must select **Create public CLB**, otherwise, you cannot collect cluster data across VPCs. For example, if your instance VPC is already connected to the cluster VPC through [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), you don't need to create a public CLB instance.
  3. **Region**: Select the region where the cluster resides.
  4. **Cluster**: Select one or multiple clusters to be associated with.
  5. **Global tag**: It is used to tag each monitoring metric with the same key-value pair.
5. Click **OK**.





### Canceling association

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **TMP** in the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Associate with cluster** page, click **Cancel association** on the right side of the instance.
![](https://qcloudimg.tencent-cloud.cn/raw/7e3c09fbf4251176fb0d38247801be70.png)
4. Click **OK** in the **Disassociate cluster** pop-up window.



