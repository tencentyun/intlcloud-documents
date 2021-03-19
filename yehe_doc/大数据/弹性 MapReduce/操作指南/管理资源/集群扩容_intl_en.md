## Feature Overview
When the compute and storage resources of your EMR cluster are insufficient, you can add more core and task nodes in the console. When the master node is overloaded or runs out of resources, you can scale out the cluster or add router nodes to share the load of the master node or to serve as task submitters in the cluster. You can scale the cluster at any time.

The default scale-out instance specification is the instance specification selected when the cluster is created. If the default specification is sold out or you want to adjust the configuration, you can set it in **Node Specification**.

## Prerequisites
- Add router nodes: a router node can be used as a submitter, through which you can submit Yarn, Hive, and Spark computing tasks to the cluster. You are advised to select a model with larger memory, preferably not lower than the master node specification.
- For a pay-as-you-go cluster, all newly added nodes support the pay-as-you-go billing mode.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click a cluster ID/name on the **Cluster List** page to go to the cluster details page.
2. On the cluster details page, select **Cluster Resource** > **Resource Management** > **Scale Out** and select the type of nodes to be added (core, task, or router), billing mode, optional services, scale-out quantity, etc. as needed.
![](https://main.qcloudimg.com/raw/f10d928355103effbfa67113f4ef6594.png)
3. After selecting the components and node quantity, click **Confirm**, and make the payment. Then, the cluster will start scaling out, which usually takes 10 to 20 minutes.
 - Deployment process: displays the information of service deployment processes after components are selected for the added nodes. You can also select **Show deployment process** to view the deployment process.
 - Tag: used to identify the added node resources.
 - Current specification: the default specification.
    - You can set the default specification for scale-out by clicking [Set Node Specification](https://intl.cloud.tencent.com/document/product/1026/34533).
    - The default node specification is used for scale-out. You can adjust it by clicking **Set Node Specification**.
4. For ClickHouse cluster scale-out, you can add an even number of nodes in a high-availability (HA) instance, and unlimited nodes in a non-HA instance. You can choose an existing cluster or a new one for the nodes to be added.
>!There will be no data in the newly added nodes after a ClickHouse cluster is scaled out. You need to manually migrate data to achieve data balance and improve the utilization of cluster resources. Please migrate data instantly after the cluster scale-out is completed successfully.
>
![](https://main.qcloudimg.com/raw/76b2279772ab7a7402d438acbaa60493.png)
