## Overview

Tencent Cloud TKE allows you to upgrade the Kubernetes version. You can use this feature to upgrade a running Kubernetes cluster. The upgrade process includes pre-upgrade checking, upgrading the Master, and upgrading the node.

<span ID="UpgradeNotice"></sapn>

## Upgrade Notice
- **The upgrading action is irreversible. Perform this operation with caution.**
- Before upgrading the cluster, check whether the cluster is healthy. If the cluster is abnormal, you can fix it yourself or [submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to contact us.
- When upgrading a cluster, you must first upgrade the Master, and then upgrade the node as quickly as possible. During the upgrade process, we recommend that you do not perform any operations in the cluster.
- Only upgrading to the next Kubernetes version offered by TKE is supported. Upgrading across multiple versions (such as upgrading from 1.8 to 1.12, skipping 1.10) is not supported. You can upgrade to the next version only if the Master and node versions are consistent.

## Directions

Upgrading a cluster involves two steps. The first step is to [upgrade the Master Kubernetes version](#Master) and the second is to [upgrade the node Kubernetes version](#Node). See below for details:
![](https://main.qcloudimg.com/raw/9a86b7ebd520700999af9b6e62fe5bd4.png)
<span id="Master"></span>
### Upgrading the Master Kubernetes version
>! **Currently, Master version upgrade is supported only for managed clusters**, and the upgrade takes 5-10 minutes, during which you are unable to operate your cluster.


#### Considerations
- **Before upgrading, read the [Upgrade Notice](#UpgradeNotice).**
- For TKE clusters of the v1.7.8, the network mode is bridge. Upgrading the cluster does not automatically switch the network mode to cni.
- Upgrading the cluster does not switch kube-dns to core-dns.
- When you upgrade a cluster to v1.10 and 1.12, some features configured when the cluster is created, such as support for ipvs, will become unavailable.
- After the upgrade of an existing cluster, if the master version is 1.10 or later, and the node version is V1.8 or earlier, the PVC feature will be unavailable.
- For major version upgrades (for example, from 1.12 to 1.14), the original custom parameters will not be retained, you need to reconfigure them for the new version. For more information, see [Custom Kubernetes component launch parameters](https://intl.cloud.tencent.com/document/product/457/38139).
- Before upgrading the Kubernetes version, refer to the TKE Kubernetes major version update notes.
- After upgrading the master version, we recommend that you upgrade the node version as soon as possible.

#### Directions
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, select the ID of the desired cluster, and enter the cluster details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the cluster information module on the cluster’s **Basic Information** page, click **Upgrade** to the right of the Master version, as shown in the figure below:
![](https://main.qcloudimg.com/raw/65eb801aaeefc2d499f5451eac1bccc8.png)
5. In the pop-up window, click **Submit** and wait until the upgrade is complete.
In this example, the original master version of the cluster is 1.10.5. After the upgrade, the Master version is 1.12.4. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/c6ed7a61c8438c6d76c64a34bb925cc3.png)






<span id="Node"></span>
### Upgrading the node Kubernetes version

After the cluster’s Master Kubernetes version is upgraded, the cluster list page will show that an upgrade is available for the cluster node, as shown below:
![](https://main.qcloudimg.com/raw/4981b44503c27682a16fc102713d6d0a.png)



#### Considerations
 - **Before upgrading, read the [Upgrade Notice](#UpgradeNotice).**
 - You can upgrade the node when it’s running.

#### Selecting an upgrade method
You can upgrade the node Kubernetes version in two ways: [reinstall and rolling upgrade](#chongzhuang) and [in-place rolling upgrade](#yuandi). 
- **Reinstall and rolling upgrade**: reinstall the node to upgrade the node version. This method supports major and minor version upgrades, such as upgrades from version 1.10 to version 1.12, or from version 1.14.3 to version 1.14.8.
- **In-place rolling upgrade**: upgrade directly without re-installation. This only replaces components such as Kubelet and kube-proxy. Currently, this method is supported only for minor version upgrades, such as from version 1.14.3 to version 1.14.8.



<span id="chongzhuang"></span>
#### Reinstall and rolling upgrade
Rolling upgrade based on the reinstalled node. Only one node is upgraded at a time. When the previous node is upgraded successfully, the upgrade of next node starts. See below:
![](https://main.qcloudimg.com/raw/bd85fe590108c8aa83eaac53af4439e6.png)

- **Pre-upgrade checking**: check the Pods on a node before draining. The specific items for pre-upgrade checking are as follows:
   - Calculate the number of pods of all workloads in this node. If the pod number of any workload changes to 0 after the node is drained, then the check fails, and the upgrade cannot be performed.
   - The following system control plane workloads will be ignored:
		- l7-lb-controller
		- cbs-provisioner
		- hpa-metrics-server
		- service-controller
		- cluster-autoscaler
- **Evicting Pods**: first mark the node as unschedulable. Then, evict or delete all Pods from the node.
- **Removing nodes**: remove the node from the cluster. This step only performs basic cleanup, and will not delete the node instance of the node in the cluster. Therefore, the node’s attributes such as label and taint are retained.
- **Reinstalling nodes**: reinstall the node’s operating system and reinstall the new version of kubelet.
- **Post-upgrade checking**: check whether the node is ready and schedulable, and check whether the current proportion of unavailable pods exceeds the max limit.


#### Reinstall and rolling upgrade (node Kubernetes version)
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, select the ID of the cluster for node Kubernetes version upgrade to enter the cluster details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the cluster information module, click **Upgrade** to the right of the Node Kubernetes version, as shown in the figure below:
![](https://main.qcloudimg.com/raw/b81c9c37422de8f76b2e51d7017bb416.png)
5. In the **Notes on Upgrade** step, select **Reinstall and rolling upgrade** as the upgrade method. Read the upgrade notice carefully, check the checkbox of **I have read and agree to the terms above**, and then click **Next**.
>! This upgrade method will reinstall the operating system, and the original data will be cleared. Back up the data in advance.

![](https://main.qcloudimg.com/raw/8643f4ba2799bbc7cd7f022e8c465ae7.png)
6. In the **Select nodes** step, select the nodes to be upgraded, and click **Next**.
7. In the **Upgrade Settings** step, enter the node information as required, and click **Next**.
8. In the **Confirmation** step, confirm the information and click **Finish** to start the upgrade.
9. View the progress of the node upgrade until all the nodes are upgraded.

<span id="yuandi"></span>
#### In-place rolling upgrade
Node in-place upgrade uses the rolling upgrade method, meaning that it will only upgrade one node at a time, with the next node not being upgraded until the current node upgrade is successful. In-place upgrade currently only supports upgrading to different minor versions of the same major version. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/c6e9f30699c429a83e621b1d0a82cee5.png)
The steps are described as follows:

1. **Component updating**: replace and restart the kubelet and kube-proxy components on the node.
- **Post-upgrade checking**: check whether the node is ready and check whether the proportion of currently unavailable pods exceeds the max limit.



#### In-place rolling upgrade (node Kubernetes version)
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, select the ID of the desired cluster and enter the cluster details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the cluster information module, click **Upgrade** to the right of the Node Kubernetes version, as shown in the figure below:
![](https://main.qcloudimg.com/raw/598448074a6123e1387cea015e2c2521.png)
4. In the **Notes on Upgrade** step, select **In-place rolling upgrade** as the upgrade method. Read the upgrade notice carefully, place a check mark next to **I have read and agree to the terms above**, and then click **Next**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/a5fa1dbd29f9a24f6930c4e40e12ab2e.png)
6. In the **Select nodes** step, select the nodes to be upgraded, and click **Next**.
7. In the **Confirmation** step, confirm the information and click **Finish** to start the upgrade.
8. View the progress of the node upgrade until all the nodes are upgraded.



