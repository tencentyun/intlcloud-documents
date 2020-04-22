## Operation Scenarios
This document describes how to add a component that is not installed in the cluster in the EMR Console.
>Please manage the components through **Component Management**. Component changes made directly to a server (such as adding a component) will not be synced to the console and thus cannot be further managed.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and click **Component Management** on the left sidebar. Then, you can perform operations such as **Add Component**, **Rolling Restart**, and **Reset Native UI Password**. In the **Operation** column of a component, click **Configure** to perform operations on it such as adding or modifying parameters and rolling back at the cluster or server level. Click **Manage Role** to enter the service/node-level management page of the component. The following uses **Add Component** as an example to describe how to add a component that is not installed in the cluster.
![](https://main.qcloudimg.com/raw/2d6506556a7fda83246ed89e94fcb9b4.png)
2. On the component management page, click **Add Component**.
3. If there is no metadatabase in the cluster and Hive, Sqoop, Hue, Ranger, Oozie, and Presto are to be installed, you need to purchase a TencentDB instance as the metadata store. There are two storage methods for Hive metadata: you can store the metadata in the default MetaDB instance of the cluster or associate the metadata with EMR-MetaDB or a self-built MySQL database. In the latter case, metadata will be stored in an associated database and will not be terminated when the cluster is terminated.
![](https://main.qcloudimg.com/raw/306312805518e274a5b90e4967887870.png)
4. The selection for MetaDB purchase and Hive metadatabase is the same as when you purchase a new cluster.
5. After selecting the desired item, click **OK**.
