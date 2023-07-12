## Overview
You can view the fees incurred by the use of COS under your account in the Billing Center in the Tencent Cloud console.


>!
>- COS bills are settled in the order of **free tier > pay-as-you-go billing**.
> - By default, the system uses the pay-as-you-go billing mode for settlement; that is, the system will deduct the free tier (if any) first and then bill the excessive usage in a pay-as-you-go manner.
> - For more information on the free tier and billable items, see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240) and [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) respectively.



## Viewing Bills by Instance/Bill Details


You can view bills by instance and bill details in the [Billing Center](https://console.cloud.tencent.com/expense/overview) in the console.

- Bill by instance: It displays the bill amount by resource ID, which is the same as the bill by instance (L2) file. For more information, see [Bill Management](https://www.tencentcloud.com/document/product/555/7430).
- Bill details: Detailed records are not aggregated, and each fee entry is a detailed record. The details are the same as those in the bill details (L3) file. For more information, see [Bill Management](https://www.tencentcloud.com/document/product/555/7430).





<span id="XBZD"></span>



#### Directions
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com).
2. Click **Billing Center** in the top-right corner to enter the Billing Center overview page.
3. On the left sidebar, click **Bills** > **Bill Details** to view the bills by instance and bill details under the current account.
>? Select **Bill Overview** to view the billing trends and summary.
>
4. On the **Bill by Instance** tab, select **Cloud Object Storage** from the drop-down list to view your COS usage by region, billing mode, transaction type, etc. If you select **Hide 0 USD Items**, the Billing Center will automatically hide the bills of 0 USD items.
![](https://qcloudimg.tencent-cloud.cn/raw/d57e860dc2e1c482c6ba421c84cffb05.png)
On the **Bill Details** tab, select **Cloud Object Storage** from the drop-down list to view your unaggregated usage details.
![](https://qcloudimg.tencent-cloud.cn/raw/0e158dd0cf06ac91b4bbe30dfee2ca58.png)
>? 
>- To query the usage details of each billable item by **bucket** and cost allocation by bucket or region, click [Usage Details Download](https://console.cloud.tencent.com/expense/bill/dosageDownload) on the left sidebar to download the COS usage details report.
>- Currently, COS supports billing by bucket, which is made available through an allowlist. If your account is in the allowlist, you can see that fees are displayed by **bucket name** as the resource ID in bills by instance and bill details.
>
The configuration options are as described below:
 - **Region:** Select different regions in the region drop-down list to view the bill details by region.
 - **Billing Mode:** Select different billing modes in the billing mode drop-down list to view the bill details under pay-as-you-go billing mode.
 - **Transaction Type:** Select different transaction types in the transaction type drop-down list to view the bill details by pay-as-you-go purchase.





<span id="download"></span>

## Downloading Bill

You can download the target bill in the [Bill Download Center](https://console.cloud.tencent.com/expense/overview). Currently, available bill types include PDF bills (L0), bill summary (L1), bills by instance (L2), and bill details (L3).

>?
>- For more information on bills and bill fields, see [Bill Management](https://www.tencentcloud.com/document/product/555/7430) and [Fields in Bills](https://intl.cloud.tencent.com/document/product/555/37506) respectively.
>- For detailed directions on how to download bills, see [Bill Download Center](https://intl.cloud.tencent.com/document/product/555/44357).

