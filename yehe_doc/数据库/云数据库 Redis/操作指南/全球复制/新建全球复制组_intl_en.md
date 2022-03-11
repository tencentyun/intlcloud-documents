TencentDB for Redis allows you to create a replication group in the console and add master or read-only instances to it, so as to implement consistent data sync in a one-master or multi-master architecture within the replication group. 

>?To use the global replication feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

## Concepts
- **Instance role:** You need to assign different roles to instances in a replication group, including **master instance** and **read-only instance**.
  - **Master instance:** It provides data read/write access and is used to write the business data.
  - **Read-only instance:** It provides the data read-only access and is used for read-only data operations or disaster recovery.
- **IP address:** Each instance in a replication group has a separate IP address, which can be accessed independently.
- **Master/Replica switch:** Automatic failover can be performed between master and replica nodes in each instance. However, it is not supported between master and read-only instances.

## Version Description
- Global replication supports only 4.0 Standard Architecture, 4.0 Cluster Architecture, 5.0 Standard Architecture, and 5.0 Cluster Architecture instances.
- The current version of the global replication feature supports only instances deployed in the same AZ. Multi-AZ instances will be supported in the future.

## Notes
### Specification limits
- An instance running on cluster architecture can have up to 64 shards in a global replication group.
- When creating a replication group, you must specify the master instance in the group.
- Currently, you can add up to four instances in a global replication group in the following deployment schemes: one master and three read-only instances, four master instances, or two master and two read-only instances.

### Region limits
The global replication feature can replicate data in the same AZ or across AZs between any Tencent Cloud regions no matter where instances in the replication group are deployed.
Currently, only the following regions and AZs support global replication:

| Region | AZ |
|---------|---------|
| Virginia | Virginia Zone 2 |
| Beijing | Beijing Zone 5 |
| Shanghai | Shanghai Zone 5 |
| Hong Kong (China) | Hong Kong Zone 3 |
| Guangzhou | Guangzhou Zone 6 |
| Singapore | Singapore Zone 2 |
| Nanjing | Nanjing Zone 3 |

### Command description
- The **FLUSHDB** or **FLUSHALL** command will be synced to all instances in the replication group. Therefore, run them with caution.
- The **Pub** and **Sub** command group will not be synced. We recommend you use the `Stream` data structure to replicate notification messages across regions.
- When the **RESTORE** command is synced, if the target subinstance has the same key, it will not be executed.

## Billing Description
- If instances in a replication group are in the same region, no additional fees will be incurred.
- For cross-region data replication within a replication group, bandwidth fees will be incurred. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/553/35174).

## Creating Global Replication Group
### Prerequisites
- You have [created a TencentDB for Redis instance](https://intl.cloud.tencent.com/document/product/239/37712), and the instance is in **Running** status.
- The data in the master TencentDB for Redis instance in the replication group has been cleared. 

### Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Select **Global Replication** on the left sidebar.
3. On the **Redis - Global Replication** page on the right, click **Create Replication Group**.
4. In the **Create Replication Group** pop-up window, configure the following parameters and click **OK**.
<table width="100">
<thead><tr><th width="15%">Parameter</th><th width="55%">Description</th><th width="15%">Required</th><th width="15%">Sample Value</th></tr></thead>
<tbody>
<tr>
<td>Name</td>
<td>Name of the replication group to be created. Enter a name as prompted.</td>
<td>Yes</td>
<td>test</td></tr>
<tr>
<td>Remarks</td>    
<td>Brief description of the replication group. You can enter any characters to distinguish the group from others.</td>
<td>No</td>
<td>Replication group creation test</td></tr>
<tr>
<td>Master Instance Region</td> 
<td>Select the region of the master instance in the replication group.</td>
<td>Yes</td>
<td>Guangzhou</td></tr>
<tr>
<td>Select Master Instance</td> 
<td>Select the master instance in the replication group, which must have no data. The version, architecture, and memory capacity of the selected instance will be displayed, and you need to confirm whether the specification meets your requirements.</td>
<td>Yes</td>
<td>test-XXX</td></tr>
</tbody></table>
> !The Redis kernel of the master instance specified during replication group creation must be upgraded to the Global Replication Edition. After the upgrade is completed, one or multiple momentary disconnections lasting 5 seconds will occur.
> 
5. Return to the **Redis - Global Replication** page, and you can see the newly created replication group in the replication group list.
Click <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> before the name of the replication group to show its instance list, where you can view the status of the master instance. You can use the master instance after the system upgrades its kernel to the Global Replication edition.
![](https://qcloudimg.tencent-cloud.cn/raw/9a49f26745b61d2ab3315e86631da150.png)

## Adding Instance to Replication Group
After creating a replication group, you can add instances in the same or different regions and assign master and read-only instance roles to the added instances as needed to implement data sync.

### Notes
- Currently, you cannot add multi-AZ instances to a replication group. This will be supported in the future, so stay tuned.
- You can add up to **four** instances to a replication group. Such instances must have no data; otherwise, they cannot be added. Adding instances with existing data will be supported in the future.
- An instance newly added to a replication group will sync data from the master instance node, and it cannot be manipulated or accessed before the full data is synced.
- Once an instance is added to a replication group, its kernel edition will be upgraded, and one or multiple momentary disconnections will occur after the upgrade.

### Prerequisites
- You have created a global replication group, and it is in **Running** status.
- You have created an instance to be added to the replication group. Its compatible Redis version and architecture must be the same as those of the master instance specified during replication group creation, its memory capacity must be greater than or equal to the used capacity of the master instance, and it must be in **Running** status.
- If you want to specify the instance to be added as a master instance, it must have at least two replica nodes.
- You must clear the data in the instance to be added to the replication group no matter whether it will be added as a master or read-only instance.

### Directions
1. In the [instance list](https://console.cloud.tencent.com/redis/replication) on the **Redis - Global Replication** page, select the target replication group.
2. In the **Operation** column of the replication group, click **Add Instance**.
3. In the **Add Instance** pop-up window, read the notes carefully, configure the following parameters, and click **OK**.
  - **Region**: Select the region of the target instance.
  - **Select Instance**: Select the target instance.
  - **Instance Role**: Assign a role (**master instance** or **read-only instance**) to the target instance.
> ? The instance role is not limited when you add an instance to a replication group. Set the role to master or read-only instance as needed.
> 
4. Return to the **Redis - Global Replication** page. In the replication group list, click <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> before the name of the target replication group to show its instance list, where you can see the newly added instance.
![](https://qcloudimg.tencent-cloud.cn/raw/9a49f26745b61d2ab3315e86631da150.png)
You can add multiple instances to a replication group as needed and then sync data between them.

## Notes on Availability
### Cross-region disaster recovery
A master instance and a read-only instance can be added to a replication group to set up a cross-region disaster recovery system. However, the system will not automatically perform failover, which can only be manually performed in the console or through TencentCloud API. For detailed directions, see [Switching Instance Role](https://intl.cloud.tencent.com/document/product/239/45604).

### Replication exceptions
No matter whether a replication group has one or multiple master instances, when replication is interrupted, the system will not set them as read-only instances or perform other operations; instead, it will automatically resume the replay of incremental logs after instance recovery. We recommend you configure alarms for replication exceptions and set master instances as read-only instances when a replication exception such as replication interruption occurs, so as to guarantee the data consistency.

