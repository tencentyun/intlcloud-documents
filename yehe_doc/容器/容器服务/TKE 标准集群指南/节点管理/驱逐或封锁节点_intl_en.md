## Overview

This document explains how to drain or cordon a node.

## Directions

### Cordoning a Node

After cordoning a node, new Pods cannot be scheduled to it. If you want to schedule a Pod to the node, you need to uncordon the node manually. If a node has been bound as backend target node, it will be removed from the target node list after it is condoned. You can cordon a node with one of the following two methods:
<dx-tabs>
::: Method A
- When [adding a node](https://intl.cloud.tencent.com/document/product/457/30652), on the **CVM Configuration** page, click **Advanced Settings** and select **Cordon this node**.
![](https://main.qcloudimg.com/raw/037232a406de9c6aba88662896edb9d5.png)
:::
::: Method B
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. Click the ID/name of the cluster where to cordon the node to go to the cluster management page as shown below.
![](https://main.qcloudimg.com/raw/b8c00a8ebed60c3e7c2169ae901f2eb1.png)
4. In the left sidebar, select **Node Management** > **Nodes** to go to the **Node List** page.
5. In the node list, select the row of the node to be cordoned and click **Cordon** as shown below.
![](https://main.qcloudimg.com/raw/1223786bd47bd64f72a2610093d9cf82.png)
6. In the pop-up dialog box, click **OK** to complete the cordoning.
:::
</dx-tabs>



### Uncordoning a Node

After a node is uncordoned, new Pods can be scheduled to it. You can uncordon a node with one of the following two methods:
<dx-tabs>
::: Method A
When you create a node by running a script, you can uncordon it by adding a command for uncordoning the node in the script. Below is an example:
```shell
#!/bin/sh
# your initialization script
echo "hello world!"
# If you set unschedulable when you create a node, 
# after executing your initialization script, 
# use the following command to make the node schedulable.
node=`ps -ef|grep kubelet|grep -oE 'hostname-override=\S+'|cut -d"=" -f2`
#echo ${node}
kubectl uncordon ${node} --kubeconfig=/root/.kube/config
```

The `kubectl uncordon` command indicates uncordoning the node.

:::
::: Method B
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. Click the ID/name of the cluster where to uncordon the node to go to the management page of the cluster. See the figure below:
![](https://main.qcloudimg.com/raw/90b8582a585f296f797c0ecd316c3045.png)
4. In the left sidebar, select **Node Management** > **Nodes** to go to the **Node List** page.
5. In the node list, select the row of the node to be uncordoned and click **Uncordon** as shown below.
![](https://main.qcloudimg.com/raw/cc8c6f0b271ad7fb839dd689348104a1.png)
6. In the pop-up dialog box, click **OK** to complete the uncordoning.

:::
</dx-tabs>



### Draining a Node

#### Overview

Before performing maintenance on a node, you can safely drain a Pod from a node by draining the node. After the node is drained, all Pods (excluding those managed by DaemonSet) in the node will be automatically drained to other nodes in the cluster, and the drained node will be set to cordoned status.
>! For locally stored Pods, data will be lost after they are drained. Please be cautious when doing so.

#### Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. Click the ID/name of the cluster where to drain the node to go to the management page of the cluster. See the figure below:
![](https://main.qcloudimg.com/raw/549dd5be2af3ebf26a31a313e832bbf0.png)
4. In the left sidebar, select **Node Management** > **Nodes** to go to the **Node List** page.
5. Click **More** > **Drain** in the row of the node to be drained. See the figure below:
![](https://main.qcloudimg.com/raw/d1d4f0fdd6cd819958046aa36a2f0f24.png)
6. In the pop-up dialog box, click **OK** to complete the draining.






