## Overview
HDFS federation management is an HDFS federated cluster deployment and management feature, including NameService management and mount table management. Federation management is supported for Hadoop-type clusters in HA mode. There are two federation types to choose from: ViewFs federation and router-based federation, and the federation type cannot be changed once selected. A router node will be used to deploy an added NameNode. This router node does not support termination and role start/stop at the node level.

>!
1. The HDFS federation management feature is currently made available through an allowlist. To use it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
2. All EMR versions support ViewFs federation. As only HDFS v2.9.0 and later support router-based federation, only EMR v3.x.x and later support router-based federation.
3. Suspending the NameNode role process on a federated node on the **Role Management** page may affect the cluster scaling, so you need to resume the process first before scaling the cluster.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to go to the cluster details page.
2. On the cluster details page, click **Cluster Service** and select **Operation** > **Federation Management** in the top-right corner of the HDFS component block to enter the **Federation Management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/263196087adfe138be527a248a4d2865.png)
3. Click **Add NameService** to create an HDFS federation. You need to enter the NameService name and select the federation type, NameNode, and DFSRouter (for router-based federation only).
![](https://qcloudimg.tencent-cloud.cn/raw/ed979d340d4279e06331d3475d095738.png)
4. Select **Add Federated Node**.
Federated nodes adopt router nodes in the cluster. Therefore, you need to add a router node on the **Resource Management** page first and then set it to a federated node. The NameNode process requires two nodes, on each of which the NameNode and ZKFC processes will be deployed.
When creating a router-based federation for the first time, you need to select at least two nodes to deploy the DFSRouter process. When creating another federation, you can reuse the DFSRouter nodes, and the number of the nodes can be greater than or equal to zero.
![](https://qcloudimg.tencent-cloud.cn/raw/7da7aa786e0471e2a2b826bec3fae555.png)
>!
>- For HDFS versions earlier than 3.3.0, when you successfully add a NameService to a router-based federation (**not for the first time** ), you need to restart the old DFSRouter process on the **Role Management** page (preferably during off-peak hours). For HDFS v3.3.0 and later which support hot loading the configuration, this operation is not required.
>- After adding a federated NameService to a cluster with Kerberos enabled, you need to restart the YARN ResourceManager first (preferably during off-peak hours) before you can use the files on the new NameService for jobs submitted to YARN.
>- The NameService name cannot be modified or deleted once set and cannot be system keywords such as "nsfed", "haclusterX", and "ClusterX".
5. Add a mount table.
You can add a mount table only after successfully adding a NameService. To reduce the configuration complexity, we recommend you map only first-level directories such as "/tmp", "/user", and "/srv" to NameServices. You can add multiple mount paths at a time.
	- Path: Path name of the unified ViewFs or router-based federation namespace, also known as the mount point.
	- Target NameService: The NameService corresponding to the real path to which the mount point maps.
	- Target path: The real path on the corresponding NameService, whose name can be different from that of the global path.
![](https://qcloudimg.tencent-cloud.cn/raw/3b01cab48683ab4c6ffb9535ebc01d0e.png)

>!
>- Path direction:
	1. Log in to the NameNode and run `hdfs dfs -ls /` to point to the path under the namespace managed by the NameNode. For ViewFs federation, you need to use `hdfs dfs -ls ViewFs://ClusterX/` to point to the global path; for router-based federation, use `hdfs dfs -ls hdfs://nsfed/` instead.
	2. Log in to another node, such as the router node serving as a client. `hdfs dfs -ls /` points to the global path.
>-	The data of all business components needs to be placed in first-level directories but not the root directory for access, as the root directory cannot be mounted.
>-	The default NameService has the `/emr` directory, which needs to be mounted.

