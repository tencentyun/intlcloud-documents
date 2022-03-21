This document describes how to select the primary and secondary AZs of a cluster on the cluster purchase page in the TDSQL-C for MySQL console.

## Overview
TDSQL-C for MySQL supports multi-AZ deployment in the same region, which has higher availability and better disaster recovery capability than single-AZ deployment.

TDSQL-C for MySQL clusters benefit from increased availability and durability when deployed in multi-AZ mode. When you provision a multi-AZ database cluster, TDSQL-C for MySQL will automatically create a primary database instance and synchronously replicate data to the secondary instance in another AZ. Each AZ runs on its own independent and physically distinct infrastructure designed for high reliability. In the event of an infrastructure failure, automatic failover to the secondary instance will be performed, so that you can resume database operations as soon as the failover is completed. As the endpoints of the database instances remain unchanged after failover, applications can resume database operations without manual intervention required.

## Directions
### Selecting AZs on purchase page when creating cluster
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click **Create** in the cluster list.
2. In the **Database Configuration** item on the purchase page, select the desired region, and available primary and secondary AZs will be displayed below, which you can select as needed.
3. After selecting the database configuration, click **Next** to enter the **Basic Information** and **Advanced Configuration** items.
![](https://qcloudimg.tencent-cloud.cn/raw/be5e6b089e344e1a0ea18c1daddb2eaa.png)
![](https://qcloudimg.tencent-cloud.cn/raw/8c6e378d12d62a3ab1c0c8a38718994f.png)
5. After completing the configuration and confirming that everything is correct, click **Buy Now**.
6. After the purchase is completed, you will be redirected to the cluster list. After the status of the newly created cluster becomes **Running**, you can go to the cluster list page or click the cluster ID to enter the **Cluster Details** page, where you can query the AZs in **Availability Info**.
![](https://qcloudimg.tencent-cloud.cn/raw/da17e5019faa7021a1b64cdda493019a.png)

### Modifying AZ information
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster name in the cluster list or **Manage** in the **Operation** column to enter the cluster details page.
2. In the **Availability Info** module on the cluster details page, click **Modify** after **Deployment Mode** to modify the AZ.
![](https://qcloudimg.tencent-cloud.cn/raw/b46495faa0c8c464fe9d1d5e14586800.png)
3. In the pop-up window, select the desired configuration and click **OK**.
>?Currently, only the secondary AZ can be modified, but not the primary AZ.
>
![](https://qcloudimg.tencent-cloud.cn/raw/ef7d1596674bf8617d2514208d682cc1.jpg)


