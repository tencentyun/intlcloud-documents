




## Overview

You can easily create a TMP instance and associate it with a cluster in the current region. Clusters associated with the same TMP instance share the same monitoring metrics and alarming policies. Currently, TMP supports managed clusters, self-deployed clusters, elastic clusters and edge clusters. This document describes how to create and manage TMP instances in the TKE console.

## Directions

### Service authorization

When using TMP for the first time, you need to assign the `TKE_QCSLinkedRoleInPrometheusService` role to the service, which is used to authorize the TMP to access the COS bucket.
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **TMP** in the left sidebar to pop up the **Service authorization** window.
2. Click **Go to Cloud Access Management** to enter the **Role management** page.
3. Click **Grant** to complete authentication.
![](https://qcloudimg.tencent-cloud.cn/raw/6bc3c7651a63bc372df274f689b3f2c2.png)


### Creating TMP instance
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **TMP** in the left sidebar.
2. Click **Create** at the top of the instance list page.
3. You will be redirected to the **Tencent Managed Service for Prometheus** page.
4. Purchase an instance as needed. For parameter details, see [Creating Instance](https://intl.cloud.tencent.com/document/product/1116/43170).
5. Click **Complete**. Now you can click **Associate with TKE** to see the list of TMP instances.
6. You can check the instance creation progress on the page. If the instance status changes to "Running", the instance was successfully created and is running properly.
    ![](https://qcloudimg.tencent-cloud.cn/raw/1c8be13e3a0bccc74671e87301ea7b26.png)
>? If it takes too long to create an instance or the displayed status is abnormal, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).



### Deleting TMP instance
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **TMP** in the left sidebar.
2. On the instance list page, click **Terminate/Return** on the right of the instance to be deleted.
3. In the **Terminate/Return** pop-up window, click **OK** to delete the current instance.
>? When the instance is deleted, the monitoring components installed in the cluster as well as the EKS cluster and CLB instance associated with the instance will be deleted at the same time by default.

