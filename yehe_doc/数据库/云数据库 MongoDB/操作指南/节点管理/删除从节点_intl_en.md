## Overview

Deleting secondary nodes can reduce the high availability of a cluster. When the business load is low, you can remove secondary nodes appropriately to avoid wasting resources.

## Instructions

- Deleting secondary nodes can reduce the high availability of a cluster. Therefore, proceed with caution. Make sure that after some secondary nodes are deleted, the cluster still has three (one-primary-two-replica), five (one-primary-four-replica), or seven (one-primary-six-replica) nodes in total.
- A hidden node cannot be deleted, as when a secondary node fails, the system will automatically switch it with the hidden node to guarantee the cluster's high availability.
- The IP address of a deleted secondary node won't be retained, so connections to thesecondary node will be closed.


## Prerequisites

- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- If your instance is pay-as-you-go, make sure that your Tencent Cloud account balance is sufficient.
- The instance and its associated instances are in **Running** status and are not executing any tasks.

## Deleting a secondary node (replica set)

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the **Instance ID** to enter the **Instance Details** page and click the **Node Management** tab.
6. On the **Mongod Node** tab on the **Node Management** tab, select the target secondary node in the **Instance List** and select **Operation** > **Delete Secondary Node**.
> ?In the node list, if the value of a node in the **Hidden** column is **true**, the node is hidden and cannot be deleted.
7. In the **Delete Secondary Node** pop-up window, read the notes on node quantity adjustment and confirm the instance name.

<table class="table-striped">
<tbody>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
   <tr>
   <td>Instance ID/Name</td>
   <td>The name of the instance for which to adjust the node quantity.</td></tr>	
   <tr>
   <td>Instance Configuration</td>
   <td>Check the current specification of the instance, including the CPU core quantity, memory, disk capacity, and node quantity. The node quantity includes all primary and secondary nodes. The nodes are evenly distributed to shards; for example, if there are two shards and eight nodes, each shard will have four nodes. You should determine the number of nodes to be deleted based on the current specification.</td>    </tr>	
   <tr>
   <td>Secondary Node Information</td>
   <td>Confirm the information of the secondary nodes to be deleted, including the node ID, AZ, role, and tags.</td>   </tr>
   <tr>
   <td>Configuration Change Fees</td>
   <td>Fees after specification adjustment. In pay-as-you-go billing mode, fees are charged hourly by the new specification in three billing tiers.</td>   </tr>
   <tr>
   <td>Compare</td>
   <td>You can compare the specifications and maximum numbers of connections before and after the specification adjustment of mongod secondary nodes in order to assess whether the new specification meets your needs.</td>    </tr>
</tbody></table>  
8. Confirm the fees and click **OK**.
9. On the left sidebar, select **Task Management**, and you can view the ongoing task. Wait until **Task Progress** becomes **100%** and **Task Status** becomes **Completed**.

## Related APIs

| API                                                 | Description     |
| ------------------------------------------------------------ | -------------------- |
| [ModifyDBInstanceSpec](https://intl.cloud.tencent.com/document/product/240/34699) | Adjusts TencentDB instance configuration. |


