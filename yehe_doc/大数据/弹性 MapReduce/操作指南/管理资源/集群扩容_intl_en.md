## Feature Description
When the compute and storage resources of your EMR cluster are insufficient, you can add more core and task nodes in the console. When the master node is overloaded or runs out of resources, you can scale out the cluster or add router nodes to share the load of the master node or to serve as task submitters in the cluster. You can scale the cluster at any time.

The current scale-out instance specification is the default instance specification selected when the cluster was created. If the current default specification is not available or you want to adjust the configuration, you need to set it in [node specification](https://intl.cloud.tencent.com/document/product/1026/34533).

## Prerequisites
- Add router nodes: A router node can be used as a submitter, through which you can submit Yarn, Hive, and Spark computing tasks to the cluster. We recommend you select a model with larger memory, preferably not lower than the master node specification.
- For a pay-as-you-go cluster, all newly added nodes support the pay-as-you-go billing mode.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Resource** > **Resource Management** > **Scale Out** and select the type of nodes to be added (core, task, or router), billing mode, AZ, subnet, optional services, scale-out quantity, etc. as needed.
![](https://main.qcloudimg.com/raw/f10d928355103effbfa67113f4ef6594.png)

 - Deployment process: Displays the information of service deployment processes after components are selected for the added nodes. You can also select **Show deployment process** to view the deployment process.
 - Do not start services after scaling: If this option is selected during scaling, added nodes will not start the service. When needed, you can start the service through [starting/stopping services](https://intl.cloud.tencent.com/document/product/1026/40259).
 - Tag: Used to identify the added node resources.
 - Current specification: The default specification.
    - You can set the default specification for scale-out by clicking [Set Node Specification](https://intl.cloud.tencent.com/document/product/1026/34533).
    - The default node specification is used for scale-out. You can adjust it by clicking **Set Node Specification**.
3. After selecting the components and node quantity, click **Confirm**, and make the payment. Then, the cluster will start scaling out, which usually takes 10 to 20 minutes.
4. For ClickHouse cluster scale-out, you can add an even number of nodes in a high-availability (HA) instance, and unlimited nodes in a non-HA instance. You can choose an existing cluster or a new one for the nodes to be added.
>! There will be no data in the newly added nodes after the virtual ClickHouse cluster is scaled out. You need to migrate the data manually as the system won't automatically do it for you. In order to achieve data balance and improve resource utilization, migrate your data in time after successful cluster scaling.

