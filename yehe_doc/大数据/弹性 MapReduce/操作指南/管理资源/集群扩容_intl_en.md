## Feature Overview
When the computing and storage resources of your EMR cluster are insufficient, you can add more core and task nodes in the console. When the load of the cluster master node is high or runs out of resources, you can scale out the cluster or add router nodes to share the load of the master node or serve as cluster task submitters. You can scale the cluster at any time.

The current scale-out instance specification is the default instance specification selected when the cluster was created. If the current default specification is not available or you want to adjust the configuration, you need to set it in **Node Specification**.

## Prerequisites
- Scale out Router Node: a router node can be used as a submitter, so you can submit Yarn, Hive, and Spark computation tasks to the cluster through it. Therefore, you are recommended to select a model with larger memory, preferably not lower than the master node specification.
- For a pay-as-you-go cluster, all added nodes support the pay-as-you-go billing mode.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster List**, and click the ID/Name of the target cluster to enter the cluster details page.
2. Select **Cluster Resource** > **Resource Management** > **Scale Out** on the cluster details page and select the type of nodes to be added (core, task, or router), optional services, scale-out quantity, etc. as needed.
![](https://main.qcloudimg.com/raw/f10d928355103effbfa67113f4ef6594.png)
3. After selecting the required components and quantity for the added nodes, click **OK** and make the payment. Then, the cluster will start the scale-out operation, which will usually take 10–20 minutes.
 - Deployment Process: it displays the information of corresponding service processes deployed after the component types are selected for added nodes. You can also select **Show Deployment Process** to view the deployment process.
 - Tag: it is used to identify the added node resources.
 - Current Specification: it is the default specification.
    - If the default specification for scale-out is not set, you can set it in [node specification management](https://intl.cloud.tencent.com/document/product/1026/34533) later.
    - The node specification used during scale-out is the default specification. If you want to adjust it, go to the node specification page.


4. For the ClickHouse cluster scale-out, you can add an even number of nodes in the high-availability (HA) mode, and unlimited nodes in non-HA mode. Choose an existing or new cluster for nodes you want to add.
>! There will be no data in the newly added nodes after ClickHouse cluster is scaled out. You need to manually migrate data to achieve data balance and improve the utilization of cluster resources. Migrate data promptly after a successful cluster scale-out.
>
![](https://main.qcloudimg.com/raw/76b2279772ab7a7402d438acbaa60493.png)
