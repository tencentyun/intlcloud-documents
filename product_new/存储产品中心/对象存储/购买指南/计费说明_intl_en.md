## Billing Method

COS can be charged in a pay-as-you-go manner.

This billing method applies to all regions where the COS service is provided. For more information, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).

## Billing Cycle

Billable items in COS include storage capacity, requests, data retrievals, and traffic as shown below:

![](https://main.qcloudimg.com/raw/41bce47bb77bf1b44b0076388a4a8e7f.png)

The fees for storage capacity, requests, and data retrievals are **settled on a monthly** basis. Fees for the previous month are calculated and bills are generated on the 3rd to 5th days of each month.

Traffic fees are **settled on a daily basis**. Fees for the past day are calculated and bills are generated everyday.

At the time of bill settlement, the system will settle in the order of **free quota > pay-as-you-go billing**.

By default, the system uses the pay-as-you-go billing method for bill settlement.

### Free Quotas

You can enjoy a certain amount of standard storage capacity provided by COS free of charge. For more information, see [Free Quotas](https://intl.cloud.tencent.com/document/product/436/6240).

### Relevant Links

1. For COS pricing in each billing method, see [COS Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
2. For more information on arrears processing in COS, data retention and purge schedule, and billing descriptions, see [COS Arrears Processing](https://intl.cloud.tencent.com/document/product/436/10044).
3. In the pay-as-you-go billing mode, you can estimate the usage and calculate the fees using the [COS Fees Calculator](https://buy.cloud.tencent.com/price/cos/calculator).

<a id="bill"></a>

## Billable Items

Billable items in COS include storage capacity, requests, data retrievals, and traffic as shown below. For pricing details, see [COS Pricing](https://intl.cloud.tencent.com/document/product/436/6239).

### Storage Capacity Fees

Storage capacity fees are calculated based on the storage capacity actually used by your data. The specific billable items and descriptions of such fees are as shown below:

| Billable Item | Applicable Storage Class | Meaning | Description |
| ---------------- | -------------- | -------------------------------------- | ------------------------------------------------------------ |
| Storage capacity | All | Calculated based on the actual storage capacity occupied by your data | Settled on a monthly basis <br />Storage capacity fees = storage capacity unit price \* monthly storage capacity used <br />Monthly storage capacity used = sum of daily storage capacity used in the month / number of days in the month <br/>Daily storage capacity used = sum of 5-minute storage capacity used / 288 (number of statistical points) |

#### Billing Restrictions

1. Standard_IA storage class: If the storage duration is less than 30 days, it will be calculated as 30 days. If a single file stored is less than 64 KB, it will be calculated as 64 KB; otherwise, it will be calculated as the actual size.
2. Archive storage class: This storage class is available in Mainland China only. If the storage duration is less than 90 days, it will be calculated as 90 days. If a single file stored is less than 64 KB, it will be calculated as 64 KB; otherwise, it will be calculated as the actual size.
3. If you upload an object in Standard_IA or Archive storage class with versioning not enabled, COS will delete the existing object of the **same name** (if any), and in this case, storage fees will still be incurred by **earlier deletion of the object**.

### Request Fees

Request fees are calculated based on the number of requests. You can use the APIs, SDKs or console to upload, download, query, or delete objects and do more, which are actually implemented by sending requests to COS.

Requests include read requests and write requests. The monthly unit prices are the same for different request types but vary by storage class. The more requests sent, the higher the fees. The specific billable items and descriptions of such fees are as shown below:

| Billable Item | Applicable Storage Class | Meaning | Description |
| ------------ | -------------- | ------------------------------------ | ------------------------------------------------------------ |
| Requests | All | Calculated based on the number of requests sent | Settled on a monthly basis <br />If the accumulated number of requests is below 10,000, it will be calculated as 10,000 requests <br />Request fees = unit price per 10,000 requests \* monthly accumulated number of requests / 10,000 (rounded down) |

#### Billing Restrictions

1. Request fees are charged for at least 10,000 requests; therefore, if the monthly accumulated number of requests is below 10,000, it will be calculated as 10,000 requests.
2. When archived data is read, the data is first restored to Standard storage class and then read there; therefore, the number of requests is counted in the Standard storage class.

### Data Retrieval Fees

Data retrieval fees are calculated based on the amount of data retrieved. The larger the amount, the higher the fees. The specific billable items and descriptions of such fees are as shown below:

| Billable Item | Applicable Storage Class | Meaning | Description |
| ---------------- | ---------------------- | -------------------------------- | ------------------------------------------------------ |
| Data retrieved | Standard_IA <br /> Archive | Calculated based on the amount of data retrieved | Settled on a monthly basis <br /> Data retrieval fees = unit price per GB \* monthly amount of data retrieved |

### Traffic Fees

Traffic fees are calculated based on the accumulated traffic generated by storage data reads. The specific billable items and descriptions of such fees are as shown below:

| Billable Item | Applicable Storage Class | Meaning | Description |
| -------------- | -------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| Public network upstream traffic | All | Traffic generated by data transmitted from client to COS over the internet | Free |
| Private network upstream traffic | All | Traffic generated by data transmitted from client to COS over the Tencent Cloud private network | Free |
| Public network downstream traffic | All | Traffic generated by data transmitted from COS to client over the internet | Settled on a daily basis <br /> Public network downstream traffic fees = unit price per GB \* daily accumulated public network downstream traffic |
| Private network downstream traffic | All | Traffic generated by data transmitted from COS to client over the Tencent Cloud private network | Free |
| CDN origin-pull traffic | All | Traffic generated by data transmitted from COS to CDN edge server | Settled on a daily basis <br />CDN origin-pull traffic fees = unit price per GB \* daily accumulated CDN origin-pull traffic |
| Cross-region replication traffic | All | Traffic generated by data transmitted from a bucket in one region to another bucket in another region | Settled on a daily basis <br />Cross-region replication traffic fees = unit price per GB \* daily accumulated cross-region replication traffic |

>- In the same region, Tencent Cloud products automatically communicate with one another over the private network and no traffic fees will be incurred. For more information on how to determine whether the Tencent Cloud private network is used for access, see [Judgment Method for Private Network Access](https://intl.cloud.tencent.com/document/product/436/30613).
>- Traffic generated by object downloads directly through **object links** and object browsing through **static website access node** is public network downstream traffic.
>- After CDN acceleration is enabled, traffic generated by browsing and downloading COS data from client though the **CDN accelerated domain name** is CDN origin-pull traffic.
>- Traffic generated by replication of data in a bucket in one region to another bucket in another region through the copy API or cross-region replication is cross-region replication traffic.

#### Traffic Direction
The figure below shows the traffic fees incurred by data transmitted from COS to end user with CND acceleration enabled and disabled, respectively.
![](https://main.qcloudimg.com/raw/0cbaaf4d9d524b12e3d320190152fe4f.png)


#### Billing Restrictions

When archived data is read, the data is first restored to Standard storage class and then read there; therefore, the traffic is counted in the Standard storage class.
