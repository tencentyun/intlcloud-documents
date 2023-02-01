The records of automatic scaling actions can be viewed in **Scaling History**.
## Custom scaling records
- Supports filtering the scaling records by time and searching by policy name.
- Supports sorting by **Execution Time**, **Policy Name**, **Scaling Type**, or **Execution Status**. You can click **Details** in the **Operation** column to view detailed information.
- There are four execution statuses of automatic scaling:
	- Executing: the automatic scaling is being executed.
	- Successful: all nodes are added to or removed from the cluster.
	- Partially successful: Some nodes are successfully added or removed from the cluster, while others fail due to disk quota management or CVM inventory.
	- Failed: no node is added to or removed from the cluster.
- **Number of Scaling Nodes** displays the details of the execution result. If the execution fails, it will display the cause of the failure as well as the solution.
- **Scaling Specification** displays the instance specification and the number of added or removed nodes after the rule is triggered.
![](https://qcloudimg.tencent-cloud.cn/raw/17eec852791477154ff4cb5723ad04dc.png)


## Managed scaling records
- Supports filtering the scaling records by **Execution Time** or **Scaling Type**.
- Supports sorting by **Execution Time**, **Scaling Type**, **Model Specification**, **Quantity**, **Execution Status**, or **Reason**.
- There are two execution statuses of managed scaling:
	- Successful: The target node is added to or removed from the cluster based on the cluster load.
	- Failed: The target node failed to be added to the cluster based on the cluster load due to resource insufficiency. We recommend you modify the preset resource specification.
- Model Specification: The target model specification and type after the rule is triggered for a scale-out or scale-in.
- Quantity: The specification and number of added or removed nodes after the operation.
![](https://qcloudimg.tencent-cloud.cn/raw/2f8243a4f6b5c6e830cd53431ca5b736.jpg)
