
The [spend analysis](https://console.cloud.tencent.com/expense/cost/analysis) feature helps you better manage your spend on Tencent Cloud resources. In spend analysis, you can view your spend trends by multiple dimensions, including monthly (last 12 months) and daily (last 6 months).

![](https://main.qcloudimg.com/raw/76c5fbd0294f5b952f25242ff3ec2d15.png)

>!
> - Spend data has a delay of 2 days. It can be used for cost analysis and budget planning, but not for settlement or reconciliation.
> - Daily spend includes your actual spend on monthly subscription and pay-as-you-go resources. Assume that you pay 120 USD for a 12-month subscription of a CVM. The 120 USD will be entirely counted into the spend of the day of purchase.
> - The spend data on this page and in the notifications we send to you is estimation and may differ from your actual spend. It only covers your spend until the date you view the page.
> - The chart displays the top 10 projects by spend, and the rest are aggregated into "Others". You can export the data to view the spend of all projects.
> - The spend analysis feature is currently in beta test. To try it out, contact your Tencent Cloud rep.
> 

## Spend Overview

You can view your daily spend trends in the last 6 months and monthly trends in the last 12 months.
![](https://qcloudimg.tencent-cloud.cn/raw/66cdb23196597a357e6b2ef07e371d8a.png)
- Categorize By: view your spend trends by multiple dimensions, including the default dimension, product, billing mode, subproduct, project, region, AZ, and transaction type
- Spend Type: total spend, cash payment, complimentary cash, and vouchers
- Granularity: view daily or monthly spend in a specified time period
- Chart Type: stacked/clustered bar chart and line chart
- Advanced Filters:
 - You can expand and collapse the filter panel.
 - Filter conditions: product, subproduct, project, region, AZ, billing mode, and transaction type
 - After you click **Advanced Filters** to expand the filter panel, click a **condition** (such as product), select products, and click **Filter** to display the list of all purchased products.
![](https://qcloudimg.tencent-cloud.cn/raw/1fc791f0eeb5b0c951f02f2ebe4cb632.png)
 - You can view all (default) or use **Include only** and **Exclude only** to filter the results.
 ![](https://qcloudimg.tencent-cloud.cn/raw/ea0b70356c6b315628d4922314322880.png)
 - Click **Clear All** to clear all selected conditions.

## Spend Details

You can preview or download the data of a selected time period.
![](https://main.qcloudimg.com/raw/c4c74043abca4d523541e9778c689313.png)

## Alert Settings

You can set different alerts. When your spend exceeds an alert threshold, an alert notification will be sent two days later at 10:00 am. If multiple alerts are triggered, they will be merged into one SMS message or email.

![](https://main.qcloudimg.com/raw/33edbac4cae613273280a520af249290.png)

#### Creating alert

1. Click **New**.
>? You can add up to three thresholds for an alert, which will be triggered if any of the thresholds is exceeded.
>
![](https://main.qcloudimg.com/raw/7f2d9359a6d7ab37924ae5f53db06b2e.png)
2. In the pop-up window, configure the alert as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/e4d1bc2213c710dd7f0f55e9236f2baa.png)
Two alert types are supported: daily data alert and monthly data alert.
 - Daily data alert has three modes: day-over-day, month-over-month, and fixed value (compare your daily spend against a fixed value).
 Daily data alert formulas:
    - MoM = ABS ((Daily spend this month − Spend on the same day last month) / Spend on the same day last month × 100%)
    - DoD = ABS ((Daily spend on a day − Spend on the previous day) / Spend on the previous day × 100%)
    - Fixed value = Compare spend on a day against a fixed value
 - Monthly data alert has two modes: month-over-month and fixed value (compare your monthly spend against a fixed value).
 Monthly data alert formulas:
    - MoM = ABS ((Spend this month - Spend last month) / Spend last month × 100%)
For example, on August 18, spend in the current month is your total spend between August 1 and August 16, which is compared against your spend between July 1 and July 16.
    - Fixed value = Compare spend in the current month against a fixed value
   - You can configure alert notifications by product and billing mode.
   Product: All purchased products of the current user are displayed. The logic of the billing mode is similar.
3. Click **Save**.


#### Modifying alert settings

You can click **Edit** to modify the alert settings as needed.
![](https://main.qcloudimg.com/raw/846b0e69752bb7bb068380ec4ede7b8f.png)

#### Deleting alert or batch deleting alerts

You can click **Delete** to delete an alert or select multiple alerts and click **Delete** at the top of the page to batch delete them.
![](https://main.qcloudimg.com/raw/a9415d98fa89067093c73010d0a0a2e5.png)


## Subscribing to Spend Analysis Alert

1. Go to the [Message Subscription](https://console.cloud.tencent.com/messageCenter/messageConfig) page, find **Billing Center**, and click **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/0d2cd118b9e28fb06875e2b626ad5f5b.png)
2. In the pop-up window, find **Financial Issues** > **Spend Alerts**, and click **Modify Message Recipient**.
![](https://qcloudimg.tencent-cloud.cn/raw/13101ee0b208ba6b920957dcd4c27dcd.png)
>? The spend analysis feature supports two alert channels: SMS and email.
>
3. In the pop-up window, modify the recipient (the default recipient is the creator) and click **Confirm**.

## Viewing Permissions of Different User Types

1. The spend analysis overview and details of the root account can be viewed by the root account and its sub-accounts (sub-users/collaborators) if the root account has enabled the spend analysis feature.
2. The spend analysis overview and details of the root account cannot be viewed by the root account or its sub-accounts (sub-users/collaborators) if the root account hasn’t enabled the spend analysis feature.






