TencentDB for MongoDB supports quick adjustment of instance specification and provides flexible scaling operations. You can flexibly adjust the specifications of MongoDB instances according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

<span id="guize"></span>

## Configuration Rules
1. You can adjust the configuration of TencentDB for MongoDB instances and their associated instances only when they are under normal status (running) and are not executing any tasks.
2. You cannot cancel a configuration adjustment operation in progress.
3. The name, access IP and access port of an instance will not change after configuration adjustment.
4. **Data migration may be involved in configuration adjustment. During data migration, the TencentDB for MongoDB instance can be accessed normally and the business will not be affected.**
5. **Instance switchover may be needed after configuration adjustment is completed. It is recommended that applications be configured with auto reconnection feature, and that instance switchover be conducted during the instance maintenance period. For more information, see [Setting Instance Maintenance Period](https://cloud.tencent.com/document/product/240/19910)**.

## Adjusting Configurations

1. Log in to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb/), and go to the instance list.
2. Select the instance for which you want to adjust the configuration, and click **Adjust Configuration** in the **Operation** column.
   ![](https://main.qcloudimg.com/raw/6cb8aa962340d52960f73c10cd98b61d.png)
3. In the pop-up box, select the configuration you want to adjust to, and then click **OK**.

## Calculating Fees

### Upgrade instances
1. If you upgrade a monthly subscription database instance, the price difference between original and upgraded specifications is deducted from your account. If the account balance is insufficient, you need to top it up. After upgrade, the instance is billed by the new specification.
2. If the upgraded instance is a pay-as-you-go instance, it will be billed by the new specification in the next billing period.

### Degrade instances
1. If you degrade a monthly subscription database instance, the price difference is calculated according to the following formula:
 **Refund amount=Remaining amount for the original configuration - Purchase price of the new configuration**
Description:
 - **Remaining amount for the original configuration**: The amount obtained by **the effective order amount of the original configuration minus the consumed amount for the original configuration**.
 - **The effective order amount of the original configuration**: The amount paid for the order in effect, excluding discounts and vouchers.
 - **The consumed amount for the original configuration** is calculated based on the following rules:
    - For the consumed resources, if the application for degrading the configuration is submitted one month after the purchase, the monthly fees are deducted. If such application is submitted less than a month after the purchase, the fees for the actually consumed resources are deducted.
    - The consumed resources are calculated with an accuracy down to seconds.
 - **Purchase price of the new configuration**: The current official price of the new configuration x the remaining usage duration.

>!
> - **<font color="red">Rebates and vouchers are not returned.</font>**
> - **The refund amount** will be returned to your account **by the proportions of cash paid and voucher amount used for the purchase**.
> - If the refund amount is ≤0, it is considered 0, that is, the refund amount is 0.

2. If you degrade a pay-as-you-go database instance, it will then be billed by the **Tier 1 price for the new configuration**.


