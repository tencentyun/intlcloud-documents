## Operation Scenarios
Dependent on the architecture of the TencentDB for MongoDB instance, instance restart divides into mongos restart and mongod restart. Restarting the instance will cause a momentary disconnection. Especially, when mongod is being restarted, if there are data writes, rollback may occur and lead to data loss.
During the restart, the TencentDB for MongoDB instance will not be able to provide services. Please make preparations in advance to avoid business interruption. Currently, the mongod restart feature is made available through an allowlist. If needed, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. Restart is a high-risk operation and should be handled with caution.

## Directions
1. Log in to the [MongoDB Console](https://console.cloud.tencent.com/mongodb). In the instance list, select the desired instance and click **Restart** at the top or click **More** > **Restart** in the "Operation" column.
 ![](https://main.qcloudimg.com/raw/5e704dbdbc5ab151bac6b57856a5f5e0.jpg)
2. In the pop-up dialog box, select the components to be restarted, click **OK**, and wait for the task to complete.
