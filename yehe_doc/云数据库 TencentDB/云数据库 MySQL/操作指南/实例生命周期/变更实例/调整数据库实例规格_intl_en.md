
## Overview
TencentDB for MySQL supports quick adjustment of instance specification and allows flexible scaling operations. You can elastically adjust the specifications of MySQL instances according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization. For details on instance adjustment fees, please see [Instance Adjustment Fee](https://intl.cloud.tencent.com/document/product/236/32345).

#### Instance disk space description
- To ensure business continuity, upgrade your instance specifications or purchase additional disk capacity in time before disk capacity is used up.
>?You can view disk space on the instance details page in the [MySQL Console](https://console.cloud.tencent.com/cdb), or receive disk alarms with the [Alarming Feature](https://intl.cloud.tencent.com/document/product/236/8457).
- When the size of the data stored on an instance exceeds its capacity limit, the instance will be locked and become read-only. You will not be able to write data to it. You will need to expand its capacity or delete some database tables in the console to unlock it.
- To avoid the database from triggering the lock status repeatedly, a locked instance will be unlocked and allowed for reads and writes only when its remaining available capacity accounts for more than 20% of its total capacity or over 50 GB.

<span id="guize"></span>
## Configuration Adjustment Rules
- You can adjust the configuration of a TencentDB for MySQL instance and its associated instances only when they are in normal status (running) and are not executing any tasks.
- You cannot cancel a configuration adjustment operation in progress.
- The name, access IP, and access port of an instance will remain the same after configuration adjustment.
- Data migration may be involved in configuration adjustment. During data migration, the TencentDB for MySQL instance can be accessed normally and the business will not be affected.
- Instance switchover may be needed after configuration adjustment is completed (i.e., the MySQL instance may be disconnected for seconds). It is recommended that applications be configured with auto reconnection feature and that instance switchover be conducted during the instance maintenance period. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/236/10929).
- During configuration adjustment, you should try to avoid such operations as modifying MySQL's global parameters and user password.

## Directions
### Adjusting the instance configuration in the console
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb), find the desired instance in the instance list, and select **More** > **Adjust Configurations** in the "Operation" column.
![](https://main.qcloudimg.com/raw/bddf4d9354753da23a0730fb91e01227.png)
2. In the pop-up dialog box, select the desired configuration and click **Submit**.
 - Pay-as-you-go instance:
![](https://main.qcloudimg.com/raw/fd7b5ead8e0aaeaa89248dcf12f58c02.png)

### Adjusting the instance configuration through the API
You can upgrade the instance configuration using the `UpgradeDBInstance` API. For more information, see [UpgradeDBInstance](https://intl.cloud.tencent.com/document/product/236/15876).
>?Downgrading the instance configuration through API is unavailable for the time being. You can do so in the console if needed.
