## Scenarios

Tencent Cloud TKE provides a version upgrade feature for Kubernetes. You can use this feature to upgrade a running Kubernetes cluster. The upgrade process includes pre-upgrade checking, upgrading the master, and upgrading the nodes.



## Upgrade Notice<span ID="UpgradeNotice"></sapn>
- **Upgrades are irreversible. Perform this operation with caution.**
- Currently the cluster upgrade feature is in beta. To apply to use it, [submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1).
- Before upgrading the cluster, check whether the cluster status is healthy. If the cluster status is abnormal, you can repair it yourself or [submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to contact us.
- When upgrading a cluster, you must first upgrade the master version, and then complete the node version upgrade as quickly as possible. During the upgrade process, it is not recommended to perform any operation in the cluster.
- Only the upgrade of the closest Kubernetes version offered by TKE is supported. Upgrading across multiple versions (such as upgrading from 1.8 to 1.12, skipping 1.10) is not supported. You can upgrade to the next version only if the master and node versions are consistent.

## Directions

Upgrading a cluster is divided into two steps: upgrading the Kubernetes version of the master, and upgrading the Kubernetes version of the nodes. The specific information is shown in the following figure:
![](https://main.qcloudimg.com/raw/1b4a4b4e25c9d9a66eb4f0c6d609bf49.png)

### Upgrading the Kubernetes master version
**Currently, master version upgrade is only supported for managed clusters**, and the upgrade takes 5-10 minutes, during which you will be unable to operate your cluster.


#### Considerations
- **Before upgrading, read the [Upgrade Notice](#UpgradeNotice).**
- For 1.7.8 version TKE clusters, the network mode is bridge. The cluster upgrade does not automatically switch the network mode to cni.
- Upgrading the cluster does not switch kube-dns to core-dns.
- After the cluster’s master version is upgraded to 1.10 and 1.12, some features configured when creating a cluster, such as support for ipvs, will become unavailable.
- For the existing cluster upgrade, if the master version is 1.10 and above, and the Node version is 1.8 and below, the PVC feature is unavailable.


#### Upgrading the Kubernetes master version

1. Log in to the TKE Console, and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar to go to the **Cluster Management** page.
2. Select the ID of the cluster whose Kubernetes master version is to be upgraded to go to the cluster’s **Deployment** page.
3. Select **Basic Information** in the left sidebar to go to the cluster’s **Basic Information** page.
4. In the cluster information module on the cluster’s **Basic Information** page, click **Upgrade** to the right of the master’s version. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/3ba70cdb57fa729d647e3fb2a3aa4a73.png)
5. In the pop-up window, click **OK** and wait until the upgrade is complete.
Before the sample cluster’s Kubernetes version is upgraded, the master version is 1.10.5. After the upgrade, the master version is 1.12.4. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/099ce1d116ac2ecdb995680b154fd23f.png)


### Upgrading the node Kubernetes version

After the cluster’s Kubernetes master version is upgraded, the cluster list page will show that an upgrade is available for the cluster node. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/05d3f2b65d31d309ad16c33970186dcd.png)
You can upgrade through the following steps:


#### Considerations
 - **Before upgrading, read the [Upgrade Notice](#UpgradeNotice).**
 - You can perform the upgrade operation when the Node is running.

#### Selecting an upgrade method
Two upgrade methods are supported for upgrading the Kubernetes version of a node: **reinstall and rolling upgrade** and **in-place rolling upgrade**. You can select one according to your requirements:
- **Reinstall and rolling upgrade**: reinstall the node to upgrade the node version. This method supports major and minor version upgrades, such as upgrades from version 1.10 to version 1.12, or from version 1.14.3 to version 1.14.8.
- **In-place rolling upgrade**: in-place, without re-installation. This only replaces components such as Kubelet and kube-proxy. Currently, this method is only supported for minor version upgrades, such as from version 1.14.3 to version 1.14.8.




#### Reinstall and rolling upgrade
Rolling upgrade based on the reinstalled node. Only one node is upgraded at a time, and the upgrading of the next node does not start until the upgrading of the current node is successful. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/9a2b7caa360e40aa8a1b919c7917217a.png)
The steps are described as follows:
1. **Pre-upgrade checking**: check the Pods on a node before draining them. The specific items for pre-upgrade checking are as follows:
   - Tabulate the number of pods of all workloads in this node. If the pod number of any workload changes to 0 after the node is drained, then the check fails, and the upgrade cannot be performed.
   - The following system control plane workloads will be ignored:
		- l7-lb-controller
		- cbs-provisioner
		- hpa-metrics-server
		- service-controller
		- cluster-autoscaler
- **Draining Pods**: first mark the node as unschedulable. Then, drain or delete all Pods from the node.
- **Removing nodes**: remove the node from the cluster. This step only performs basic cleanup, and will not delete the node instance of the node in the cluster. Therefore, the node’s attributes such as label and taint are retained.
- **Reinstalling**: reinstall the node’s operating system and reinstall the new version of kubelet.
- **Post-upgrade checking**: check if the node is ready and schedulable.




#### Reinstall and rolling upgrade Kubernetes version on a node
1. Log in to the TKE Console, and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar to go to the **Cluster Management** page.
2. Select the ID of the cluster whose Kubernetes node is to be upgraded to go to the cluster’s **Deployment** page.
3. In the left sidebar, select **Basic Information** and click **Upgrade** on the right of the node Kubernetes version. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/68c53549dd487d18b202c9dfd09e5aa0.png)
4. In the **Notes on Upgrade** step, select **Reinstall and rolling upgrade** as the upgrade method. Read the notice carefully, and place a check mark next to **I have read and agree to the terms above**, then click **Next**. This is shown in the following figure.
>This upgrade method will reinstall the system, and the original data will be cleared. Note that you should back up the data in advance.
>
![](https://main.qcloudimg.com/raw/5edfaedfbb569d3d339adc80bd6d774c.png)
6. In the **Select nodes** step, select the nodes that need to be upgraded in this batch, and click **Next**.
6. In the **Upgrade Settings** step, enter the node information as required, and click **Next**.
7. In the **Confirmation** step, confirm the information and click **Finish** to start the upgrade.
8. View the progress of the node upgrade until all the nodes are upgraded.


#### In-place rolling upgrade
Node in-place upgrade uses the rolling upgrade method, meaning that it will only upgrade one node at a time, with the next node not being upgraded until the current node upgrade is successful. in-place upgrade currently only supports upgrading to different minor versions of the same major version. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/9bfc2ff8fb0af26ba30214a715fe633d.png)
The steps are described as follows:
1. **Component updating**: replace and restart the kubelet and kube-proxy components on the node. The parameters will be initialized to the default values.
- **Post-upgrade checking**: check if the node is ready and schedulable.



#### In-place rolling upgrade of the Kubernetes version on a node
1. Log in to the TKE Console, and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** on the left sidebar to go to the **Cluster Management** page.
2. Select the ID of the cluster whose Kubernetes node is to be upgraded to go to the cluster’s **Deployment** page.
3. In the left sidebar, select **Basic Information** and click **Upgrade** on the right of the node Kubernetes version. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/68c53549dd487d18b202c9dfd09e5aa0.png)
4. In the **Notes on Upgrade** step, select **In-place rolling upgrade** as the upgrade method. Read the notice carefully, and place a check mark next to **I have read and agree to the terms above**, then click **Next**. This is shown in the following figure.
![](https://main.qcloudimg.com/raw/118172ac03f18b7001ad0eb83d4ea7ba.png)
5. In the **Select nodes** step, select the nodes that need to be upgraded in this batch, and click **Next**.
6. In the **Confirmation** step, confirm the information and click **Finish** to start the upgrade.
7. View the progress of the node upgrade until all the nodes are upgraded.



