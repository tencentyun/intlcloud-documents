## Operation Scenarios
Dependent on the architecture of the TencentDB for MongoDB instance, instance restart divides into mongos restart and mongod restart. Restarting the instance will cause a momentary disconnection. Especially, when mongod is being restarted, if there are data writes, rollback may occur and lead to data loss.
During the restart, the TencentDB for MongoDB instance will not be able to provide services. Please make preparations in advance to avoid business interruption. Currently, the mongod restart feature is made available through an allowlist. If needed, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. Restart is a high-risk operation and should be handled with caution.

## Directions
1. Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and enter the replica set or shard instance list.
2. Select the instance to be restarted, click **Restart** at the top, or select **More** > **Restart** in the "Operation" column of the instance.
3. In the pop-up dialog box, select the components to be restarted, click **Confirm**, and wait for the task to complete.
