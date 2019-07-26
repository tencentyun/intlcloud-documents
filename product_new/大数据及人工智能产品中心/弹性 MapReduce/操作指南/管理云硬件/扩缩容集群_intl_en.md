## Application Scenario
The EMR Console allows you to manage all kinds of nodes in your cluster, including the master node, core nodes, and task nodes, common nodes, router nodes, and MySQL metadatabase, if any.

## Operation Guide

### Scaling out Cluster
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and select **Cloud Hardware Management** in the left sidebar.
    ![](https://main.qcloudimg.com/raw/c518ad31fed7dae6f80878f26e6ec68e.png)
2. Select the core or task node to add to the cluster and click **Scale Up**.
3. Select the desired number of nodes and click **Confirm**. Once you’ve paid, please wait and let the cluster complete the scaling-up, which usually takes about 10 to 20 minutes.
>We do not recommend terminating the Core node after the scaling-out. The Core node stores your data and you may lose your data once it is terminated.
>
![](https://main.qcloudimg.com/raw/c2f862848dd9bb390f0679530a0da235.png)


### Scaling In Cluster
>After a node is terminated, **the data stored in it will be deleted**. By terminating a node, you confirm that the data in it can be deleted.

You can scale in a cluster by terminating the task nodes in it. On the list page, select the task node to be terminated (if you select other node types at the same time, the **Scale In** button will be grayed out) and click **Scale In**.
- Pay-as-you-go nodes will start the termination process directly.
