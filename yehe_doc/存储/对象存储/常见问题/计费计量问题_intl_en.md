## Billing Mode

### How is COS billed?

COS is pay-as-you-go. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).


### What are the billable items of COS?

COS billable items include [storage usage](https://intl.cloud.tencent.com/document/product/436/40099), [requests](https://intl.cloud.tencent.com/document/product/436/40100), [data retrievals](https://intl.cloud.tencent.com/document/product/436/40097), [traffic](https://intl.cloud.tencent.com/document/product/436/33776), and [management features](https://intl.cloud.tencent.com/document/product/436/40098). For more information, see [Pricing | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos). 



### Can COS be billed by bandwidth?

No. COS can be billed only on a pay-as-you-go (postpaid) basis.

### How are COS request fees calculated?

Request fees are calculated based on the number of requests sent to COS, including **user requests** and **backend requests** generated after you configure a feature. For more information, see [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).


### What changes have been made to COS pricing?
On September 30, 2021, the published prices of COS were reduced as follows:
1. Unit price of object tagging
 - Product pricing: The public cloud prices for regions in and outside the Chinese mainland were reduced to 0.00025817 USD/10,000 tags/day and 0.0003098 USD/10,000 tags/day, respectively.
 - Billing cycle: Fees incurred between 00:00 and 23:59:59 on a day are settled the next day.
 - Bill description: These prices have taken effect for bills generated starting from October 1, 2021 (i.e., fees incurred after September 30, 2021).

2. Unit price of DEEP ARCHIVE read/write requests
 - Product pricing: The public cloud prices for all regions were reduced to 0.07 USD/10,000 requests.
 - Billing cycle: Fees incurred in a month are billed on the first day of the next month.
 - Bill description: These prices have taken effect for bills generated starting from October 1, 2021 (i.e., fees incurred in September).


### To which regions will the reduction in the unit price of STANDARD_IA storage usage apply?

The reduction in the unit price of STANDARD_IA storage usage from 0.018 USD/GB/month to 0.015 USD/GB/month will apply to certain regions of Tencent Cloud International, including Mumbai, Seoul, Bangkok, Silicon Valley, Moscow, Jakarta, and  São Paulo. The reduction has taken effect on July 1, 2022.


## Free Tier

### Does COS offer a free tier?

COS offers a limited free tier to all new users (i.e., individual and enterprise users activating COS for the first time) to deduct the fees incurred by data stored in the STANDARD storage class. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240).


### Does COS offer a free tier outside the Chinese mainland?

Yes. The free tier is applicable to **public cloud regions** (including regions outside the Chinese mainland). For more information on regions, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

The free tier offered by COS can be used to deduct only **STANDARD storage usage** but not **other** billable items, such as STANDARD_IA storage usage, ARCHIVE storage usage, requests, and traffic. For more information, see [Billable Items](https://intl.cloud.tencent.com/document/product/436/40096).


### Why does my account still have overdue payments (with fees deducted) even if I am entitled to the free tier?

The following are some of the possible reasons why your account has overdue payments if your free tier hasn't expired:

1. Multiple billable items are used, but the free tier is insufficient to deduct the fees of all the billable items:
 - When you upload data to the STANDARD storage class, [storage usage fees](https://intl.cloud.tencent.com/document/product/436/40099) will be incurred, which can be deducted from the free tier offered by COS. COS provides multiple separately billed storage classes. The free tier of STANDARD cannot be applied to deduction of fees of other storage classes (such as STANDARD_IA).
 - Objects that need to be accessed or downloaded by other users incur [traffic](https://intl.cloud.tencent.com/document/product/436/33776) and [requests](https://intl.cloud.tencent.com/document/product/436/40100) fees, which cannot be deducted from the free tier.
    - If you upload and download data between the COS bucket and CVM instance in the same region, the access is over the private network in the same region and doesn't incur traffic fees (cross-region private network access will incur cross-region traffic fees). If your data is downloaded to the local file system through the console, API, or COS tools, public network downstream traffic fees will be incurred.
    - COS offers multiple storage classes that generate different types of requests. For example, if STANDARD_IA data is downloaded, STANDARD_IA requests will be generated and billed on a pay-as-you-go basis.
 - If your COS bucket is used together with CDN, CDN origin-pull traffic fees may also be incurred. For more information, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776#cos-.E4.BD.9C.E4.B8.BA-cdn-.E6.BA.90.E7.AB.99.E6.97.B6.E4.BA.A7.E7.94.9F.E7.9A.84.E6.B5.81.E9.87.8F).
 - If you enable global acceleration, global acceleration fees will also be incurred.
2. Resource usage in excess of the free tier:
For example, if COS offers you free STANDARD storage usage of 50 GB, but your actual usage is 60 GB, the excess of 10 GB will be pay-as-you-go.
3. Expiration of the free tier:
COS offers new users a free tier of STANDARD storage usage valid for six months. After the free tier expires, storage usage will be pay-as-you-go.


### Does the free tier apply to the INTELLIGENT TIERING storage class?

No. The free tier is applicable only to **STANDARD storage usage** but not **other billable items** such as STANDARD_IA/ARCHIVE storage usage, requests, and traffic.

INTELLIGENT TIERING is an independent storage class and incurs INTELLIGENT TIERING storage usage fees, which cannot be deducted from the free tier for the STANDARD storage class. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240).

### Does COS offer a free tier for CDN usage?

No. COS and CDN are different products. The CDN origin-pull traffic generated by the use of CDN is billed by COS on a pay-as-you-go basis, and the generated CDN traffic is billed by CDN. For more information on the differences between these two types of traffic, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776#cos-.E4.BD.9C.E4.B8.BA-cdn-.E6.BA.90.E7.AB.99.E6.97.B6.E4.BA.A7.E7.94.9F.E7.9A.84.E6.B5.81.E9.87.8F).


## Traffic

### How is the public network downstream traffic in COS generated and billed?

Public network downstream traffic is the traffic generated by data transfer from COS to the client over the internet. Traffic generated by downloading an object directly through an object link or by browsing an object at a static website endpoint is public network downstream traffic. For billing details, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776) and [Pricing | Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/6239).

### Will downloading files through the COS console, tools, API, or SDK incur public network downstream traffic fees?

The traffic (private or public network traffic) generated by accessing COS is subject to the use case, and only access to COS from a Tencent Cloud product in the same region will be over the private network by default with no public network downstream traffic fees incurred. For more information on how to identify private network access, see [Overview](https://intl.cloud.tencent.com/document/product/436/30613).

### What is public network traffic in COS?

Public network downstream traffic is the traffic generated by data transfer from COS to the client over the internet. Downloading a file stored in COS in the COS console, accessing or downloading an object through a tool, object address, or custom domain name, and previewing an object in a browser will generate public network downstream traffic. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30613).

### Will accessing COS over the private network incur fees?

Accessing COS over the private network will incur **storage usage fees** and **request fees** but not **traffic fees**. For more information, see [Billable Items](https://intl.cloud.tencent.com/document/product/436/40096).


### How will COS be billed after it is connected to CDN?

After COS is connected to CDN, the fees incurred by COS and CDN will be billed separately.

- COS fees include storage usage fees, request fees, and CDN origin-pull traffic fees.
- CDN fees include CDN traffic fees.

### Why is public network downstream traffic generated after I enable CDN acceleration?

If you still use a COS origin domain name (in the format of `<BucketName-APPID>.cos.<region>.myqcloud.com`) to access files in COS after enabling CDN acceleration, public network downstream traffic fees will be incurred. We recommend you use a CDN acceleration domain name instead, which will generate CDN origin-pull traffic only.


### What is CDN origin-pull traffic in COS? How is it generated?

CDN origin-pull is to pull data from COS to the cache node by CDN when a file not cached on a CDN edge node is accessed at a CDN domain name.

>? CDN origin-pull will incur origin-pull traffic fees. For more information on the unit price, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776#cos-.E4.BD.9C.E4.B8.BA-cdn-.E6.BA.90.E7.AB.99.E6.97.B6.E4.BA.A7.E7.94.9F.E7.9A.84.E6.B5.81.E9.87.8F).
>

### How is the CDN origin-pull traffic in COS billed?

CDN origin-pull traffic is the traffic generated by data transfer from COS to a CDN edge node. After CDN acceleration is enabled, traffic generated by browsing or downloading COS data in the client at a **CDN acceleration domain name** is CDN origin-pull traffic. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) and [Pricing | Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/6239).

### What are the differences between CDN origin-pull traffic and CDN traffic?

CDN origin-pull traffic is a billable item in COS. It is the origin-pull traffic generated by data transfer from COS to the CDN edge node when COS is used as the CDN origin.

CDN traffic is a billable item in CDN. It is the traffic generated by data transfer from a CDN edge node to the client.



### Will fees be charged for traffic and requests generated by data transfer between COS and CVM?

For data transfer between a COS bucket and a CVM instance in the same region, fees will be charged for requests but not the private network traffic. If they are in different regions, fees will be charged for both requests and traffic. For more information on how to identify private network access, see [Overview](https://intl.cloud.tencent.com/document/product/436/30613).


### Will there be traffic fees when I upload a file to a COS bucket?

No. The upstream traffic generated by file uploads is free of charge.

### Will there be traffic fees when I access Tencent Cloud products in the same region?

Tencent Cloud products in the same region access each other over the private network by default, with no traffic fees incurred. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30613).


## Bill

### How do I view bills?

You can view the fees incurred by the use of COS under your account in the [Billing Center](https://console.cloud.tencent.com/expense/bill/summary) in the console. For more information, see [Viewing Billing Details](https://intl.cloud.tencent.com/document/product/436/31631). You can view bucket-level bill details by downloading the usage details in the [Billing Center](https://console.cloud.tencent.com/expense/bill/summary).

## Overdue Payment and Service Suspension

### Can I still access and download files in the COS console if my COS service is suspended due to overdue payments?

After the COS service is suspended due to overdue payments, you cannot read or write data from or to COS, but you can top up your account. For more information, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/436/10044).

### Why can't I use the COS service after topping up my account to a positive balance?

Your account will be automatically unblocked in ten minutes after it is topped up. If your account is still displayed as blocked, the browser may have cached the historical page. In this case, we recommend you **refresh the webpage** or **clear the browser cache** first.

### Why are there daily and monthly billing modes in the transaction details?

COS comes with multiple billable items. Storage, requests, STANDARD_IA data retrievals, and ARCHIVE data retrievals are billed monthly, while DEEP ARCHIVE data retrievals, traffic, and management features are billed daily. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).


## Others

### How is data migration from another cloud to COS billed?

When you migrate data from another cloud to Tencent Cloud COS, outbound traffic fees will be charged by your source cloud storage vendor. The write traffic generated by migration to Tencent Cloud is free of charge, but storage usage and request fees will be incurred. For COS billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).

### How is data stored in STANDARD_IA for less than 30 days billed?

STANDARD_IA storage of data for less than 30 days will be calculated as 30 days, and storage for 45 days will be calculated as two cycles. For more information, see [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099#.E5.AD.98.E5.82.A8.E5.AE.B9.E9.87.8F.E8.B4.B9.E7.94.A8).

### How is data stored in ARCHIVE for less than 90 days billed?

ARCHIVE storage of data for less than 90 days will be calculated as 90 days. For more information, see [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099#.E5.BD.92.E6.A1.A3.E5.AD.98.E5.82.A8.E5.AE.B9.E9.87.8F.E8.B4.B9.E7.94.A8).


### How is data stored in DEEP ARCHIVE for less than 180 days billed?

DEEP ARCHIVE storage of data for less than 180 days will be calculated as 180 days. If you successfully uploaded an object to DEEP ARCHIVE without enabling versioning, COS will delete the existing object (if any) that has the same name. In this case, storage usage fees will be incurred for the early deletion of the object. For more information, see [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099#.E6.B7.B1.E5.BA.A6.E5.BD.92.E6.A1.A3.E5.AD.98.E5.82.A8.E5.AE.B9.E9.87.8F.E8.B4.B9.E7.94.A8).



### What are data retrieval fees in COS?

Data retrieval fees are fees incurred by reading or downloading **STANDARD_IA** data or restoring **ARCHIVE** or **DEEP ARCHIVE** data to STANDARD. They are calculated based on the amount of retrieved data. The higher the amount, the higher the fees. If you don't have special storage needs, you can directly use STANDARD, which doesn't involve data retrieval fees.


### What fees will be incurred by copying STANDARD_IA data?

Copying STANDARD_IA data will incur request fees and data retrieval fees and may also incur cross-region replication traffic fees if the destination and source files are in different regions.

For the calculation details of such fees, see [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100), [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097#.E4.BD.8E.E9.A2.91.E5.AD.98.E5.82.A8.EF.BC.88.E5.A4.9A-az.EF.BC.89.2F.E4.BD.8E.E9.A2.91.E5.AD.98.E5.82.A8.E6.95.B0.E6.8D.AE.E5.8F.96.E5.9B.9E.E8.B4.B9.E7.94.A8), and [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776).


### Will a copy generated by restoring ARCHIVE or DEEP ARCHIVE data in COS incur fees?

A copy generated by restoring ARCHIVE or DEEP ARCHIVE data is in the **STANDARD** storage class and will incur STANDARD storage usage fees.

### How are less than 10,000 read/write requests billed?

They will be billed based on the actual quantity. The minimum billable quantity of read/write requests is 10,000. The prices of read/write requests vary by storage class. For more information, see [Pricing | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos) and [Read/Write Requests](https://intl.cloud.tencent.com/document/product/436/40100#.E8.AF.BB.E5.86.99.E8.AF.B7.E6.B1.82.E8.B4.B9.E7.94.A8).


### Why are the COS read/write request fees zero?

If the number of requests does not reach the minimum value for fee deduction, the request fees will be zero.

Case study: If 23 STANDARD read requests for your data stored in the STANDARD storage class in a bucket in Beijing region were made in December 2021, the unit price of STANDARD read/write requests was 0.002 USD/10,000 requests, and your account wasn't entitled to any discount, then the STANDARD read request fees were 0.0023 \* 0.002 = 0.0000046 USD. As fee deduction is accurate down to two decimal places, your request fees for the month were 0 USD.

Cause: As bills support eight decimal places at most, while fee deduction is accurate down to two decimal places, the system will automatically adjust the accuracy difference. For more information, see [Bills](https://intl.cloud.tencent.com/document/product/555/7465).




### Will I be charged immediately after activating COS?

Activating COS is free of charge, and fees will be incurred only after you use it. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).

### Will file uploads to COS incur fees?

When you upload a file to COS, the generated **traffic is free of charge**, but the generated **write request** will incur fees, and the **storage usage fees** will be calculated based on the file size. If you access or download the object over the public network, public network downstream traffic fees will be incurred. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) and [Pricing | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos).

### Why are fees still deducted after my data in COS is deleted?

If you no longer use the COS service, you need to delete all the buckets under your account. Double check whether **all the buckets have been deleted**. If fees are still incurred after all the buckets are deleted, they may be **the monthly fees incurred in the last month**. COS storage usage fees and request fees are billed monthly, that is, a bill generated in the current month is for usage in the last month. You can go to the [transaction details](https://console.cloud.tencent.com/expense/transactions) page and click **Details** on the right of a billable item to view fee deduction details.

### What fees will be incurred by accessing COS through a URL?

[Public network downstream traffic fees](https://intl.cloud.tencent.com/document/product/436/33776) and [request fees](https://intl.cloud.tencent.com/document/product/436/40100) may be incurred. If you enable CDN and access data through a CDN domain name, CDN traffic fees and [CDN origin-pull traffic fees](https://intl.cloud.tencent.com/document/product/436/33776) will also be incurred.

### Do IOPS, latency, and throughput of COS vary by price?

No. For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

