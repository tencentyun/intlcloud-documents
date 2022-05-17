## Overview
Instance information records the basic information of your EMR cluster. You can view the basic configuration, software information, and hardware information of the cluster on the **Instance Information** page.
- The **Basic Configuration** section displays basic information of the cluster, such as network information, creation time, security group, high-availability switch status, master public IP, billing mode, host login method, automatic service role definition switch status, and COS switch status.
- The **Software Info** section displays the cluster type, use case, product version, deployed component, MetaDB, Hive metadatabase, and Kerberos mode switch status.
- The **Hardware Configuration** section displays the quantity of nodes in each type.

This document describes how to view the cluster instance information in the console.

## Directions
1. After successfully creating a cluster, log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the cluster.
2. If COS is not enabled for the cluster, click **Authorize**.
![](https://qcloudimg.tencent-cloud.cn/raw/b14801d2228963d13147ad1619da1975.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3e338981d8b141c2ebeb12b0cb96b7a8.png)

If you need refined authorization, you can set a custom service role for accessing Tencent Cloud resources during the execution of big data jobs. You should select **Tencent Cloud product service** as the service role type and **Elastic MapReduce** as the service supporting the role.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f96921b986ee11385bf0bbc417bc1f2c.png" style="zoom: 67%;" />
To change the host login password or method of cluster nodes after scale-out, click **Change**.
![](https://qcloudimg.tencent-cloud.cn/raw/e3c2b470688a91e9ace010a1893be5bd.png)

>? 
>- The login method set for initializing nodes in an EMR cluster. After the cluster is created, modification of the setting here applies only to new nodes.
>- You can go to the CVM console to change host passwords/keys of existing nodes of the cluster. Before change, see **Shutting Down Instances** to understand the potential shutdown risks.
