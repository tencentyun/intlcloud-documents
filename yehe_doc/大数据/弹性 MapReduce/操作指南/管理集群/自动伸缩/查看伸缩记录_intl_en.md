The records of auto-scaling actions can be viewed in **Scaling history**.
## Custom scaling records
- Supports filtering the scaling records by execution time range and search by policy name.
- Sorts by **Execution time**, and displays **Execution time**, **Policy name**, **Scaling type**, and **Execution status**. You can click **Details** in the **Operation** column to view details.
- There are four auto-scaling execution statuses:
	- Executing: The auto-scaling is being executed.
	- Successful: All nodes are added to or removed from the cluster.
	- Partially successful: Some nodes are successfully added or removed from the cluster, while others fail due to disk quota management or CVM inventory.
	- Failed: No node is added to or removed from the cluster.
- **Resource supplement retry** displays whether this feature is enabled. If it is enabled, the number of retries will be displayed.
- **Elastic node count** displays the details of the execution result. If the execution fails, it will display the cause of the failure as well as the solution.
- **Scaling spec** displays the specification executed successfully and the number of added or removed nodes after the rule is triggered.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RNkt960_%E5%9B%BD%E9%99%8527.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/n67K301_%E5%9B%BD%E9%99%8528.png)

## Managed scaling records
- Supports filtering the scaling records by execution time range and scaling type.
- Sorts by **Execution time**, and displays **Scaling type**, **Model spec**, **Quantity**, **Execution status**, and **Reason**.
- There are two execution statuses of managed scaling:
	- Successful: The target nodes are added to or removed from the cluster based on the cluster load.
	- Failed: The target nodes failed to be added to the cluster based on the cluster load due to resource insufficiency. In this case, we recommend you modify preset resource specification.
- Model spec: The specification and type of models added or removed after a scale-out or scale-in rule is triggered.
- Quantity: The number of added or removed nodes in various specifications after the operation.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/2Iv9588_%E5%9B%BD%E9%99%85%E7%AB%9929.png)
