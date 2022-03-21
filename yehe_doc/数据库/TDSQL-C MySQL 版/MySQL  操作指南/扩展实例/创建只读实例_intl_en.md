This document describes how to create a read-only instance in the TDSQL-C console.

## Overview
TDSQL-C for MySQL allows you to create one or more read-only instances in a cluster, which are suitable for read/write separation and one-write-multiple-read application scenarios and capable of greatly enhancing the read load capacity of your database cluster.

- A TDSQL-C for MySQL cluster supports two instance types: primary instance (read-write instance) and secondary instance (read-only instance).
- A TDSQL-C for MySQL cluster provides read-write and read-only addresses by default. You can access all read-only instances at the cluster's read-only address. After a read-only instance is created, new read-only connection requests to the read-only address will be automatically forwarded to the read-only instance.
- A read-only instance is billed in the same way as the read-write instance. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1098/40620).
- Unified read/write separation addresses (i.e., read and write requests are separated automatically) are not supported currently.

>?For more information on how to access a TDSQL-C cluster, see [Connecting to TDSQL-C Cluster](https://intl.cloud.tencent.com/document/product/1098/40627).

## Notes
- Read-only and read-write instances share the same storage, so there is no need to maintain the account and database.
- A read-only instance does not need to be synced with the read-write instance through binlog or copy/migrate data. It can be created in seconds.
- The delay between a read-only instance and the read-write instance is usually within milliseconds, which can be viewed through the read-only instance delay monitoring metric on the instance monitoring page.
- The specification of a read-only instance can be different from that of the read-write instance, which makes it easier for you to adjust the configuration according to the load. We recommend you keep the specifications of read-only instances the same.
- When you add a monthly subscribed read-only instance in a monthly subscribed cluster, the instance will expire at the same time as the cluster.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
2. On the cluster management page, select the **Instance List** tab and click **Create** to enter the read-only instance purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/540717d685ce3e607dce567cacd17723.png)
3. On the purchase page, select the target read-only instance configuration, confirm that everything is correct, and click **Buy Now**.

