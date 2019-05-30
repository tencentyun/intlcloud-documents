## Operation Scenario

This document explains how to drain or cordon a node.

## Directions

### Cordoning a Node

After a node is cordoned, new Pods cannot be scheduled to it, and if you want to schedule new Pods to it, you will need to manually uncordon it. There are two ways to cordon a node:

#### Method 1

- When [creating a node](https://cloud.tencent.com/document/product/457/32203), on the "CVM configuration" page, click **Advanced settings** and select "Enable cordoning".
![](https://main.qcloudimg.com/raw/c446202f6c0690131d5e99bfc0fe38bf.png)

#### Method 2

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. Click the ID/name of the cluster where node needs to be cordoned to enter the cluster management page. See the figure below:
![](https://main.qcloudimg.com/raw/a81fa565be60dbddafe55010319a4e08.png)
4. In the left sidebar, select "Node Management" > "Nodes" to go to the "Node list" page.
5. In the node list, select the row of the node to be cordoned and click **Cordon**. See the figure below:
![](https://main.qcloudimg.com/raw/73cd2c1930b10f44a1edda90c9a6882b.png)
6. In the pop-up dialog box, click **OK** to complete the cordoning.

### Uncordoning a Node

After a node is uncordoned, new Pods can be scheduled to it. There are two ways to uncordon a node:

#### Method 1

When you create a node by running a script, you can uncordon it by adding a command for uncordoning the node in the script. Below is an example:
```shell
#!/bin/sh
# your initialization script
echo "hello world!"
# If you set unschedulable when you create a node, 
# after executing your initialization script, 
# use the following command to make the node schedulable.
node=`ifconfig eth0 | grep inet | awk '{print $2}' | tr -d "addr:"`
#echo ${node}
kubectl uncordon ${node} --kubeconfig=/root/.kube/config
```
The `kubectl uncordon` command indicates uncordoning the node.

#### Method 2

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. Click the ID/name of the cluster where node needs to be uncordoned to enter the cluster management page. See the figure below:
![](https://main.qcloudimg.com/raw/a81fa565be60dbddafe55010319a4e08.png)
4. In the left sidebar, select "Node Management" > "Nodes" to go to the "Node list" page.
5. In the node list, select the row of the node to be uncordoned and click **Uncordon**. See the figure below:
![](https://main.qcloudimg.com/raw/13787bfc8e94e280cf0904f29dcf5712.png)
6. In the pop-up dialog box, click **OK** to complete the uncordoning.

### Draining a Node

#### Overview

Before performing maintenance on a node, you can safely evict a Pod from a node by draining the node. After the node is drained, all Pods (excluding those managed by DaemonSet) in the node will be automatically evicted to other nodes in the cluster, and the drained node will be set to cordoned status.
>! For locally stored Pods, data will be lost after they are evicted. Please be cautious when doing so.

#### Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. Click the ID/name of the cluster where node needs to be uncordoned to enter the cluster management page. See the figure below:
![](https://main.qcloudimg.com/raw/a81fa565be60dbddafe55010319a4e08.png)
4. In the left sidebar, select "Node Management" > "Nodes" to go to the "Node list" page.
5. In the row of the node to be drained, click **More** > **Drain**. See the figure below:
![](https://main.qcloudimg.com/raw/79aaa2483a61583cce6cbe3ba24a8089.png)
6. In the pop-up dialog box, click **OK** to complete the draining.
