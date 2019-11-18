## Operation Scenario
TencentDB for MySQL supports quick adjustment of instance specification and allows flexible scaling operations. You can elastically adjust the specifications of MySQL instances according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

<span id="guize"></span>

## Configuration Adjustment Rules
- You can adjust the configuration of a TencentDB for MySQL instance and its associated instances only when they are in normal status (running) and are not executing any tasks.
- You cannot cancel a configuration adjustment operation in progress.
- The name, access IP, and access port of an instance will remain the same after configuration adjustment.
- Data migration may be involved in configuration adjustment. During data migration, the TencentDB for MySQL instance can be accessed normally and the business will not be affected.
- Instance switchover may be needed after configuration adjustment is completed (i.e., the MySQL instance may be disconnected for seconds). It is recommended that applications be configured with auto reconnection feature and that instance switchover be conducted during the instance maintenance period. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/236/10929).
- During configuration adjustment, you should try to avoid such operations as modifying MySQL's global parameters and user password.

## Directions
### Adjusting the Instance Configuration in the Console
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. Select the instance to be adjusted in the instance list and select **More** > **Adjust Configuration** in the "Action" column.
![](https://main.qcloudimg.com/raw/bddf4d9354753da23a0730fb91e01227.png)
3. In the pop-up dialog box, select the desired configuration and click **Submit**.
 - Pay-as-you-go instance:
![](https://main.qcloudimg.com/raw/fd7b5ead8e0aaeaa89248dcf12f58c02.png)

### Adjusting the Instance Configuration through the API
You can upgrade the instance configuration using the UpgradeDBInstance API. For more information, see [Upgrading a TencentDB Instance](http://intl.cloud.tencent.com/document/product/236/15876).
> Degrading the instance configuration through API is unavailable for the time being. You can do so in the console if needed.
