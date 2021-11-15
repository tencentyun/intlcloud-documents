TencentDB for PostgreSQL allows you to create one or more read-only replicas to form a read-only replica group (RO group), which is suitable for read/write separation and one-primary-multiple-secondary application scenarios and capable of greatly enhancing the read load capacity of your databases.

## Prerequisites
- You have created a primary instance. For more information, please see [Purchasing Instances](https://intl.cloud.tencent.com/document/product/409/7550).
- You have created one or more read-only replicas. For more information, please see [Creating Read-only Replicas](https://intl.cloud.tencent.com/document/product/409/39545).

## [Creating an RO Group](id:cjzdslrz)
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click the instance ID or **Manage** in the **Operation** column to access the instance management page.
2. Click **Add Read-only Replica** in the **Instance Architecture Diagram** section on the **Instance Details** tab or click **Create** on the **Read-only Replica** tab.
![](https://main.qcloudimg.com/raw/bcc375d86e0cbccea0c51fc473dab6da.png)
3. On the displayed purchase page, specify the following read-only replica configurations, confirm that everything is correct, and click **Buy Now**.
 - **Specify RO Group**: the **Create RO Group** option indicates that if multiple read-only replicas are purchased at a time, all of them will be assigned to the newly created RO group. The RO group automatically allocates read weights to each read-only replica, and automatically distributes read requests among the read-only replicas based on their read weights.
 - **RO Group Name**: the RO group name doesn't have to be unique and can contain up to 60 characters comprised of letters, digits, "-", "_", and ".".
 - **Remove Read-only Replicas Exceeding the Delay Threshold**: this option indicates whether to enable the removal policy. A read-only replica is removed from the RO group when its delay exceeds the threshold, and rejoins to the RO group when its delay is smaller than the threshold. A removed read-only replica will become inactive, its weight will be set to 0 automatically, and warning notifications will be sent out. For more information on how to configure the read-only replica removal alarm and recipients, please see [Alarming](https://intl.cloud.tencent.com/document/product/409/7563). 
    Whether or not this feature is enabled, read-only replicas will be removed upon failure, and rejoin to the RO group when it is recovered.
 - **Delay Threshold**: set a delay threshold for a read-only replica. When the data sync log size difference between the primary instance and the read-only replica is greater than the specified threshold, the read-only replica will be removed from the RO group.
 - **Minimum Read-only Replicas**: this is the minimum number of read-only replicas that have to be retained in the RO group. When there are fewer read-only replicas in the RO group, even if a read-only replica exceeds the delay threshold, it will not be removed.
![](https://main.qcloudimg.com/raw/bf44729ad18ba556ec19ebf652bd668b.png)
5. Return to the instance list. The status of the created read-only replica is **Delivering**. If the status changes to **Running**, the read-only replica has been successfully created.

## Configuring an RO Group
On the RO group configuration page, you can configure the basic information of the group such as name, removal policy, delay threshold, minimum number of retained read-only replicas, and read weights.
>?Read-only replicas in an RO group can have different specifications, and read weights are automatically allocated to each replica according to its specification.
>
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click the primary instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Read-only Replica** tab, click **Configuration** in the **Operation** column in the RO group list to access the RO group configuration page.
![](https://main.qcloudimg.com/raw/3d3181b7bc09b6bc484e78a4e4011f0c.png)
3. Configure the RO group and click **Submit**.
 - **Assign Read Weight**: the traffic of each read-only replica in an RO group will be automatically distributed according to its read weight, which can realize load balancing and reduce the difficulty of managing multiple read-only replica IP addresses. An RO group automatically allocates read weights to each read-only replica. The following table lists the read weights of read-only replicas of different specifications:
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
 - **Rebalance Load**:
    - If load rebalancing is disabled, modifying weight will take effect only for new loads, but neither affect the read-only replicas accessed by existing persistent connections nor cause short disconnection from the database.
    - If load rebalancing is enabled, when the configurations of read-only replicas in the RO group are modified, all connections to the RO group will be disconnected and new connections will be rebalanced according to the weights.
![](https://main.qcloudimg.com/raw/45b4aacc78429c2cb47bf3a9c226cd22.png)

## Deleting an RO Group
An RO group can be deleted if it has no read-only replicas.
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click the primary instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Read-only Replica** tab, locate the desired RO group, confirm that it has no read-only replicas, and click **More** > **Delete** in the **Operation** column.
![](https://main.qcloudimg.com/raw/f90e124d71f1ff3324d3dce408a68d46.png)
