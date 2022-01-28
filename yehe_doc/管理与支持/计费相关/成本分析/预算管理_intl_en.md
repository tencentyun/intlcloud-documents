## Overview

This feature helps you manage budgets for Tencent Cloud products. You can create different budget alerts for monthly/quarterly/annual spends. When your spend exceeds an alert threshold, alert notifications will be sent to you.

>? The budget management feature is currently in beta test. To try it out, contact your Tencent Cloud rep.
>

## Directions

1. Log in to the [Billing Center](https://console.cloud.tencent.com/expense/overview).
2. On the left sidebar, select **Cost Analysis > Budget Management** to enter the budget management page.
3. Click **New**.
![](https://qcloudimg.tencent-cloud.cn/raw/fedadab6f2eb475bb1913cf8214a81b0.png)
4. Perform the following operations:
 1. Set the following budget information:
![](https://qcloudimg.tencent-cloud.cn/raw/fd92af55324b288cc08361ba59a0a142.png)
    - Budget Name: enter a budget name, which will be displayed in the budget list.
    - Budget Period: select a budget period. Calendar month/quarter/year is used. For example, Q1 is from January to March.
    - Effective: set the time period during which the budget will be effective.
    - Budget Amount Type:
       - Fixed: during the validity period, the budget amount is the same in each period.
       - Variable: during the validity period, the budget amount can be customized in each period.
    - Monthly/Quarterly/Annual Budget Amount:
       - If you select **Fixed**, enter a fixed value.
       - If you select **Variable**, enter the alert threshold value for each month, quarter, or year.
       - Auto Fill: select **Auto Fill**, set the starting budget and expected growth, and click **Confirm** to automatically enter the monthly/quarterly/annual budget amount. You can set only one starting budget amount and growth rate.
   ![](https://qcloudimg.tencent-cloud.cn/raw/52967d94fd515381e613379caa59b4a4.png)
>!Expected growth rate refers to the percentage you expect the budget amount to increase from the previous period.
>
 2. Set the budget scope.
    ![](https://qcloudimg.tencent-cloud.cn/raw/1a6e48d5a7955ef7f9d745250b7ae580.png)
    - The budget is applicable to all products by default. You can also apply it and its alert settings to one or more specific products.
    - The budget is applicable to all billing modes by default. You can also apply it and its alert settings to pay-as-you-go or monthly subscription only.
 3. Set alert thresholds. You can customize up to 3 alert thresholds for each budget.
    ![](https://qcloudimg.tencent-cloud.cn/raw/8a22a14da57ac3bbdadd82e47e3ca28b.png)
    - Actual spend: Alerts are triggered based on your actual spend.
    - Absolute value: Alerts are triggered when an absolute value is exceeded.
    - Percentage of budgeted amount: An amount threshold is calculated based on the specified percentage of budgeted amount, and alerts will be triggered when the amount is exceeded. If the budgeted amounts vary with month, the amount threshold changes accordingly.
5. Click **Save**.
You can perform the following operations on the budget management page:
 - View: view created budgets.
 - Edit: modify existing budgets.
 - Delete: delete a budget or batch delete multiple budgets.

## Alert Notification

- Alert channel: You can choose to receive alert notifications via email, SMS, or Message Center. Make sure that the recipient you select has a verified email address and mobile number.
- Alert effective time: After an alert is configured, it will take effect at 9:00 the next day. For example, if an alert is set on December 9, we will check at 9:00 on December 10 to determine whether an alert threshold is exceeded. If it is, alert notifications will be sent on December 10.
