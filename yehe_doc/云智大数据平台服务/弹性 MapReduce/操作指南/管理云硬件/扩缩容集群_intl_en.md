## Operation Scenarios
The EMR Console allows you to manage all kinds of nodes in your cluster, including the master node, core nodes, and task nodes, common nodes, router nodes, and MySQL metadatabase, if any.

## Directions

### Scaling out cluster
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and select **Cloud Hardware Management** in the left sidebar.
![](https://main.qcloudimg.com/raw/15c18b6f04d6fdd37fcdba2cf89b5dbf.png)
2. Select the core or task node to add to the cluster and click **Scale Up**.
 - Pay-as-you-go clusters can be scaled out only with pay-as-you-go nodes.
> Scale Router Node: a router node can be used as a submitter; therefore, you can submit Yarn, Hive, and Spark computation tasks to the cluster through it. Therefore, you are recommended to select a model with larger memory, preferably not lower than the master node specification.
3. Select the desired components and quantity for node expansion and click **OK**. After the payment is successfully made, the cluster will start to be scaled out. The operation usually takes 10 to 20 minutes. Please wait patiently. You can also choose to check **Show Deployment Progress** to view the deployment progress which displays the service information of corresponding processes deployed after the component types are selected for node expansion.
4. 	The tag is used to identify the node expansion resources.
5. 	Current specification is the default specification.
a. If the default specification for expansion is not set, you can set it in [node specification management](https://intl.cloud.tencent.com/document/product/1026/34533) later.
b. The node specification used during expansion is the default specification. If you want to adjust it, go to the node specification page.
 
>You are not recommended to terminate the core node after the expansion, as it stores your data and you may lose your data once it is terminated.
>
![](https://main.qcloudimg.com/raw/f10d928355103effbfa67113f4ef6594.png)

### Scaling in cluster
>After a node is terminated, the data stored in it will be deleted. By terminating a node, you confirm that the data in it can be deleted.

You can scale in a cluster by terminating the task nodes in it. On the list page, select the task node to be terminated (if you select other node types at the same time, the **Scale In** button will be grayed out) and click **Scale In**.
- On-demand cluster: once terminated, the cluster will not be retained in the recycle bin but will be completely terminated and cannot be recovered. Please do so with caution.
Before terminating a cluster, please make sure that your data has been backed up as it cannot be recovered after termination.
