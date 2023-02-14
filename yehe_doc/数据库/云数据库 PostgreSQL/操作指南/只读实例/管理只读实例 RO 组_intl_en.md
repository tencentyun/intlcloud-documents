TencentDB for PostgreSQL allows you to create one or more read-only instances to form an RO group, which is suitable for read/write separation and one-primary-multiple-standby application scenarios. This greatly improves the read load capacity of your database.

## Prerequisites
- You have created a primary instance. For more information, see [Purchase Methods](https://intl.cloud.tencent.com/document/product/409/40953).
- You have created a read-only instance. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/409/39545).

## [Creating RO Group](id:cjzdslrz)
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click **More** > **Create Read-Only Instance** in the **Operation** column of the target instance to enter the instance purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/6495563cd3e7f4b4fb179498ea7c7d56.png)
>?You can also click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
>- Click **Add Read-Only Instance** in the **Instance Architecture Diagram** section on the **Instance Details** tab to enter the read-only instance purchase page.
>- Or, click **Create** on the **Read-Only Instance** tab to enter the read-only instance purchase page.
![](https://main.qcloudimg.com/raw/bcc375d86e0cbccea0c51fc473dab6da.png)
2. On the purchase page, select the desired read-only instance configuration, confirm that everything is correct, and click **Buy Now**.
 - **Specify RO Group**: Select **Create RO Group**. If multiple read-only instances are purchased at a time, all of them will be assigned to the newly created RO group. The RO group automatically allocates read weights to each read-only instance and automatically distributes read requests among them based on their read weights.
 - **RO Group Name**: The RO group name doesn't need to be unique and can contain up to 60 letters, digits, hyphens, and underscores.
 - **Remove Delayed RO Instances**: This option indicates whether to enable the removal policy. A read-only instance will be removed from the RO group when its delay exceeds the threshold, and will rejoin the RO group when its delay drops below the threshold. A removed read-only instance will become inactive, its weight will be set to 0 automatically, and warning notifications will be sent. For more information on how to configure read-only instance removal alarms and recipients, see [Alarming Feature](https://intl.cloud.tencent.com/document/product/409/7563).
    No matter whether delayed read-only instance removal is enabled, a read-only instance that is removed due to instance failure will rejoin the RO group when it is repaired.
 - **Delay**: This sets the delay time for a read-only instance. When the threshold is exceeded, the instance will be removed from the RO group.		
 - **Delay Threshold**: This sets the delay threshold for a read-only instance. When the data sync log size difference between the primary instance and the read-only instance is above the threshold, the read-only instance will be removed from the RO group.
 - **Least RO Instances**: This is the minimum number of instances that should be retained in the RO group. When there are fewer instances in the RO group, even if an instance exceeds the delay threshold, it will not be removed.
![](https://main.qcloudimg.com/raw/bf44729ad18ba556ec19ebf652bd668b.png)
3. Return to the instance list. The status of the created instance is **Delivering**. After the status changes to **Running**, the read-only instance has been successfully created.

## Configuring RO Group
On the RO group configuration page, you can configure the basic information of the group such as name, removal policy, delay threshold, and least read-only instances.
>?Read-only instances in an RO group can have different specifications, and read weights are automatically assigned by the system according to instance specifications.
>
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click a primary instance ID to enter the instance management page.
2. On the instance management page, click the **Read-Only Instance** tab and click **Configure** in the **RO Group** column to enter the RO group configuration page.
![](https://main.qcloudimg.com/raw/3d3181b7bc09b6bc484e78a4e4011f0c.png)
3. On the RO group configuration page, configure the RO group and click **Submit**.
 - **Assign Read Weight**: The traffic of each read-only instance in an RO group will be automatically distributed according to its read weight, which can implement load balancing and reduce the difficulty in managing multiple read-only instance IP addresses. An RO group automatically assigns read weights to each read-only instance. The following table lists the read weights of read-only instances of different specifications:
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
    - If rebalancing is disabled, modifying weight will only affect new loads. The operation has no impact on read-only instances accessed by existing persistent connections and does not cause momentary database disconnections.
    - If rebalancing is enabled, when the configurations of read-only instances in the RO group are modified, all connections to the RO group will be disconnected, and new connections will be rebalanced according to instance weights.
![](https://main.qcloudimg.com/raw/45b4aacc78429c2cb47bf3a9c226cd22.png)

## Deleting RO Group
An RO group can be deleted if it has no read-only instances.
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click a primary instance ID to enter the instance management page.
2. On the instance management page, select the **Read-Only Instance** tab to view all RO groups. You can delete an RO group after confirming that there are no read-only instances in it.
![](https://main.qcloudimg.com/raw/f90e124d71f1ff3324d3dce408a68d46.png)
