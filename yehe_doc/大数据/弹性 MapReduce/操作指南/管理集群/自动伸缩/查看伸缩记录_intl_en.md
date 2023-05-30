The records of auto scaling actions can be viewed in **Scaling history**. Grading of auto scaling events is supported, and event alarm policies are set based on the event level. For more information about event levels, see [Cluster Events](https://intl.cloud.tencent.com/document/product/1026/36889). For more information about event alarm configuration, see [Alarm Configurations](https://intl.cloud.tencent.com/document/product/1026/31120).
## Custom Scaling Records
- Supports filtering the scaling records by execution time range and searching by policy name.
- Sorts by **Execution time**, and displays **Execution time**, **Policy name**, **Scaling type**, and **Execution status**. You can click **Details** in the **Operation** column to view details.
- There are four auto scaling execution statuses:
	- Executing: The automatic scaling is being executed.
	- Successful: All nodes are added to or removed from the cluster.
	- Partially successful: Some nodes are successfully added or removed from the cluster, while others fail due to disk quota management or CVM inventory.
	- Failed: No node is added to or removed from the cluster.
- **Resource supplement retry** displays whether this feature is enabled. If it is enabled, the retries will be displayed.
- **Elastic node count** displays the details of the execution result. If the execution fails, it will display the cause of the failure as well as the solution.
- **Scaling Specification** displays the instance specification and the number of added or removed nodes after the rule is triggered.
![](https://qcloudimg.tencent-cloud.cn/raw/8ea2558be96c35666a45217ac351df0c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/baacd6d01c81cb98e6583377ed56620d.png)

## Managed scaling records
- Supports filtering the scaling records by **Execution Time** or **Scaling Type**.
- Supports sorting by **Execution Time**, **Scaling Type**, **Model Specification**, **Quantity**, **Execution Status**, or **Reason**.
- There are two execution statuses of managed scaling:
	- Successful: The target node is added to or removed from the cluster based on the cluster load.
	- Failed: The target node failed to be added to the cluster based on the cluster load due to resource insufficiency. We recommend you modify the preset resource specification.
- Model Specification: The target model specification and type after the rule is triggered for a scale-out or scale-in.
- Quantity: The number of added or removed nodes in various specifications after the operation.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dfK3476_%E5%9B%BD%E9%99%8539.png)
