TencentDB for MongoDB supports quick instance specification adjustment and flexible scaling operations. You can adjust MongoDB instance specifications based on your circumstances, such as during initial stage, rapid development stage, peak hours, and off-peak hours, for better resources and costs usage.

<span id="guize"></span>

## Configuration Rules
1. You can adjust the configuration of TencentDB for MongoDB instances and their associated instances only when they are under normal status (running) and are not executing any tasks.
2. You cannot cancel a configuration adjustment in progress.
3. The name, access IP and access port of an instance remain the same.
4. **Data migration may happen during configuration adjustment. When data is migrated, you can access the TencentDB for MongoDB instance as normal and your business will not be affected.**
5. **Instance switchover may be needed after configuration adjustment is completed. We recommended you enable auto reconnection for your applications, and switchover your instances during the maintenance period. For more information, see [Setting Instance Maintenance Period](https://cloud.tencent.com/document/product/240/19910)**.

## Adjusting Configurations

1. Log in to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb/), and go to the instance list.
2. Select the instance for which you want to adjust the configuration, and click **Adjust Configuration** in the **Operation** column.
   ![](https://main.qcloudimg.com/raw/6cb8aa962340d52960f73c10cd98b61d.png)
3. In the pop-up box, select the configuration you want to adjust to, and then click **OK**.

## Calculating Fees

### Upgrading instances
1.You can upgrade a prepaid (monthly/yearly subscription) database instance, and you would be charged for the price difference between your current plan and the plan to which you'd like to upgrade. If the account balance is insufficient, you need to top it up. After upgrade, the instance is billed by the new specification rate.
2. You can upgraded a pay-as-you-go instance, and the account will switch to the new plan when the current billing month finishes.
### Downgrading instances
1. You can downgrade a prepaid (monthly/yearly subscription) database instance. The price difference is calculated based on the following formula:
**Refund = Remainder of your current configuration charge - Price of the new configuration**

Description:
- **Remainder of your current configuration charge**: **Total capacity of the original configuration - Used capacity**.
- **Total capacity of the original configuration**: The cash you paid, excluding discounts and vouchers.
- **Used capacity** is calculated based on the following rules:
- You would be charged for one-month usage if you downgrade your plan upon the end of a billing cycle. You would be responsible to pay for what you use. 
- The used capacity is calculated with an accuracy down to seconds.
- **Charge for the new configuration**: The current official price of the new configuration x the remaining usage duration.
>!
> - **Rebates and vouchers are not refunded.**
> - **The refund** will go back to your account **as the proportions of cash paid and voucher amount used for the purchase**.
> - The refund is considered as $0 when it is less or equal to $0.

2. If you are downgrading a pay-as-you-go database instance, you will be charged by the **Tier 1 price for the new configuration**.
