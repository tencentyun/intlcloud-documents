## Overview

The budget management feature is developed to meet the internal management needs of Tencent Cloud customers. It lets you configure, track, and analyze budgets to help control your costs.

>? The budget management feature is currently in beta test. To try it out, please contact your Tencent Cloud sales rep.
>

## Directions

1. Log in to the [Billing Center](https://console.cloud.tencent.com/expense/overview).
2. On the left sidebar, select **Cost Management > Budget Management** to enter the budget management page.
3. Click **New** to create a budget.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dwQ8962_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_3%E6%96%B0%E5%BB%BA%E9%A2%84%E7%AE%97.png)
4. In the **Edit budget** window, configure the following:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TuF7925_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_4%E7%BC%96%E8%BE%91%E9%A2%84%E7%AE%97.png)
 - **Basics**: Enter a name for the budget, which will be displayed in the budget list.
 - **Budget information**: 
    - **Budget period:** Select a yearly, quarterly, monthly, or daily period for the budget.
    - **Period type:** A budget can be effective for a specified period or effective indefinitely. If the budget is effective indefinitely, it will continue being effective with no end time defined.
>! 
> - If your budget is effective indefinitely, there is no limit to the number of budget period cycles. This type of budget **only supports fixed budgeting.**
> - For a planned budget, you can enter specific budget amounts for up to 12 budget periods. Any additional budget periods will have the same amount as the 12th period.
    - **Effective period:** Specify the period of time during which the budget will be effective. If you selected **Effective indefinitely**, no end time will be defined.
    - **Budgeting method:** Select **Fixed** or **Planned**.
    - **Budget amount:** Enter the amount of cost you plan to incur during each budget period. For a fixed budget, enter a fixed amount that is applied to every budget period. For a planned budget, enter a specific amount for each period.

 - **Budget scope**:
    - We recommend selecting **All billable items** (selected by default). 
    - You can also specify a **Custom** budget scope. Custom dimensions for defining a budget include product, subproduct, region, availability zone, billing mode, transaction type (consumption type), project, and tag. Under each dimension, you can select multiple criteria based on your past consumption records.

 - **Advanced settings**: You can select cost attributes to further refine your budget.
    - We recommend selecting **Consumption bills** for bill type and **Total amount after discounts** for spend type.
    For bill type, you can set the budget based on your standard bills or consumption bills. If you select consumption bills, you need to enable consumption bills first. The consumption bill type is usually used for managing amortized costs.
    - You can also select the spend type you want the budget to be based on. For example, you can configure your budget to be based on the original price of orders without discounts applied, or you can set a budget specifically to track your cash spend and voucher deductions. The available spend types are **total amount after discounts**, **original price**, **cash**, **voucher deduction**, **free credit**, and **commission**.

 - **Chart area**: The chart area displayed on the right shows your cost history to help you configure your budget more accurately.
    - The auxiliary chart shows Cost Explorer data, and the displayed costs correspond to your configured settings. You can also go directly to the **Cost Explorer** page for more detailed cost analysis.
    - It also shows your budget amount and the alerts you configure for the budget.

>? For a daily budget, spend history from the past 20 days is displayed. For a monthly budget, the past 12 months are displayed. For a quarterly budget, the past 4 quarters are displayed. For an annual budget, yearly data is displayed.
>

5. After filling in all the information, click **Next** to configure alerts.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/2dEz776_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_5%E8%AE%BE%E7%BD%AE%E6%8F%90%E9%86%92.png)
 - **Budget alerts**:
    - **Actual cost:** The alert is triggered based on the actual cost amount.
    - **Against fixed value:** The alert is triggered when a certain fixed amount is reached.
    - **Percentage of budgeted amount:** The alert is triggered when a certain percentage of your budget amount is reached.

 - **Fluctuation alert**: Fluctuation alerts are triggered when your daily or monthly costs increase by an abnormal amount, which is calculated based on the fluctuation type you select. You can set up to 3 fluctuation alerts.
    - For a daily budget period, the following fluctuation types are available: PoP (against yesterday); MoM (against same day last month); Daily comparison (against fixed value)
    - For a monthly or longer budget period, the following fluctuation types are available: PoP (against yesterday); MoM (against same day last month); PoP (against last month).
    - The following shows how each fluctuation type is calculated:

| Fluctuation Type | Calculation | Remarks |
|---------|---------|---------|
| PoP (against yesterday) | (Today’s amount – Yesterday’s amount) ÷ Number of previous periods × 100% | To avoid analysis being impacted due to larger monthly settlement fees that occur on the 1st of each month, the PoP (against yesterday) and MoM (against same day last month) fluctuation types do not cover monthly settlement fees. | 
| MoM | (Today’s amount – Amount on same day last month) ÷ Number of days last month × 100% |If the amount from the same day last month cannot be obtained (for example, if today is May 31 and there is no data from April 31) the system will calculate fluctuation based on the amount from the closest available day (April 30). |
| PoP (against last month) | (This month’s amount – Previous month’s amount) ÷ Previous month’s amount × 100% |
|Daily comparison | Today’s amount > Fixed amount |

>! For each budget, you can set up to three alert thresholds and up to three fluctuation alerts.
>

**Alert recipients**: To select alert recipients, go to the [Message Subscriptions](https://console.intl.cloud.tencent.com/message/subscription) page in the console and select **Financial Issues** > **Budget Management**, and click **Modify Message Recipient**.
 - If you edit a threshold amount after an alert has been triggered, the alert will be resent the next time the system checks the threshold status.
 - If multiple alerts are triggered simultaneously, the alerts will be combined into a single alert notification.
 - The same alert will only be triggered once per monitoring cycle.

6. Click **Next** to confirm the budget.
Review the budget information, alert thresholds, alert details, and other settings for your budget. If they are all correct, click **Save**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Degm890_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_6%E7%A1%AE%E8%AE%A4%E9%A2%84%E7%AE%97.png)

## Visual Analysis Panel
Click on a budget name in the budget list to enter the budget analysis panel to further analyze the historical performance of the selected budget. You can also edit, delete, or copy the budget.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ABFs816_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_%E5%8F%AF%E8%A7%86%E5%8C%96%E9%9D%A2%E6%9D%BF1.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QEjX852_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_%E5%8F%AF%E8%A7%86%E5%8C%96%E9%9D%A2%E6%9D%BF2.png)
- **Budget for the current period:** You can view information about the current period’s budget, including the amount of budget already spent, the budget amount compared to your actual costs, and the number of alerts triggered.
- **Budget history:** You can view the historical status of your budget since the time it was created. The chart shows Cost Explorer data so you can view your actual costs against your budget for each budget period. You can also go directly to **Cost Explorer** for further analysis or go to **Alert History** to view the history of triggered budget alerts, including the alert time and alert content.
- **Budget information:** On the right panel, you can view the settings for the selected budget. You can also edit, delete, or copy the budget.

>? To ensure your budget stays consistent and complete, if your budget changes, we recommend that you create a new budget instead of editing your existing budget.
