## Feature Description
This document describes how to add components in the EMR console.
>!
>- You need to manage the components through **Cluster Service**. Component changes made directly by logging in to a node (such as adding a component) will not be synced to the console and thus cannot be further managed.
>- Components on a different EMR version or component version cannot be added. Instead, you can only add components on the current EMR version.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Service** > **Add Component** to add a component not installed in the cluster.
![](https://main.qcloudimg.com/raw/da6721fc6fe82ce629177aebdbe299e6.png)
3. If there is no metadatabase in the cluster and Hue, Ranger, Oozie, Druid, and Superset components are to be installed, you need to purchase a TencentDB instance as the metadata store. You cannot add the Kudu component to a non-HA cluster.
4. There are two storage options for Hive metadata: you can store the metadata in the MetaDB (default option) or associate the metadata with EMR-MetaDB or a self-built MySQL database. In the latter case, metadata will be stored in the associated database and will not be deleted when the cluster is terminated.
![](https://main.qcloudimg.com/raw/150f0d9e0cb8edb28d38d2c1e0db6702.png)
5. The selection for MetaDB purchase and Hive metadatabase is the same as when you purchase a new cluster.
6. After selecting the component, click **OK**.
