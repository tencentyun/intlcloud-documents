This document describes how to create a read-only instance in the TDSQL-C for MySQL console.

## Overview
TDSQL-C for MySQL allows you to create one or more read-only instances in a cluster, which are suitable for read/write separation and one-write-multiple-read application scenarios and can greatly enhance the read load capacity of your database cluster.

- A TDSQL-C for MySQL cluster supports two instance types: source instance (read-write instance) and replica instance (read-only instance).
- A TDSQL-C for MySQL cluster provides private read-write and read-only addresses by default. You can access all read-only instances at the cluster's private read-only address. After a read-only instance is created, access requests to it at the private read-write address will be automatically forwarded to it.
- A read-only instance is billed in the same way as the read-write instance. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/1098/48406).

>?For more information on how to access TDSQL-C for MySQL, see [Connecting to Cluster](https://www.tencentcloud.com/document/product/1098/40627).

## Notes
- Read-only and read-write instances share the same storage, so there is no need to maintain the account and database.
- A read-only instance does not need to replicate or migrate data, nor does it need to be synced with a read-write instance through binlog. It can be created in seconds.
- The delay between a read-only instance and the read-write instance is usually within milliseconds, which can be viewed through the read-only instance delay monitoring metric on the monitoring and alarms page.
- Read-only and read-write instances can have different specifications. However, to make it easier for you to adjust the configuration based on the load, we recommend you keep the specifications of read-only instances the same.
- When you add a monthly subscribed read-only instance to a monthly subscribed cluster, the instance will expire at the same time as the cluster.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a **cluster ID/name** in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
2. On the cluster management page, select the **Instance List** tab and click **Read-Only Instance** > **Add Read-Only Instance** to enter the read-only instance purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/540717d685ce3e607dce567cacd17723.png)
3. On the purchase page, select the target read-only instance configuration, confirm that everything is correct, and click **Buy Now**. Then, you can view the new instance in the instance list.
