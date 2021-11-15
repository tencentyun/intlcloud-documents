
TencentDB for PostgreSQL allows you to create one or more read-only replicas to form a read-only replica group (RO group), which is suitable for read/write separation and one-primary-multiple-secondary application scenarios and capable of greatly enhancing the read load capacity of your databases. This document describes how to manage RO groups.

## Rebalancing Traffic
- If load rebalancing is disabled, modifying weight will take effect only for new loads but not affect the read-only replicas accessed by existing persistent connections or cause short disconnection from the database.
- If load rebalancing is enabled, the read weights of upgraded read-only replicas will change, which causes all connections to the RO group to be disconnected after the upgrade is completed, and all new connections will be rebalanced according to the new weights.
If you are not satisfied with the connection distribution of each read-only replica in the RO group, you can also manually rebalance it: log in to the [console](https://console.cloud.tencent.com/postgres), click the primary instance ID to access the instance management page, select the **Read-only Replica** tab, locate the desired read-only replica in the RO group, and click **Rebalance** in the **Operation** column.

>!Make sure your business has an automatic reconnection mechanism. Neither enable automatic rebalancing nor manually rebalance if there is no automatic reconnection mechanism.

## Removing Failed Read-only Replicas
When a read-only replica in a RO group becomes inaccessible due to an unexpected error, the RO group automatically removes the read-only replica. This rule is a default rule.

## Removing Delayed Read-only Replicas
If this feature is enabled, a read-only replica will be removed from the RO group if the data sync log size difference between the primary instance and the read-only replica is greater than the specified threshold (MB).

## Allocating Read Weights
The traffic of each read-only replica in an RO group will be automatically distributed according to its read weight, which can realize load balancing and reduce the difficulty of managing multiple read-only replica IP addresses. An RO group automatically allocates read weights to each read-only replica. The following table lists the read weights of read-only replicas of different specifications:
<table>
<tr><th>Specification</th><th>Weight</th></tr>
<tr><td>2 GB memory</td><td>1</td></tr>
<tr><td>4 GB memory</td><td>2</td></tr>
<tr><td>8 GB memory</td><td>2</td></tr>
<tr><td>12 GB memory</td><td>4</td></tr>
<tr><td>16 GB memory</td><td>4</td></tr>
<tr><td>24 GB memory</td><td>8</td></tr>
<tr><td>32 GB memory</td><td>8</td></tr>
<tr><td>48 GB memory</td><td>10</td></tr>
<tr><td>64 GB memory</td><td>12</td></tr>
<tr><td>96 GB memory</td><td>14</td></tr>
<tr><td>128 GB memory</td><td>16</td></tr>
<tr><td>240 GB memory</td><td>26</td></tr>
<tr><td>480 GB memory</td><td>50</td></tr>
</table> 

## References
- For more information on how to create one or more read-only replicas, please see [Creating Read-only Replicas](https://intl.cloud.tencent.com/document/product/409/39545).
- For more information on how to create one or more read-only replicas and add them to an RO group, please see [Managing RO Groups](https://intl.cloud.tencent.com/document/product/409/39546).
