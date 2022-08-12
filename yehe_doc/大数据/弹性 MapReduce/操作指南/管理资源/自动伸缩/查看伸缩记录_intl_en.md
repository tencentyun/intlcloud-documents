The records of automatic scaling actions can be viewed in **Scaling History**.
- Supports filtering the scaling records by time and searching by policy name.
- Supports sorting by **Execution Time**, **Policy Name**, **Scaling Type**, and **Execution Status**. You can click **Details** in the **Operation** column to view detailed information.
- There are four execution statuses of automatic scaling:
	- Executing: The automatic scaling is being executed.
	- Successful: All nodes are added to or removed from the cluster.
	- Partially successful: Some nodes are successfully added or removed from the cluster, while others fail due to disk quota management or CVM inventory.
	- Failed: No node is added to or removed from the cluster.
- **Number of Scaling Nodes** displays the details of the execution result. If the execution fails, it will display the cause of the failure as well as the solution.
- **Scaling Specification** displays the instance specification and the number of added or removed nodes after the rule is triggered.
![](https://qcloudimg.tencent-cloud.cn/raw/2f8243a4f6b5c6e830cd53431ca5b736.jpg)

