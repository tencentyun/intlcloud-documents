## Scenario
This document describes how to add nodes to the edge cluster that you created.


## Prerequisites
Prepare as instructed below:
- Node source: you can use an existing server in the [CVM console](https://console.cloud.tencent.com/cvm) or the [ECM console](https://console.cloud.tencent.com/ecm/instance), or a server on another platform or in your on-premises data center.
- Node processor: supports x86_64, ARM, and ARM64.
- The following operating systems of nodes are supported:
 - Ubuntu 18.04 and 16.04
 - CentOS 7.6, 7.5, and 7.4
 - Tencent Linux Release 2.4 and 2.2 (Final)
 - SUSE Linux Enterprise Server 12 SP3
 - Debian 9.0
- Ensure that `wget`, `systemctl`, and `iptable` have been installed on the node to be added.
- The node network must be able to actively access the internet.

## Directions
1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Edge Clusters** in the left sidebar.
2. On the **Edge Clusters** page, click the cluster ID to go to the **Deployment** management page.
3. In the left sidebar, choose **Node Management** > **Node** to go to the **Node List** page.
4. On the **Node List** page, click **Add a node**.
5. In the **Add a node** window that appears, complete the following steps to obtain the node initialization script.
   1. Obtain the initial configuration from the **Configure** step. You can modify the following parameters:
      - **Interface**: indicates the network interface used by the node to communicate within the private network.
      - **NodeName**: indicates the name of the node in the cluster. This name must be unique in the cluster.
   2. Click **Next: install**. If you are prompted to enable public network access, click <img src="https://main.qcloudimg.com/raw/fd1ae3941057881ca71bcf8b2874b510.png" style="margin:-6px 0px"> to enable it.
   3. In the **Install** step, copy the script download command for downloading the node initialization script.
4. Log in to the prepared server, switch to the `root` account, and run the copied command.
5. Run the following commands to execute the node initialization script.
```
chmod +x script.sh
```
```
./script.sh
```
6. After the script is successfully executed, go to the "Node List" page and refresh it to check that the newly added node exists.
You can also perform other node operations, such as draining, removing, cordoning, or uncordoning a node, and editing the node label.

## Relevant Operations
<span id="OpenExtranetAccess"></span>

### Disabling public network access for a cluster

1. On the **Edge Clusters** page, click **View cluster credentials** for the cluster for which you want to disable public network access.
2. In the "Cluster Credentials" window that appears, click <img src="https://main.qcloudimg.com/raw/84c11b68fbbd46c46c2cae68d45baee2.png" style="margin:-6px 0px"> for "public network access" to disable public network access for the cluster.
