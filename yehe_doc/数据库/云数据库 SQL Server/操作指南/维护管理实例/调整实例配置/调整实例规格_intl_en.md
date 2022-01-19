This document describes how to adjust the instance specification in the TencentDB for SQL Server console.

## Instance Specification
For more information on instance specifications supported by TencentDB for SQL Server and their prices, see [Product Pricing](https://intl.cloud.tencent.com/document/product/238/8294).

## Prerequisites
You can adjust the configuration of a TencentDB for SQL Server instance and its associated instances only when they are in normal status (Running) and are not executing any tasks.

## Specification Adjustment Process
**Scaling**
After you adjust the configuration in the console, the system will decide to complete the change by scaling or data migration. The configuration adjustment process is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/49f03015ca1012cd1be81ca83e442425.png)

## Impact of Configuration Adjustment
### Single-Item adjustment
Single-Item adjustment refers to the adjustment of either the specification or disk, which has the following impact:
<table>
<tbody>
<tr><th width=12%>Edition</th><th width=12%>Adjustment Item</th><th width=12%>Adjustment Decision</th><th>Adjustment Impact</th><th width=19%>Time</th></tr>
<tr>
<td rowspan="1">Basic Edition</td>
<td>Specification upgrade<br>or<br>Disk capacity expansion<br>or<br>Specification downgrade</td><td>Upgrade and downgrade</td><td>1. The instance will be restarted during configuration adjustment. <br>2. The service will become unavailable for around 3 minutes. <br>3. Perform the adjustment during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>        
<tr>
<td rowspan="4">High-Availability Edition/Cluster Edition</td>
<td>Disk capacity reduction</td><td>Downgrade</td><td>1. The instance disk capacity will be reduced during the configuration adjustment. <br>2. Data migration and instance restart will not be performed, and no momentary disconnections will occur. <br>3. The submitted adjustment will take effect immediately without affecting the business. </td><td>The submitted adjustment will be executed immediately.</td></tr>
<tr>
<td>Specification downgrade</td><td>Downgrade</td><td>1. The instance specification will be downgraded during configuration adjustment. <br>2. The service will become unavailable for around 1 minute. <br>3. Perform the adjustment during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
<tr>
<td>Specification upgrade<br>or<br>disk capacity expansion</td><td>Migration and upgrade</td><td>1. Data migration will be involved during the instance configuration adjustment, and the higher the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration completion, which is accompanied by a disconnection from the database lasting for just seconds. Make sure that your business has a reconnection mechanism. <br>3. During the momentary disconnection, most operations related to databases, accounts, and networks cannot be executed. Therefore, be sure to perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
<tr>
<td>Specification upgrade<br>or<br>disk capacity expansion</td><td>Upgrade</td><td>1. The instance specification or disk capacity will be upgraded or expanded during configuration adjustment. <br>2. Data migration and instance restart will not be performed, and no momentary disconnections will occur. <br>3. The submitted adjustment will take effect immediately without affecting the business. </td><td>The submitted adjustment will be executed immediately.</td></tr>
</tbody></table>

### Combo adjustment
Combo adjustment refers to the adjustment of both the specification and disk capacity, which has the following impact:
<table>
<tbody>
<tr><th width=12%>Edition</th><th width=12%>Adjustment Item</th><th width=12%>Adjustment Decision</th><th>Adjustment Impact</th><th width=19%>Time</th></tr>
<tr>
<td rowspan="1">Basic Edition</td>
<td>Specification upgrade<br>Disk capacity expansion<br>Specification downgrade</td><td>Upgrade and downgrade</td><td>1. The instance will be restarted during configuration adjustment. <br>2. The service will become unavailable for around 3 minutes. <br>3. Perform the adjustment during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>        
<tr>
<td rowspan="6">High-Availability Edition/Cluster Edition</td>
<td>Specification upgrade + disk capacity expansion</td><td>Upgrade</td><td>1. The instance specification or disk capacity will be upgraded or expanded during configuration adjustment. <br>2. Data migration and instance restart will not be performed, and no momentary disconnections will occur. <br>3. The submitted adjustment will take effect immediately without affecting the business. </td><td>The submitted adjustment will be executed immediately.</td></tr>
<tr>
<td>Specification upgrade + disk capacity expansion</td><td>Migration and upgrade</td><td>1. Data migration will be involved during the instance configuration adjustment, and the higher the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration completion, which is accompanied by a disconnection from the database lasting for just seconds. Make sure that your business has a reconnection mechanism. <br>3. During the momentary disconnection, most operations related to databases, accounts, and networks cannot be executed. Therefore, be sure to perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
<tr>
<td>Specification upgrade + disk capacity reduction</td><td>Upgrade and downgrade</td><td>1. The instance specification will be upgraded and the disk capacity will be reduced during configuration adjustment. <br>2. Data migration and instance restart will not be performed, and no momentary disconnections will occur. <br>3. The submitted adjustment will take effect immediately without affecting the business. </td><td>The submitted adjustment will be executed immediately.</td></tr>
<tr>
<td>Specification upgrade + disk capacity reduction</td><td>Migration, upgrade, and downgrade</td><td>1. Data migration will be involved during the instance configuration adjustment, and the higher the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration completion, which is accompanied by a disconnection from the database lasting for just seconds. Make sure that your business has a reconnection mechanism. <br>3. During the momentary disconnection, most operations related to databases, accounts, and networks cannot be executed. Therefore, be sure to perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
</tr>
<td>Specification downgrade + disk capacity expansion</td><td>Upgrade and downgrade, or migration, upgrade, and downgrade</td><td>1. The service may become unavailable for around 1 minute, and data migration may be involved during the instance configuration adjustment, and the higher the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration completion, which is accompanied by a disconnection from the database lasting for just seconds. Make sure that your business has a reconnection mechanism. <br>3. During the momentary disconnection, most operations related to databases, accounts, and networks cannot be executed. Therefore, be sure to perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
</tr>
<td>Specification downgrade + disk capacity reduction</td><td>Downgrade</td><td>1. The instance specification will be downgraded during configuration adjustment. <br>2. The service will become unavailable for around 1 minute. <br>3. Perform the adjustment during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
</tbody></table>

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select the region and target instance in the instance list, and click **Adjust Configuration** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/84f60eedd1e5492b31da602ef387b9f9.png)
2. In the **Adjust Configuration** window that pops up, select the desired CPU, memory, and disk capacity, and click **Confirm**.
>?
>- ?Select the **Time to Take Effect** of the configuration adjustment and click the orange note.
>  - During maintenance time: you can modify the maintenance time on the instance details page.
>  - Adjust now: the configuration adjustment will be performed immediately.
>- If disk capacity reduction is involved, in order to avoid failures, the new disk space must be greater than or equal to 2 times the currently used disk space.
>- If the instance to be adjusted is associated with other instances (read-only instances) and data migration is involved, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a7b802d9713230b55bbf5642d341facd.png)
3. On the payment page you are redirected to, confirm the configuration information and fees and click **Submit Order**.
4. You will be redirected to the instance list. When the instance status changes from **Switching (after configuration adjustment)** to **Running**, the specification upgrade is completed. You can query and check the new specification on the **Instance List** or **Instance Details** page.


