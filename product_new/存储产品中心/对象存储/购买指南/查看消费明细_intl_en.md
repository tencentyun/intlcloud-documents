## Overview
You can view the information of fees incurred by your account's usage of the COS service in the **Billing Center** in the Tencent Cloud Console. At present, the Billing Center supports two billing query methods, i.e., **New Version of Billing** and **Resource Billing v1.0**. The time available for viewing the new version of bills depends on when your account activates the New Version of Billing. For example, if your account activated it in May 2018, you can view the new version of bills generated in and after May 2018. For bills before May 2018, you can only view the resource bills v1.0. The Resource Billing v1.0 was officially deprecated in December 2018. If you did not activate the New Version of Billing after that, the system did so automatically for you in December 2018. The bills for November 2018 and before can only be viewed in Resource Billing v1.0. For more information, see [Resource Billing v1.0](#JBZD).

>- At the time of COS bill settlement, the system will settle in the order of **free quota > resource package > pay-as-you-go billing**.
>  - By default, the system uses the pay-as-you-go billing method for bill settlement, i.e., the system will deduct the free quota first (if available) and then bill the excessive usage (if any) in a pay-as-you-go manner.
>  - If you have purchased a resource package, during the validity period of the package, the system will deduct the free quota and resource package first and then bill the excessive usage (if any) in a pay-as-you-go manner and deduct the amount payable from your account.
> - For more information on free quotas, billing descriptions, and precautions, see [Free Quotas](https://intl.cloud.tencent.com/document/product/436/6240) and [Billing Descriptions](https://intl.cloud.tencent.com/document/product/555/7432).

## Query Method
<span id="XBZD">

### New Version of Billing
If you have activated the New Version of Billing, the billing system will perform statistics collection for the new version of bills, and you can only query billing details in New Version of Billing.
For more information, see [New Version of Billing](https://cloud.tencent.com/document/product/555/14192).

#### Directions
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com).
2. Click **Billing Center** in the top-right corner to enter the Billing Center overview page.
3. In the left sidebar, click **Billing Management**.
4. On the Billing Management page, select **Billing Details** to view COS resource ID bills and detailed bills.
   
   > Select **Billing Overview** to view the billing trends and summary. Select **Bill Download** to download the bills in the billed months.
5. On the Billing Details page, select **COS** in the drop-down list on the "Resource ID Billing" tab to view your COS bills by various filters such as region, billing method, and transaction type. Select "Hide Zero Fees" and the Billing Center will automatically hide bills for free resources.
The relevant options are as described below:
 - **Region:** Select different regions in the Region drop-down list to view the billing details by region.
 - **Billing Method:** Select different billing methods in the Billing Method drop-down list to view billing details under pay-as-you-go or monthly subscription billing method.
 - **Transaction Type:** Select different transaction types in the Transaction Type drop-down list to view the billing details by transaction type such as pay-as-you-go, new monthly subscription, and renewal.
![](https://main.qcloudimg.com/raw/b53decf61f43802686f8adf0ab2bb00b.png)
6. At the top right of the billing page, click <img src="https://main.qcloudimg.com/raw/e421450264489d44d20f11a44e15dfaa.png"  style="margin:0;"> to download your monthly COS bills.



<span id="JBZD">

### Resource Billing v1.0

Resource Billing v1.0 only display historical bills before you activated the New Version of Billing. 

#### Directions

1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com).
2. Click **Billing Center** in the top-right corner to enter the Billing Center overview page.
3. In the left sidebar, click **Billing Management**.
4. On the Billing Management page, select **Billing Overview** to enter the billing overview, select a date (e.g., the month before the New Version of Billing was activated), and follow the prompts to enter the Resource Billing v1.0 page.
![](https://main.qcloudimg.com/raw/1d5721209126f609598f8875dc09c003.png)
5. On the **Resource Billing v1.0** page, select the billing method (if you have purchased resource packages, select **Prepaid**) and you can view the corresponding billing details by project, time and other filters.
6. In the "Tencent Cloud Services" category, select COS in the drop-down list to view the billing details of COS, such as storage capacity, read and write requests, and CDN origin-pull traffic fees.
![](https://main.qcloudimg.com/raw/fa81cb5f0e25ec6cde831a57a03ea61b.png)
7. At the top right of the billing page, click <img src="https://main.qcloudimg.com/raw/a62b1624cbabded9ada7f42549be5b44.png"  style="margin:0;"> to download your monthly COS bills.

