## Billing Method

COS supports Pay-as-You-Go billing method for all regions. 

For more information, see [Regions and Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

## Billing Cycle

Billable items in COS include storage capacity, requests, data retrievals, and traffic as shown below:

![](https://main.qcloudimg.com/raw/41bce47bb77bf1b44b0076388a4a8e7f.png)

The fees for storage capacity, requests, and data retrievals are **settled on a monthly** basis. Fees for the previous month are settled and billed on the 3rd to 5th days of each month.

Traffic fees are **settled on a daily basis**. Fees for the past day are settled and billed everyday.

At the time of bill settlement, the system will settle in the order of **Free Tier > Pay-as-You-Go billing**.

By default, the system uses the Pay-as-You-Go billing method for bill settlement.

### Free Tier

You are eligible for a certain amount of standard storage capacity provided by COS free of charge. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240).

### Relevant Links

1. See [COS Pricing](https://intl.cloud.tencent.com/document/product/436/6239) for more information about COS product pricing. 
2. For more information on arrears processing in COS, data retention, purge schedule and related billing issues, see [COS Arrears Processing](https://intl.cloud.tencent.com/document/product/436/10044).

<a id="bill"></a>

## Billable Items

Billable items in COS include storage capacity, requests, data retrievals, and traffic as shown below. For pricing details, see [COS Pricing](https://intl.cloud.tencent.com/document/product/436/6239).

### Storage Capacity Fees

Storage capacity fees are calculated based on the storage capacity actually used by your data. The billing details for storage capacity are as follows:

| Billable Items | Applicable Storage Class | Metric Description | Billing Description |
| ---------------- | -------------- | -------------------------------------- | ------------------------------------------------------------ |
| Storage capacity | All | Calculated based on the actual storage capacity occupied by your data | Settled on a monthly basis <br />Storage capacity fees = storage capacity unit price \* monthly storage capacity used <br />Monthly storage capacity used = sum of daily storage capacity used in the month / number of days in the month <br/>Daily storage capacity used = sum of every 5-minute storage capacity used of the day / 288 (number of statistical points) |

#### Billing Restrictions

1. Standard Infrequent Access Storage (Standard_IA Storage) class: if the storage duration is less than 30 days, it will be calculated as 30 days. If a single file stored is less than 64 KB, it will be calculated as 64 KB; otherwise, it will be calculated as the actual size.
2. Archive storage class: this storage class is available in Mainland China only. If the storage duration is less than 90 days, it will be calculated as 90 days. If a single file stored is less than 64 KB, it will be calculated as 64 KB; otherwise, it will be calculated as the actual size.
3. If you successfully uploaded an object in Standard_IA or Archive storage class without enabling versioning, COS will delete the existing object of the **same name** (if any), and in this case, storage fees will still incur for **objects that were deleted earlier**.

### Request Fees

Request fees are calculated based on the number of requests. You can perform upload, download, query, deletion and other data-related operations via API, SDK, console or related tool programs by sending request instructions to Tencent COS.

Requests are divided into read requests and write requests. The monthly unit prices are the same for all request types but vary by storage class. The more requests sent, the higher the fees. The billing details for requests are as follows:

| Billable Items | Applicable Storage Class | Metric Description | Billing Description |
| ------------ | -------------- | ------------------------------------ | ------------------------------------------------------------ |
| Number of Requests | All | Calculated based on the number of requests sent | Settled on a monthly basis <br />If the number of accumulated requests is below 10,000, it will be calculated as 10,000 requests <br />Request fees = unit price per 10,000 requests \* monthly number of accumulated requests / 10,000 (rounded down) |

#### Billing Restrictions

1. 10,000 requests serve as the smallest counting unit for request fees; therefore, if the number of monthly accumulated requests is below 10,000, it will be calculated as 10,000 requests.
2. When archived data is read, the data is first restored to standard storage class and then read there; therefore, the number of requests is counted in the standard storage class.

### Data Retrieval Fees

Data retrieval fees are calculated based on the amount of data retrieved. The larger the amount, the higher the fees. The billing details for data retrieval are as follows:

| Billable Items | Applicable Storage Class | Metric Description | Billing Description |
| ---------------- | ---------------------- | -------------------------------- | ------------------------------------------------------ |
| Data retrieved | Standard_IA <br /> Archive | Calculated based on the amount of data retrieved | Settled on a monthly basis <br /> Data retrieval fees = unit price per GB \* monthly amount of data retrieved |

#### Billing Restrictions
**Infrequent storage** and **archive storage** are storage classes for cold data. You need to retrieve objects first if you want to download and use the objects in these two storage classes. Therefore, traffic cost for downloading data and data retrieval cost will both be incurred. 

### Traffic Fees

Traffic fees are calculated based on the accumulated traffic generated by storage data reads. The billing details for traffic fees are as follows:

| Billable Items | Applicable Storage Class | Metric Description | Billing Description |
| -------------- | -------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| Public network upstream traffic | All | Traffic generated by data transmitted from client to COS over the internet | Free |
| Private network upstream traffic | All | Traffic generated by data transmitted from client to COS over the Tencent Cloud private network | Free |
| Public network downstream traffic | All | Traffic generated by data transmitted from COS to client over the internet | Settled on a daily basis <br /> Public network downstream traffic fees = unit price per GB \* daily accumulated public network downstream traffic |
| Private network downstream traffic | All | Traffic generated by data transmitted from COS to client over the Tencent Cloud private network | Free |
| CDN origin-pull traffic | All | Traffic generated by data transmitted from COS to CDN edge server | Settled on a daily basis <br />CDN origin-pull traffic fees = unit price per GB \* daily accumulated CDN origin-pull traffic |
| Cross-region replication traffic | All | Traffic generated by data transmitted from a bucket in one region to another bucket in another region | Settled on a daily basis <br />Cross-region replication traffic fees = unit price per GB \* daily accumulated cross-region replication traffic |

>- Tencent Cloud products within the same region access each other over private networks by default and no traffic fees will be incurred. For more information, see [How to Identify a Private Network Access](https://intl.cloud.tencent.com/document/product/436/30613#.E5.86.85.E7.BD.91.E4.B8.8E.E5.A4.96.E7.BD.91.E8.AE.BF.E9.97.AE).
>- Public network downstream traffic consists of the traffic generated by downloading objects through **object links** and browsing objects through **static website access node**.
>- CDN origin-pull traffic refers to traffic generated by browsing or downloading COS data from the client through **CDN acceleration domain name** after CDN acceleration is enabled.
>- Cross-region replication traffic refers to traffic generated by sending data between buckets in different regions through the replication API or cross-region replication feature.

#### Traffic Trends
The figure below shows the traffic fees incurred by data transmitted from COS to end user with CDN acceleration enabled and disabled, respectively.
![](https://main.qcloudimg.com/raw/af94a944fd1d9fb71be295f8db0f10f3.png)


#### Billing Restrictions

When archived data is read, the data is first restored to standard storage class and then read there; therefore, the traffic is counted in the Standard storage class.

