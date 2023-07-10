## Billing Mode

### How is COS billed?

COS is pay-as-you-go. For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/436/16871).


### What are the billable items of COS?

COS billable items include [storage usage](https://www.tencentcloud.com/document/product/436/40099), [requests](https://www.tencentcloud.com/document/product/436/40100), [data retrievals](https://www.tencentcloud.com/document/product/436/40097), [traffic](https://www.tencentcloud.com/document/product/436/33776), and [management features](https://www.tencentcloud.com/document/product/436/40098). For more information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=). 



### Can COS be billed by bandwidth?

No. COS can be billed only on a pay-as-you-go (postpaid) basis.

### How are COS request fees calculated?

Request fees are calculated based on the number of requests sent to COS, including **user requests** and **backend requests** generated after you configure a feature. For more information, see [Request Fees](https://www.tencentcloud.com/document/product/436/40100).


### What changes have been made to COS pricing?
On September 30, 2021, the published prices of COS were reduced as follows:
1. Unit price of object tagging
 - Product pricing: The prices for public cloud regions in and outside the Chinese mainland were reduced to 0.00025817 USD/10,000 tags/day and 0.0003098 USD/10,000 tags/day, respectively.
 - Billing cycle: Fees incurred between 00:00 and 23:59:59 on a day are settled the next day.
 - Bill description: These prices have taken effect for bills generated starting from October 1, 2021 (i.e., fees incurred in September until September 30, 2021).

2. Unit price of DEEP ARCHIVE read/write requests
 - Product pricing: The prices for all public cloud regions were reduced to 0.07 USD/10,000 requests.
 - Billing cycle: Fees incurred in a month are billed on the first day of the next month.
 - Bill description: These prices have taken effect for bills generated starting from October 1, 2021 (i.e., fees incurred in September).


### Which regions will benefit from the reduced unit pricing of STANDARD IA storage usage?

The reduction in the unit price of STANDARD_IA storage usage from 0.018 USD/GB/month to 0.015 USD/GB/month will apply to certain regions, including Mumbai, Seoul, Bangkok, Silicon Valley, Jakarta, and São Paulo. The reduction has taken effect on July 1, 2022.


## Free Tier

### Does COS offer a free tier?

COS offers a limited free tier to all new users (both individual and enterprise users) to deduct the fees incurred by data stored in the STANDARD storage class. For more information, see [Free Tier](https://www.tencentcloud.com/document/product/436/6240).


### Does COS offer a free tier outside the Chinese mainland?

Yes. The free tier is applicable to **public cloud regions** (including those outside the Chinese mainland). For more information, see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224).

The free tier offered by COS can be used to deduct only **STANDARD storage usage** but not **other** billable items, such as STANDARD_IA storage usage, ARCHIVE storage usage, requests, and traffic. For more information, see [Billable Items](https://www.tencentcloud.com/document/product/436/40096).


### Why is my account overdue or charged even if I am on the free tier?

The following are some of the possible reasons why your account has overdue payments if your free tier hasn't expired:

1. Multiple billable items are used, but the free tier is insufficient to deduct the fees of all the billable items:
 - When you upload data to the STANDARD storage class, [storage usage fees](https://www.tencentcloud.com/document/product/436/40099) will be incurred, which can be deducted from the free tier offered by COS. COS provides multiple separately billed storage classes. The free tier of STANDARD cannot be applied to deduction of fees of other storage classes (such as STANDARD_IA).
 - Objects that need to be accessed or downloaded by other users incur [traffic](https://www.tencentcloud.com/document/product/436/33776) and [requests](https://www.tencentcloud.com/document/product/436/40100) fees, which cannot be deducted from the free tier.
    - If you upload and download data between the COS bucket and CVM instance in the same region, the access is over the private network in the same region and doesn't incur traffic fees (cross-region private network access will incur cross-region traffic fees). If your data is downloaded to the local file system through the console, API, or COS tools, public network downstream traffic fees will be incurred.
    - COS offers multiple storage classes that generate different types of requests. For example, if STANDARD_IA data is downloaded, STANDARD_IA requests will be generated and billed on a pay-as-you-go basis.
 - If your COS bucket is used together with CDN, CDN origin-pull traffic fees may also be incurred. For more information, see [Traffic Fees](https://www.tencentcloud.com/document/product/436/33776#cos-.E4.BD.9C.E4.B8.BA-cdn-.E6.BA.90.E7.AB.99.E6.97.B6.E4.BA.A7.E7.94.9F.E7.9A.84.E6.B5.81.E9.87.8F).
 - If you enable global acceleration, global acceleration fees will also be incurred.
2. Resource usage in excess of the free tier:
For example, if COS offers you free STANDARD storage usage of 50 GB, but your actual usage is 60 GB, the excess of 10 GB will be pay-as-you-go.
3. Expiration of the free tier:
COS offers new users a free tier of STANDARD storage usage valid for six months. After the free tier expires, storage usage will be pay-as-you-go.


### Does the free tier apply to the INTELLIGENT TIERING storage class?

No. The free tier is applicable only to **STANDARD storage usage** but not **other billable items** such as STANDARD_IA/ARCHIVE storage usage, requests, and traffic.

INTELLIGENT TIERING is an independent storage class and incurs INTELLIGENT TIERING storage usage fees, which cannot be deducted from the free tier for the STANDARD storage class. For more information, see [Free Tier](https://www.tencentcloud.com/document/product/436/6240).

### Does COS offer a free tier for CDN usage?

No. COS and CDN are different products. The CDN origin-pull traffic generated by the use of CDN is billed by COS on a pay-as-you-go basis, and the generated CDN traffic is billed by CDN. For more information on the differences between these two types of traffic, see [Traffic Fees](https://www.tencentcloud.com/document/product/436/33776#cos-.E4.BD.9C.E4.B8.BA-cdn-.E6.BA.90.E7.AB.99.E6.97.B6.E4.BA.A7.E7.94.9F.E7.9A.84.E6.B5.81.E9.87.8F).


## Notification

### What types of notifications does COS send?

COS sends notifications for new feature launch, product change, expiration, repossession, and alarms.

### What are subscribed and non-subscribed messages?

- Subscribed messages: You can customize their recipients and notification methods in Message Center. They are used in default scenarios.
- Non-subscribed messages: You cannot modify their recipients and notification methods but can only receive them passively. They are used in special scenarios.

### How do I configure the root account and sub-accounts to receive COS notifications?

You can customize the recipients of COS notifications by setting **Message Recipient** in [Subscription Management](https://console.cloud.tencent.com/message/subscription/) in Message Center.




## Traffic


### What are the differences among COS public network downstream traffic, CDN origin-pull traffic, and global acceleration traffic?

- **Public network downstream traffic**: The traffic generated by data transfer from COS to the client over the internet, such as the traffic generated when you directly access a resource at a COS domain name in a browser.
- **CDN origin-pull traffic**: The traffic generated by data transfer from COS to a CDN edge node when you access a CDN acceleration domain after enabling CDN acceleration.
- **Global acceleration traffic**: The traffic generated by data transfer with acceleration domains after global acceleration is enabled.


### How is the public network downstream traffic in COS generated and billed?

Public network downstream traffic is traffic generated by data transfer from COS to the client over the Internet. Traffic generated by downloading an object directly through an **object link** or by browsing an object through a **static website access node** is public network downstream traffic. For more information on billing for such traffic, see [Billable Items](https://www.tencentcloud.com/document/product/436/33776) and [Product Pricing](https://www.tencentcloud.com/document/product/436/6239).

### Will I be charged for public network downstream traffic generated by downloading files through the COS console, tools, API, or SDK?

The traffic (private or public network traffic) generated by accessing COS is subject to the use case, and only access to COS from a Tencent Cloud product in the same region will be over the private network by default, with no public network downstream traffic fees incurred. For more information on how to identify private network access, see [Overview > Private Network Access](https://www.tencentcloud.com/document/product/436/30613).

### What is public network traffic in COS?

Public network downstream traffic is the traffic generated by data transfer from COS to the client over the internet. Downloading a file stored in COS in the COS console, accessing or downloading an object through a tool, object address, or custom domain name, and previewing an object in a browser will generate public network downstream traffic. For more information, see [Overview](https://www.tencentcloud.com/document/product/436/30613).

### Will accessing COS over the private network incur fees?

Accessing COS over the private network will incur **storage usage fees** and **request fees** but not **traffic fees**. For more information, see [Billable Items](https://www.tencentcloud.com/document/product/436/40096).


### How will COS be billed after it is connected to CDN?

After COS is connected to CDN, the fees incurred by COS and CDN will be billed separately.

- COS fees include storage usage fees, request fees, and CDN origin-pull traffic fees.
- CDN fees include CDN traffic fees.

### Why is there public network downstream traffic after I enabled CDN acceleration?

It may be because you are still using the COS origin domain name formatted as `<BucketName-APPID>.cos.<region>.myqcloud.com` to access COS files after you enabled CDN acceleration. We recommend that you use the CDN acceleration domain name instead, which only generates CDN origin-pull traffic.


### What is CDN origin-pull traffic in COS? How is it generated?

CDN origin-pull is to pull data from COS to the cache node by CDN when a file not cached on a CDN edge node is accessed at a CDN domain name.

>? CDN origin-pull will incur origin-pull traffic fees. For more information, see [Traffic Fees](https://www.tencentcloud.com/document/product/436/33776#cos-.E4.BD.9C.E4.B8.BA-cdn-.E6.BA.90.E7.AB.99.E6.97.B6.E4.BA.A7.E7.94.9F.E7.9A.84.E6.B5.81.E9.87.8F).
>

### How is the CDN origin-pull traffic billed in COS?

CDN origin-pull traffic is the traffic generated by data transfer from COS to a Tencent Cloud CDN edge node. After CDN acceleration is enabled, traffic generated by browsing or downloading COS data on the client at a **CDN acceleration domain name** is CDN origin-pull traffic. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) and [Pricing | Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/6239).

### What are the differences between CDN origin-pull traffic and CDN traffic?

CDN origin-pull traffic is a billable item in COS. It is the origin-pull traffic generated by data transfer from COS to the CDN edge node when COS is used as the CDN origin.

CDN traffic is a billable item in CDN. It is the traffic generated by data transfer from a CDN edge node to the client.



### Will fees be charged for traffic and requests generated by data transfer between COS and CVM?

When data transfer happens between COS and CVM from different regions, there are charges for both traffic and requests. When data is transferred in the same region, there are charges for requests, but not for traffic (free for data transfer over private network). For more information, see [How to determine access over private network](https://www.tencentcloud.com/document/product/436/30613).


### Will there be traffic fees when I upload a file to a COS bucket?

No. The upstream traffic generated by file uploads is free of charge.

### Will there be traffic fees when I access Tencent Cloud products in the same region?

Tencent Cloud products within the same region access each other over the private network by default, with no traffic fees incurred. For more information, see [How to determine an access over private network](https://www.tencentcloud.com/document/product/436/30613).


## Bill

[](id:view)
### How do I view my bill?

You can view the fees incurred by the use of COS under your account in the [Billing Center](https://console.cloud.tencent.com/expense/bill/summary) in the console. For more information, see [Viewing and Downloading Bill](https://www.tencentcloud.com/document/product/436/31631). You can view bucket-level bill details by downloading the usage details in the [Billing Center](https://console.cloud.tencent.com/expense/bill/summary).

[](id:download)
### How do I download a bill?

Log in to the Tencent Cloud console, select **Billing Center** > [Bill Download Center](https://console.cloud.tencent.com/expense/bill/downloadCenter), and download the target bill packages, PDF bills (L0), bill summary (L1), bills by instance (L2), and bill details (L3). For more information, see [Bill Download Center](https://www.tencentcloud.com/document/product/555/44357).

![](https://qcloudimg.tencent-cloud.cn/raw/553cb59e57aaeb1799c3d2343b5bf5c5.png)

[](id:type)

### What are billing by bucket and cost allocation by tag?

- Billing by bucket: It refers to using the bucket name and `APPID` together as the **resource ID** and using the bucket name as the **instance name**, i.e., generating bills by bucket. You can view the fees and usage of billable items by bucket.
- Cost allocation by tag: You can specify **[cost allocation tags](https://www.tencentcloud.com/document/product/555/32276)** to differentiate resources by category.


[](id:set)
### How do I set billing by bucket and cost allocation by tag?

COS supports billing by bucket and cost allocation by tag.
- Billing by bucket: Contact your sales rep to add your account to the allowlist of the billing by bucket feature. This feature will take effect for new bills the next day after approval, while historical bills will remain unchanged.
- Cost allocation by tag: Tag your buckets, set cost allocation tags, and contact your sales rep to add your account to the allowlist of the billing by bucket feature.

>? 
>After your account is added to the allowlist, billing by bucket will take effect only for new bills, while existing bills will remain unchanged. In addition, you cannot go back to the previous billing option.

[](id:judge)
### How do I determine whether bills are generated by bucket?

You can determine this in two ways:

- Option 1: Select **Billing Center** > **[Billing Details](https://console.cloud.tencent.com/expense/bill/summary)** and view **Bill by Instance** and **Bill Details**. If the **Resource Alias/ID** is a bucket name and APPID, billing by bucket has been enabled.
- Option 2: Select **Billing Center** > **[Bill Download Center](https://console.cloud.tencent.com/expense/bill/downloadCenter)** and download bill details (L3). If the **Resource ID** is a bucket name and APPID and **Instance Name** is a bucket name, billing by bucket has been enabled.

Below are the effects after billing by bucket is enabled:

(1) Bill by instance
![](https://qcloudimg.tencent-cloud.cn/raw/bdd9bc55eede1fc285c86e0d8b2e2650.png)

(2) Bill details
![](https://qcloudimg.tencent-cloud.cn/raw/22b5746f4ae1d8ff98748812ab98f417.png)

(3) Bill details (L3)
![](https://qcloudimg.tencent-cloud.cn/raw/bbb892a392e0a006eba5e72aebeefebd.png)

Note: After the billing by bucket feature of COS is fully launched, on the **Cost Allocation - Month** sheet in the usage details, the bucket cost allocation information won't be displayed, while other information stays unchanged. For specific bucket fees, download the L2 or L3 bill.



### How is the billing by bucket feature of COS launched?

The billing by bucket feature of COS was made available through an allowlist starting from October 28, 2022 as follows:
- If you had applied to add your UIN to the allowlist of the billing by bucket feature, the **Resource ID** and **Instance Name** columns in the bill would change, where the **Resource ID** is a bucket name + `APPID` and **Instance Name** is a bucket name.
- If you hadn't applied to add your UIN to the allowlist of the billing by bucket feature, billing would stay unchanged.

Starting from February 1, 2023, the feature was **made available to users in batches by UIN** as follows:

| Launch Date | Description | Bill Description |
|---------|---------|---------|
| October 28, 2022 | Feature launch - through allowlist. | (1) Billing stayed unchanged for users not in the allowlist. (2) Billing by bucket was enabled for users in the allowlist. |
| February 1, 2023 | Before full launch - allowed account verification. | (1) Billing stayed unchanged for users not in the allowlist. (2) Billing by bucket was enabled for users in the allowlist. |
| February 6, 2023 | Batch 1 launch - for UINs ending in 9 | (1) Billing by bucket was enabled for users in the allowlist and with UINs ending in 9. (2) Billing stayed unchanged for other users. |
| February 20, 2023 | Batch 2 launch - for UINs ending in 2 | (1) Billing by bucket was enabled for users in the allowlist and with UINs ending in 9 or 2. (2) Billing stayed unchanged for other users. |
| March 7, 2023 | Batch 3 launch - for UINs ending in 3 | (1) Billing by bucket will be enabled for users in the allowlist and with UINs ending in 9, 2, or 3. (2) Billing will stay unchanged for other users. | 
| March 14, 2023 | Batch 4 launch - for UINs ending in 4 | (1) Billing by bucket will be enabled for users in the allowlist and with UINs ending in 9, 2, 3, or 4. (2) Billing will stay unchanged for other users. | 
| March 21, 2023 | Batch 5 launch - for UINs ending in 5 | (1) Billing by bucket will be enabled for users in the allowlist and with UINs ending in 9, 2, 3, 4, or 5. (2) Billing will stay unchanged for other users. | 




[](id:period)
### How do I view the billing statistical period?

Log in to the Tencent Cloud console, select **Billing Center** > **[Bill Overview](https://console.cloud.tencent.com/expense/bill/overview)**, and view the billing statistical period of your account.

[](id:charge)
### What are billing by deduction cycle and billing by billing cycle?

- Billing by deduction cycle: The system generates a bill per calendar month based on the **resource fees deduction time**.
- Billing by billing cycle: The system generates a bill per calendar month based on the **actual resource usage time**.

[](id:relationship)
### What is the relationship between the billing mode and billing statistical period?

COS adopts the pay-as-you-go (postpaid) billing mode.

- Pay-as-you-go (postpaid) resources
  - Daily settled resources: Fees incurred from 00:00 to 23:59 on January 31 will be deducted on February 1. The record will be posted to the bill for February by deduction cycle and to the bill for January by billing cycle.
  - Monthly settled resources: Fees incurred from 00:00 on January 1 to 23:59 on January 31 will be deducted on February 1. The record will be posted to the bill for February by deduction cycle and to the bill for January by billing cycle.


For more information on billing cycles, see [Bill Management](https://www.tencentcloud.com/document/product/555/7430).

[](id:costMore)
### Why did the amount of the bill (by deduction cycle) of the first month “increase” after the upgrade from monthly to daily settlement?

Starting from July 1, 2022, the settlement cycle of COS storage usage, request, and data retrieval fees was upgraded from monthly to daily to help you manage fees in a more refined manner. The upgrade was implemented on user accounts in batches and went through a two-month beta test. The release dates of different bill statistical periods are as listed below. For more information, see [Daily Billing for COS Storage Usage, Request, and Data Retrieval](https://www.tencentcloud.com/document/product/436/47593) and [Bill Management](https://www.tencentcloud.com/document/product/555/7430).

| Release Date                               | Release Note                          | Bill Description                         |
| ------------------------------------ | ------------------------------- | ------------------------------ |
| July 1, 2022 | The first release for the first batch of accounts in beta test | (1) Resources were settled monthly before July 1, 2022. Fees incurred from 00:00 on June 1 to 23:59 on June 30 were deducted on July 1. The record was posted to the bill for July by deduction cycle and to the bill for June by billing cycle. <br> (2) Resources were settled daily after July 1, 2022. Fees incurred from 00:00 to 23:59 on July 1 were deducted on July 2. The record was posted to the bill for July 2 by deduction cycle and to the bill for July 1 by billing cycle. |
| August 1, 2022 | The second release for the second batch of accounts in beta test | (1) Resources were settled monthly before August 1, 2022. Fees incurred from 00:00 on July 1 to 23:59 on July 31 were deducted on August 1. The record was posted to the bill for August by deduction cycle and to the bill for July by billing cycle. <br> (2) Resources were settled daily after August 1, 2022. Fees incurred from 00:00 to 23:59 on August 1 were deducted on August 2. The record was posted to the bill for August 2 by deduction cycle and to the bill for August 1 by billing cycle. |
| September 1, 2022 | The third release for all accounts | (1) Resources were settled monthly before September 1, 2022. Fees incurred from 00:00 on August 1 to 23:59 on August 31 were deducted on September 1. The record was posted to the bill for September by deduction cycle and to the bill for August by billing cycle. <br> (2) Resources were settled daily after September 1, 2022. Fees incurred from 00:00 to 23:59 on September 1 were deducted on September 2. The record was posted to the bill for September 2 by deduction cycle and to the bill for September 1 by billing cycle. |

Therefore, if the monthly usage remained the same, after monthly settlement was upgraded to daily settlement, the bill amount varied by billing statistical period and billable items as follows:
- Billing by billing cycle: The monthly fees of storage usage, requests, and data retrievals remain basically unchanged after the upgrade.
- Billing by deduction cycle: The monthly fees of storage usage increase after the upgrade, while the monthly fees of requests and data retrievals remain basically unchanged after the upgrade.

In the first month after the upgrade from monthly settlement to daily settlement, the storage fees increased. This was because two bills were generated for billing by deduction cycle. The first bill was the monthly bill for the last month, while the second bill was the daily bill for the current month. Therefore, the bill amount seemed to have increased, but no additional fees were deducted in fact, which was normal under the settlement and billing logic.

In the second month after the upgrade from monthly settlement to daily settlement, your bills were settled daily, and the bill amount "decreased" compared with that in the first month, which was also normal under the settlement and billing logic.

For example:
Your account is billed by deduction cycle and was upgraded from monthly settlement to daily settlement on September 1, 2022, and you downloaded the **bill details (L3)** of COS in the [Billing Center](https://console.cloud.tencent.com/expense/bill/summary) on September 30.

Taking the **COS STANDARD storage usage** billable item as an example, the bills consisted of the monthly bill for August and daily bill for September as detailed below:
 - Pay-as-you-go monthly settlement: The monthly bill was generated on September 1 for resource usage fees incurred in the entire August (from 00:00 on August 1 to 23:59 on August 31).
![](https://qcloudimg.tencent-cloud.cn/raw/e33e62685abec6f26131da286b669b38.png)
 - Pay-as-you-go daily settlement: After the upgrade from monthly settlement to daily settlement on September 1, a daily bill was generated on each day starting from September 2 for daily resource usage fees incurred in the entire September. The bill generated on September 2 was for fees incurred from 00:00 to 23:59 on September 1, that on September 3 was for fees incurred from 00:00 to 23:59 on September 2, and so on.
As there was too much bill data, only the daily bills for September 2–3 are listed below:
![](https://qcloudimg.tencent-cloud.cn/raw/ac2d710670f781a8f90979e2515096b4.png)

Therefore, if your monthly fees increased in the first month after the upgrade from monthly settlement to daily settlement and your bill was generated by deduction cycle, the increase was normal under the settlement and billing logic, and no additional fees were deducted in fact. If you have any questions, [contact us](https://www.tencentcloud.com/contact-sales) for assistance.


### Why are there daily and monthly settlement modes in the transaction details?

Before the upgrade, COS' storage, requests, STANDARD_IA data retrievals, and ARCHIVE data retrievals are settled monthly, and their monthly settlement details are displayed in the transaction details, while DEEP ARCHIVE data retrievals, traffic, and management features are still settled daily, and their daily settlement details are still displayed in the transaction details. After the upgrade, all COS billable items are settled daily. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).

In addition, you can view the L3 bill to check whether the billable items are settled daily or monthly as instructed in [Billing](https://intl.cloud.tencent.com/document/product/436/10373).


## Fee Deduction

### Will I be charged immediately after activating COS?

Activating COS is free of charge, and fees will be incurred only after you use it. For billing details, see [Billing Overview](https://www.tencentcloud.com/document/product/436/16871).

If you upload multiple files in a total size of 1 GB to the STANDARD storage class after activating COS and then view and download them, STANDARD storage, write requests, public/private network upstream traffic, and public network downstream traffic (of about 1 GB) will be generated, and the bill generated on the next day will include the STANDARD storage, STANDARD write request, and public network downstream traffic fees. As the public/private network upstream traffic is free of charge, it will not be included in the bill.

### Will file uploads to COS incur fees?

When you upload a file to COS, the generated **traffic is free of charge**, but the generated **write request** will incur fees, and the **storage usage fees** will be calculated based on the file size. If you access or download the object over the public network, public network downstream traffic fees will be incurred. For billing details, see [Billing Overview](https://www.tencentcloud.com/document/product/436/16871) and [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).

### Why are fees still deducted after my data in COS is deleted?

If you no longer use the COS service, you need to delete all the buckets under your account. Double check whether **all the buckets have been deleted**. If fees are still incurred after all the buckets are deleted, they may be **the daily fees incurred on the previous day**. COS storage usage fees and request fees are billed daily, that is, a bill generated on the current day is for usage on the previous day. You can go to the [transaction details](https://console.cloud.tencent.com/expense/transactions) page and click **Details** on the right of a billable item to view fee deduction details.

The details about the change from monthly settlement to daily settlement are as follows: Starting from July 1, 2022, the settlement cycle of COS storage usage, request, and data retrieval fees was upgraded from monthly to daily to help you manage fees in a more refined manner. The upgrade was implemented on user accounts in batches and went through a two-month beta test. The release dates of different bill statistical periods are as listed below. For more information, see [Daily Billing for COS Storage Usage, Request, and Data Retrieval](https://www.tencentcloud.com/document/product/436/47593) and [Bills](https://www.tencentcloud.com/document/product/555/7432).


### How do I deactivate the COS service and stop being charged?

You can deactivate COS or stop its billing as follows:

1. If you decide to stop using COS, you can avoid any further billing by permanently deleting all of your COS data (including incomplete multipart uploads and object versions) as instructed in [Payment Overdue](https://intl.cloud.tencent.com/document/product/436/10044). There is no need to remove your account, and if you use other Tencent Cloud products, avoid doing so as it will affect your other services.
2. If you don't use COS for more than one month, you can set lifecycle rules to transition data in STANDARD storage class in the bucket to a colder class such as STANDARD_IA, ARCHIVE, or DEEP ARCHIVE to reduce storage fees. For more information, see [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605). The transition will generate read requests in the original storage class and write requests in the target storage class, so transition by lifecycle will incur read/write [request fees](https://intl.cloud.tencent.com/document/product/436/40100).


**Notes**

- Data, once deleted from the bucket, cannot be recovered, so make backups accordingly.
- If versioning is enabled for the bucket, disable it before deleting data.
- Check your billing cycle to avoid overdue payments. If all your billable items are settled daily, the bill for the day of data deletion will be generated on the next day. After the data is completely cleared, the system will stop billing. For more information, see [Billing Cycle](https://intl.cloud.tencent.com/document/product/436/16871).
- If your account has overdue payment (i.e., your account balance is below 0), COS services will be suspended after 24 hours, regardless of whether your resource pack is within the validity period.
- If your account has overdue payment and COS services are suspended, the free tier for which your account is eligible won't be available.
- If data in your bucket is blocked for the second time due to non-compliance, it cannot be deleted. [Contact us](https://intl.cloud.tencent.com/contact-sales) if you have any questions. 


### How will I be charged when storing data in STANDARD_IA for less than 30 days?

The minimum data storage duration in STANDARD_IA storage class is 30 days.

Below are the specific rules:
- An object stored less than 30 days is billed by 30 days as described in [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099).
- An object stored more than 30 days is billed by the actual storage duration.

For more information, see "STANDARD_IA storage usage fees" and "Billing Mode and Calculation Formula" in [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099).

### How will I be charged when storing data in ARCHIVE for less than 90 days?

The minimum data storage duration in ARCHIVE storage class is 90 days.

Below are the specific rules:
- An object stored less than 90 days is billed by 90 days as described in [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099).
- An object stored more than 90 days is billed by the actual storage duration.

For more information, see "ARCHIVE storage usage fees" and "Billing Mode and Calculation Formula" in [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099).

### How will I be charged when storing data in DEEP ARCHIVE for less than 180 days?

The minimum data storage duration in DEEP ARCHIVE storage class is 180 days.

Below are the specific rules:
- An object stored less than 180 days is billed by 180 days as described in [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099).
- An object stored more than 180 days is billed by the actual storage duration.

For more information, see "DEEP ARCHIVE storage usage fees" and "Billing Mode and Calculation Formula" in [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099).


### What are data retrieval fees in COS?

Data retrieval fees are fees incurred by reading or downloading **MAZ_STANDARD_IA/STANDARD_IA** data or restoring **ARCHIVE** or **DEEP ARCHIVE** data to STANDARD. They are calculated based on the amount of retrieved data. The higher the amount, the higher the fees. If you don't have special storage needs, you can directly use STANDARD, which doesn't involve data retrieval fees.


### What fees will be incurred by copying MAZ_STANDARD_IA/STANDARD_IA data?

Copying MAZ_STANDARD_IA/STANDARD_IA data will incur request fees and data retrieval fees and may also incur cross-region replication traffic fees if the destination and source files are in different regions.

For the calculation details of such fees, see [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100), [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097#.E4.BD.8E.E9.A2.91.E5.AD.98.E5.82.A8.EF.BC.88.E5.A4.9A-az.EF.BC.89.2F.E4.BD.8E.E9.A2.91.E5.AD.98.E5.82.A8.E6.95.B0.E6.8D.AE.E5.8F.96.E5.9B.9E.E8.B4.B9.E7.94.A8), and [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776).


### Will I be charged for a copy generated by restoring ARCHIVE or DEEP ARCHIVE data in COS?

A copy generated by restoring ARCHIVE or DEEP ARCHIVE data is in the **STANDARD** storage class and will incur STANDARD storage usage fees.

### How will I be charged for less than 10,000 read/write requests?

The read/write requests are priced by storage class and billed based on the actual quantity, with a minimum billable quantity of 10,000. For more information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=) and [Request Fees](https://www.tencentcloud.com/document/product/436/40100#.E8.AF.BB.E5.86.99.E8.AF.B7.E6.B1.82.E8.B4.B9.E7.94.A8).


### Why are the COS read/write request fees zero?

If the number of requests does not reach the minimum value for fee deduction, the request fees will be zero.

Case study: If 23 STANDARD read requests for your data stored in the STANDARD storage class in a bucket in Beijing region were made in December 2021, the unit price of STANDARD read/write requests was 0.002 USD/10,000 requests, and your account wasn't entitled to any discount, then the STANDARD read request fees were 0.0023 \* 0.002 = 0.0000046 USD. As fee deduction is accurate down to two decimal places, your request fees for the month were 0 USD.

Cause: As bills support eight decimal places at most, while fee deduction is accurate down to two decimal places, the system will automatically adjust the accuracy difference. For more information, see [Bills](https://www.tencentcloud.com/document/product/555/7465).




## Overdue Payment and Service Suspension

### Can I still access and download files in the COS console if my COS service is suspended due to overdue payment?

After the COS service is suspended due to overdue payment, you cannot read or write data from or to COS, but you can top up your account. For more information, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/436/10044).

### Why can't I use the COS service after topping up my account to a positive balance?

Your account will be automatically unblocked in 10 minutes after it is topped up. If your account is still displayed as blocked, the browser may have cached the historical page. In this case, we recommend you **refresh the webpage** or **clear the browser cache** first.


## Data Processing

### How is the PowerPoint-to-image conversion in COS' document processing service billed? Will fees be incurred if I access an object that I have accessed before?

The document processing service is offered by CI, so its fees are also charged by CI. Fees will be incurred for every request; that is, fees will be deducted every time you refresh the URL. For more information, see [Document Processing Fees](https://intl.cloud.tencent.com/document/product/1045/49490).


## Others


### How will I be charged for migrating data from another cloud to COS?

When you migrate data from another cloud to Tencent Cloud COS, outbound traffic fees will be charged by your source cloud storage vendor. The write traffic generated by migration to Tencent Cloud is free of charge, but storage usage and request fees will be incurred. For COS billing details, see [Billing Overview](https://www.tencentcloud.com/document/product/436/16871).


### What fees will be incurred by accessing COS through a URL?

[Public network downstream traffic fees](https://www.tencentcloud.com/document/product/436/33776) and [request fees](https://www.tencentcloud.com/document/product/436/40100) may be incurred. If you enable CDN and access data through a CDN domain name, CDN traffic fees and [CDN origin-pull traffic fees](https://www.tencentcloud.com/document/product/436/33776) will also be incurred.


### Do IOPS, latency, and throughput of COS vary by price?

No. For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).
