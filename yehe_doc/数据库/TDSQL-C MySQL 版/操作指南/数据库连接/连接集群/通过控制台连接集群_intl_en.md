Database Management Center (DMC) is a one-stop Tencent Cloud database management tool. Services supported include database/table-level operations, real-time monitoring, instance session management, SQL window, and data management.

This document describes how to connect to a TDSQL-C for MySQL cluster in DMC.

## Prerequisites
You have created a database cluster account as instructed in [Creating Account](https://www.tencentcloud.com/document/product/1098/44612).

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click **Log In** in its **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/uCQM939_26.png)
3. In the login window, enter the created database account and password and click **Log In**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/hx7Z039_27.png)
 - **Type**: Select **TDSQL-C for MySQL**.
 - **Region**: Select the region of the cluster.
 - **Instance**: Select the cluster to be connected to, or search for the cluster by ID in the drop-down list.
 - **Account**: Enter the account name corresponding to the cluster.
 - **Password**: Enter the password corresponding to the account.
 >?The cluster ID can be obtained in the **Cluster List** or on the **Cluster Details** page in the TDSQL-C for MySQL console.
4. The UI after successful login is as follows:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Fsyj840_28.png)

## Other ways to connect to a cluster
- [Connecting to Cluster at Private or Public Network Address from Linux CVM Instance](https://www.tencentcloud.com/document/product/1098/52628)
- [Connecting to Cluster at Private or Public Network Address from Windows CVM Instance](https://www.tencentcloud.com/document/product/1098/52629)
