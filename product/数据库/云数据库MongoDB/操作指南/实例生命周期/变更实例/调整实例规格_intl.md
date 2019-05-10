TencentDB for MongoDB supports quick instance specification adjustment and flexible scaling operations. You can adjust MongoDB instance specifications based on your differing business needs, such as during initial stage, rapid development stage, peak hours, and off-peak hours, to achieve better resource management and cost optimization.

<span id="guize"></span>

## Configuration Rules
1. You can adjust the configuration of TencentDB for MongoDB instances and their associated instances only when they are under normal status (running) and are not executing any tasks.
2. You cannot cancel a configuration adjustment in progress.
3. The name, access IP and access port of an instance remain the same.
4. **Data migration may happen during configuration adjustment. When data is migrated, you can access the TencentDB for MongoDB instance as normal and your business will not be affected.**
5. **Instance switchover may be needed after completing configuration adjustment. We recommend enabling auto reconnection for your applications, and strongly recommend scheduling instance switchover during the maintenance period. For more information, see [Setting Instance Maintenance Period](https://cloud.tencent.com/document/product/240/19910)**.

## Adjusting Configurations

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb/), and go to the instance list.
2. Select the instance for which you want to adjust the configuration, and click **Adjust Configuration** in the **Operation** column.
   ![](https://main.qcloudimg.com/raw/6cb8aa962340d52960f73c10cd98b61d.png)
3. In the pop-up box, select the configuration you want to adjust to, and then click **OK**.

## Calculating Fees

### Upgrading instances
You can upgrade a pay-as-you-go instance. The account will switch to the new plan when the current billing cycle ends.
### Downgrading instances
When you downgrade a pay-as-you-go database instance, the system will calculate your bill according to the **Tier 1 price for the new configuration**.
