## Instance Specifications
For more information on instance specifications supported by TencentDB for SQL Server and their prices, see [Product Pricing](https://www.tencentcloud.com/document/product/238/8294).

## Prerequisites
You can adjust the configuration of a TencentDB for SQL Server instance and its associated instances only when they are in running status and are not executing any tasks.

## Specification Adjustment Process
**Scaling**
After you adjust the configuration in the console, the system will determine whether to complete the adjustment by in-place scaling or data migration. The configuration adjustment process is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/49f03015ca1012cd1be81ca83e442425.png)

## Impact of Configuration Adjustment
### Single-item adjustment
Single-item adjustment refers to the adjustment of either the specification or disk, which has the following impact:
<table>
<tbody>
<tr><th>Instance Architecture</th><th>Disk Type</th><th>Adjustment Item</th><th>Adjustment Decision</th><th>Adjustment Impact</th><th>Time</th></tr>
<tr>
<td rowspan="1">Single-node instance (formerly basic edition)</td><td>Cloud disk</td>
<td>Specification upgrade <br>or<br> disk capacity expansion <br>or<br> specification downgrade</td><td>Upgrade and downgrade</td><td>1. The instance will be restarted during configuration adjustment. <br>2. The service will become unavailable for about 3 minutes. <br>3. Perform the adjustment during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>        
<tr>
<td rowspan="4">Two-node instance (formerly high-availability edition)</td>
<td rowspan="4">Local disk</td>
<td>Disk capacity reduction</td><td>Downgrade</td><td>1. The instance disk capacity will be reduced during the configuration adjustment. <br>2. Data migration and instance restart will not be performed, and no momentary disconnections will occur. <br>3. You can custom the effective time that is also the adjustment time without affecting the business. </td><td>You can select the time to take effect.</td></tr>
<tr>
<td>Specification downgrade</td><td>Downgrade</td><td>1. The instance specification will be downgraded during configuration adjustment. <br>2. The service will become unavailable for around 1 minute. <br>3. Perform the adjustment during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
<tr>
<td>Specification upgrade<br>or<br>disk capacity expansion</td><td>Migration and upgrade</td><td>1. Data migration will be involved during the instance configuration adjustment, and the larger the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration is completed, which causes a momentary disconnection from the database for few seconds. Make sure that your business has a reconnection mechanism. <br>3. Most database, account, and network operations are unavailable during the momentary disconnection. Therefore, we recommend that you perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
<tr>
<td>Specification upgrade <br>or<br> disk capacity expansion</td><td>Upgrade</td><td>1. The instance specification or disk capacity will be upgraded or expanded during configuration adjustment. <br>2. Data migration and instance restart will not be performed, and no momentary disconnections will occur. <br>3. You can customize the effective time that is also the adjustment time without affecting the business. </td><td>You can select the time to take effect.</td></tr>
<td rowspan="1">Two-node instances (formerly high-availability edition)</td><td rowspan="1">Cloud disk</td>
<td>Specification upgrade <br>or<br> disk capacity expansion<br>or<br>specification downgrade</td><td>Migration, upgrade, and downgrade</td><td>1. Data migration will be involved during the instance configuration adjustment, and the larger the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration is completed, which causes a momentary disconnection from the database for 30 seconds to 2 minutes. Make sure that your business has a reconnection mechanism. <br>3. Most database, account, and network operations are unavailable during the momentary disconnection. Therefore, we recommend that you perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
</tbody></table>	

### Combo adjustment
Combo adjustment refers to the adjustment of both the specification and disk capacity, which has the following impact:
<table>
<tbody>
<tr><th>Instance Architecture</th><th>Disk Type</th><th>Adjustment Item</th><th>Adjustment Decision</th><th>Adjustment Impact</th><th>Time</th></tr>
<tr>
<td rowspan="1">Single-node instance (formerly basic edition)</td><td>Cloud disk</td>
<td>Specification upgrade<br>Disk capacity expansion<br>Specification downgrade</td><td>Upgrade and downgrade</td><td>1. The instance will be restarted during configuration adjustment. <br>2. The service will become unavailable for around 3 minutes. <br>3. Perform the adjustment during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>        
<tr>
<td rowspan="6">Two-node instance (formerly high-availability edition)</td>
<td rowspan="6">Local disk</td>
<td>Specification upgrade + disk capacity expansion</td><td>Upgrade</td><td>1. The instance specification or disk capacity will be upgraded or expanded during configuration adjustment. <br>2. Data migration and instance restart will not be performed, and no momentary disconnections will occur. <br>3. You can custom the effective time that is also the adjustment time without affecting the business. </td><td>You can select the time to take effect.</td></tr>
<tr>
<td>Specification upgrade + disk capacity expansion</td><td>Migration and upgrade</td><td>1. Data migration will be involved during the instance configuration adjustment, and the larger the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration is completed, which causes a momentary disconnection from the database for few seconds. Make sure that your business has a reconnection mechanism. <br>3. Most database, account, and network operations are unavailable during the momentary disconnection. Therefore, we recommend you perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
<tr>
<td>Specification upgrade + disk capacity reduction</td><td>Upgrade and downgrade</td><td>1. The instance specification will be upgraded and the disk capacity will be reduced during configuration adjustment. <br>2. Data migration and instance restart will not be performed, and no momentary disconnections will occur. <br>3. The time to take effect (i.e., the time when the configuration adjustment will occur) can be customized without affecting the business.</td><td>The time to take effect can be customized.</td></tr>
<tr>
<td>Specification upgrade + disk capacity reduction</td><td>Migration, upgrade, and downgrade</td><td>1. Data migration will be involved during the instance configuration adjustment, and the larger the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration is completed, which causes a momentary disconnection from the database for few seconds. Make sure that your business has a reconnection mechanism. <br>3. Most database, account, and network operations are unavailable during the momentary disconnection. Therefore, we recommend you perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
</tr>
<td>Specification downgrade + disk capacity expansion</td><td>Upgrade and downgrade, or migration, upgrade, and downgrade</td><td>1. The service may become unavailable for around 1 minute, and data migration may be involved during the instance configuration adjustment, and the larger the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration is completed, which causes a momentary disconnection from the database for few seconds. Make sure that your business has a reconnection mechanism. <br>3. Most database, account, and network operations are unavailable during the momentary disconnection. Therefore, we recommend you perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
</tr>
<td>Specification downgrade + disk capacity reduction</td><td>Downgrade</td><td>1. The instance specification will be downgraded during configuration adjustment. <br>2. The service will become unavailable for around 1 minute. <br>3. Perform the adjustment during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
<tr>
<td rowspan="1">Two-node instance (formerly high-availability edition)</td>
<td rowspan="1">Cloud disk</td><td>Specification upgrade<br>Disk expansion<br>Specification downgrade</td><td>Migration, upgrade, and downgrade</td><td>1. Data migration will be involved during the instance configuration adjustment, and the larger the data volume, the longer the data migration time. Access to the instance will not be affected during this period. <br>2. A switch will be performed after migration is completed, which causes a momentary disconnection from the database for 30 seconds to 2 minutes. Make sure that your business has a reconnection mechanism. <br>3. Most database, account, and network operations are unavailable during the momentary disconnection. Therefore, we recommend that you perform the switch during off-peak hours. </td><td>You need to select the time to take effect.</td></tr>
</tbody></table>


## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select the region and target instance in the instance list, and click **Adjust Configuration** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/84f60eedd1e5492b31da602ef387b9f9.png)
2. In the **Adjust Configuration** window that pops up, select the desired CPU, memory, and disk capacity, and click **OK**.
>?
>- ?Select the **Time to Take Effect** of the configuration adjustment and click the orange note.
>  - During maintenance time: You can modify the maintenance time on the instance details page.
>  - Adjust now: The configuration adjustment will be performed immediately.
>- If disk capacity reduction is involved, in order to avoid failures, the new disk space must be greater than or equal to 2 times the currently used disk space.
>- If the instance to be adjusted is associated with other read-only instances and data migration is involved, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a7b802d9713230b55bbf5642d341facd.png)
3. For pay-as-you-go instances, click **Adjust** in the window.
4. You will be redirected to the instance list. When the instance status changes from **Switching (after configuration adjustment)** to **Running**, the specification upgrade is completed. You can query and check the new specification on the **Instance List** or **Instance Details** page.
