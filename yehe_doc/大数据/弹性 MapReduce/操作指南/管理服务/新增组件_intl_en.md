## Feature Overview
This document describes how to add components in the EMR Console.
>
- Please manage the components through **Cluster Service**. Component changes made directly to a server (such as adding a component) will not be synced to the console and thus cannot be further managed.
- Components on a different EMR version or component version cannot be added. Instead, you can only add components on the current EMR version.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster List**, and click the ID/Name of the target cluster to enter the cluster details page.
2. On the cluster details page, select **Cluster Service** > **Add Component** to add a component not installed in the cluster.
![](https://main.qcloudimg.com/raw/da6721fc6fe82ce629177aebdbe299e6.png)
3. If there is no metadatabase in the cluster and Hive, Sqoop, Hue, Ranger, Oozie, and Presto are to be installed, you need to purchase a TencentDB instance as the metadata store. There are two storage methods for Hive metadata: you can store the metadata in the default MetaDB instance of the cluster or associate the metadata with EMR-MetaDB or a self-built MySQL database. In the latter case, metadata will be stored in an associated database and will not be terminated when the cluster is terminated.
![](https://main.qcloudimg.com/raw/150f0d9e0cb8edb28d38d2c1e0db6702.png)
4. The selection for MetaDB purchase and Hive metadatabase is the same as when you purchase a new cluster.
5. After selecting the component, click **OK**.
