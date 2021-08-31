TencentDB for MongoDB supports quick adjustment of instance specification and allows flexible scaling operations. You can elastically adjust the specifications of TencentDB for MongoDB instances according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

<span id="guize"></span>
## Configuration Rules
1. You can adjust the configuration of a TencentDB for MongoDB instance and its associated instances only when they are in normal status (running) and are not executing any tasks.
2. You cannot cancel a configuration adjustment operation in progress.
3. The name, access IP, and access port of an instance will remain the same after configuration adjustment.
4. Data migration may be involved in configuration adjustment. During data migration, the TencentDB for MongoDB instance can be accessed normally, and the business will not be affected.
5. Instance switch may be needed after configuration adjustment is completed. It is recommended that applications be configured with auto reconnection feature and that instance switch be conducted during instance maintenance window. For more information, please see [Setting Instance Maintenance Time](https://intl.cloud.tencent.com/document/product/240/31190).

## Configuration Adjustment
1. Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb/) select the target region in the instance list.
2. Select the instance for which you want to adjust the configuration in the instance list and click **Adjust Configuration** in the "Operation" column.
3. On the pop-up page, select the configuration you want to adjust to and click **Confirm**.

## Fees Calculation
### Upgrading instance
1. After upgrade, pay-as-you-go instances will be billed based on the new instance specifications starting from the next billing cycle.

### Degrading instance

2. If you choose to degrade a pay-as-you-go instance, it will be billed at the tier 1 pay-as-you-go price for the new configuration.
