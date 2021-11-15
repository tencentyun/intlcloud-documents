This document describes how to create a read-only instance in the TDSQL-C console.

## Overview
TDSQL-C allows you to create one or more read-only instances in a cluster, which are suitable for read/write separation and one-write-multiple-read application scenarios and capable of greatly enhancing the read load capacity of your database cluster.

- A TDSQL-C cluster supports two instance types: primary instance (read-write instance) and secondary instance (read-only instance).
- A TDSQL-C cluster provides read-write and read-only addresses by default. You can access all read-only instances at the cluster's read-only address. After a read-only instance is created, new read-only connection requests to the read-only address will be automatically forwarded to the read-only instance.
- A read-only instance is billed in the same way as the read-write instance. For more information, please see [Pricing](https://intl.cloud.tencent.com/document/product/1098/40620).
- Unified read/write separation addresses (i.e., read and write requests are separated automatically) are not supported currently.

>?For more information on how to access a TDSQL-C cluster, please see [Connecting to TDSQL-C Cluster](https://intl.cloud.tencent.com/document/product/1098/40627).

## Notes
- Read-only and read-write instances share the same storage, so there is no need to maintain the account and database.
- A read-only instance does not need to be synced with the read-write instance through binlog or does not need to replicate/migrate data. It can be created in seconds.
- The delay between a read-only instance and the read-write instance is usually within milliseconds, which can be viewed through the read-only instance delay monitoring metric on the instance monitoring page.
- The specification of a read-only instance can be different from that of the read-write instance, which makes it easier for you to adjust the configuration according to the load. We recommend you keep the specifications of read-only instances the same.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster name or **Manage** in the **Operation** column in the cluster list to enter the cluster details page.
2. In the instance list, click **Create** to enter the read-only instance purchase page.
![](https://main.qcloudimg.com/raw/291d1199489672e349d23aece404ecf9.png)
3. Select the desired read-only instance configuration on the purchase page. After confirming that everything is correct, click **Buy Now**.

