TencentDB for MongoDB allows you to adjust certain database parameters, so that the database features can better adapt to your business needs. 

## Background
In the daily OPS process, quickly adjusting database parameters can optimize the query and management performance of the database in a targeted manner for ever-changing business scenarios. In addition, the parameter modification records can be viewed at any time for evidence-based problem locating.

## Version Description
Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support database parameter modification. However, there are differences in the modifiable parameters on each version as displayed in the console.

## Notes
- Currently, the parameter modification feature only supports parameters that can take effect without restart required after modification. It will support other parameters in future iterations. You can also restart the instance on the MongoDB terminal. The restart will cause a disconnection. Therefore, make business arrangements in advance and proceed with caution.
- When updating the cluster architecture or configuration, such as adjusting specifications, nodes, or shards, upgrading nodes, and migrating nodes, you don't need to configure parameters repeatedly, as the system will automatically sync the parameter configuration data.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The instance is running normally.

## Directions
### Querying parameter configuration
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb/sharding).
2. On the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. In the instance list on the right, find the target instance.
4. Click the target instance ID to enter the **Instance Details** page.
5. Select the **Parameter Settings** tab to view the database parameter configuration.

### Modifying parameter configuration
1. On the **Modifiable Parameters** tab, click **Modify Current Value**.
2. In the input box in the **Current Value** column, set the desired parameter value as shown below:
>?
>- You can modify multiple parameters at the same time.
>- When modifying parameters, be sure to set them according to the **acceptable values**.
>- In the **Restart upon Modification** column, check whether the instance will be restarted. The restart will cause a disconnection. Therefore, make business arrangements in advance and proceed with caution.
>  The acceptable values of parameters depend on the instance version and architecture. The parameters that can be modified on the current version are as listed below: 

<table width="100">
<thead>
<tr><th width="5%">Parameter</th><th width="5%">Restart upon Modification Required</th><th width="5%">Default Value</th><th width="5%">Acceptable Values</th><th width="5%">Supported Version</th><th width="25%">Supported Instance Type</th><th width="25%">Applicable Scope</th><th width="30%">Description</th></tr></thead>
<tbody>
<tr>
<td>operation.profiling.<br>slowOpThresholdMs</br></td>
<td>No</td>
<td>100</td>
<td>[0-65536]</td>
<td>4.0, 4.2</td>
<td>Replica set instance, sharded instance</td>
<td>mongod, mongos</td>
<td>Sets the slow query judgment time in ms.</td></tr>
<tr>
<td>operationProfiling.mode</td>
<td>No</td>
<td>off</td>
<td>off, slowOp, all</td>
<td>3.2, 3.6, 4.0, 4.2</td>
<td>Replica set instance, sharded instance</td>
<td>mongod</td>
<td>Sets the enabled Profile level.</td></tr>
<tr>
<td>setParameter.<br>cursorTimeoutMillis</br></td>
<td>No</td>
<td>600000</td>
<td>[1,2147483647]</td>
<td>3.2, 3.6, 4.0, 4.2</td>
<td>Replica set instance, sharded instance</td>
<td>3.2 and 3.6: mongod<br>4.0 and 4.2: mongod, mongos</br></td>
<td>Sets the cursor timeout period in ms.</td></tr>
<tr>
<td>setParameter.<br>intenalQueryExecMaxBlockingSortBytes</br></td>
<td>No</td>
<td>33554432</td>
<td>[33554432,268435456]</td>
<td>4.0, 4.2</td>
<td>Replica set instance, sharded instance</td>
<td>mongod, mongos</td>
<td>Sets the maximum memory that `Sort` can support in bytes.</td></tr>
<tr>
<td>setParameter.<br>maxTransactionLockRequestTimeoutMillis</br></td>
<td>No</td>
<td>5</td>
<td>[0,60]</td>
<td>4.0, 4.2</td>
<td>Replica set instance, sharded instance</td>
<td>mongod</td>
<td>Sets the waiting time for a single transaction lock in ms.</td></tr>
<tr>
<td>setParameter.<br>transactionLifetimeLimitSeconds</br></td>
<td>No</td>
<td>60</td>
<td>[5,300]</td>
<td>4.0, 4.2</td>
<td>Replica set instance, sharded instance</td>
<td>mongod</td>
<td>Sets the maximum lifetime of a single transaction in s.</td></tr>
<tr>
<td>setParameter.<br>failIndexKeyTooLong</br></td>
<td>No</td>
<td>true</td>
<td>true, false</td>
<td>3.2, 3.6, 4.0</td>
<td>Replica set instance, sharded instance</td>
<td>mongod</td>
<td>Sets whether to limit the length of the index key.</td></tr>
<tr>
<td>balance.window</td>
<td>No</td>
<td>NULL</td>
<td>true, false</td>
<td>4.0, 4.2</td>
<td>Sharded instance</td>
<td>mongos</td>
<td>Sets the time period to open the balance window.</td></tr>
<tr>
<td>openBalance.window</td>
<td>No</td>
<td>false</td>
<td>true, false</td>
<td>4.0, 4.2</td>
<td>Sharded instance</td>
<td>mongos</td>
<td>Enables or disables the balance window.</td></tr>
</tbody></table>
3. Click **OK**.

### Querying parameter modification record
1. On the **Parameter Settings** tab, click **Modification Log**.
2. View the parameter modification log, including values before and after modification, modification status, and modification time.


