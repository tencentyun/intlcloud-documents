## Billing Method

COS is billed on a pay-as-you-go basis as detailed below:

| Billing Method | Supported Regions |
| ------------------ | ------------------------------------------------------------ |
| Pay-as-you-go (postpaid) | All regions where the service is provided. For more information, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) |


## Free Tier

New users will receive a certain amount of standard storage provided by COS free of charge in six months after activating the COS service. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240).

> The free tier is not applicable to other billable items such as standard_IA and archive storage usage, requests, and traffic.



## Billable Items

Billable items in COS include [storage usage](#jf1), [requests](#jf2), [data retrievals](#jf3), [traffic](#jf4) and [administrative feature fees](#jf5) as shown below:

![](https://main.qcloudimg.com/raw/1355e7c9ca4ba0540edbc5fb9a0bf5a4.svg)

<span id="jf1"></span>

### Storage Usage Fees

COS offers three object storage classes for different access frequencies: standard storage, standard_IA storage, and archive storage. For more information, see [COS Storage Type](https://intl.cloud.tencent.com/document/product/436/30925).

Storage usage fees are calculated based on the storage actually used by your data. The specific billable items and descriptions of such fees are as shown below:

<table>
   <tr>
      <th>Billable Item</th>
      <th>Applicable Storage Class</th>
      <th>Meaning</th>
      <th>Billing Description</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Storage usage</td>
      <td>Standard storage<br>Standard_IA storage<br>Archive storage</td>
      <td>Calculated based on the actual storage occupied by your data</td>
      <td nowrap="nowrap"><li>Settled on a monthly basis <br><li>Storage usage fees = storage usage unit price * monthly storage used<br><li>Monthly storage used = sum of "daily storage used" in the month / number of days in the month <br><li>Daily storage used = sum of "5-minute storage used" / 288 (number of statistical points)</td>
   </tr>
</table>

#### Billing Restrictions

1. Standard_IA storage class: If the storage duration is less than 30 days, it will be calculated as 30 days. If a single file stored is less than 64 KB, it will be calculated as 64 KB; otherwise, it will be calculated as the actual size.
2. Archive storage class: This storage class is available in public cloud regions only. If the storage duration is less than 90 days, it will be calculated as 90 days. If a single file stored is less than 64 KB, it will be calculated as 64 KB; otherwise, it will be calculated as the actual size.
3. If you upload an object in standard_IA or archive storage class with versioning not enabled, COS will delete the existing object of the **same name** (if any), and in this case, storage fees will still incur for **earlier deletion of the object**.

<span id="jf2"></span>

### Request Fees

Request fees are calculated based on the number of requests. You can use the APIs, SDKs or console to upload, download, query, or delete objects and do more, which are actually implemented by sending requests to COS.

Requests include read requests and write requests. The monthly unit prices are the same for different request types but vary by storage class. The more requests sent, the higher the fees. The billing details for requests are as follows:

<table>
   <tr>
      <th>Billable Item</th>
      <th>Applicable Storage Class</th>
      <th>Meaning</th>
      <th>Billing Description</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Number of requests</td>
      <td>Standard storage<br>Standard_IA storage<br>Archive storage</td>
      <td>Calculated based on the number of requests sent</td>
      <td nowrap="nowrap"><li>Settled on a monthly basis<br><li>If the accumulated number of requests is below 10,000, it will be calculated as 10,000 requests<br><li>Request fees = unit price per 10,000 requests * monthly accumulated number of requests / 10,000 (rounded down)</td>
   </tr>
</table>

#### Billing Restrictions

1. Both successful and failed requests are billable.
2. 10,000 requests serve as the smallest counting unit for request fees; therefore, if the number of monthly accumulated requests is below 10,000 it will be calculated as 10,000 requests, no matter whether a request succeeds or fails.
3. When archived data is read, the data is first restored to Standard storage class and then read there; therefore, the number of requests is counted in the Standard storage class.

<span id="jf3"></span>

### Data Retrieval Fees

Data retrieval fees are calculated based on the amount of data retrieved. The larger the amount, the higher the fees. The specific billable items and descriptions of such fees are as shown below:

| Billable Item | Applicable Storage Class | Meaning | Description |
| ---------- | ---------------------- | -------------------------------- | ------------------------------------------------------------ |
| Data retrieved | Standard_IA <br /> Archive | Calculated based on the amount of data retrieved | <li>Settled on a monthly basis<br /><li>Data retrieval fees = unit price per GB \* monthly amount of data retrieved |

#### Billing Restrictions

**Standard_IA storage** and **archive storage** classes are for cold data. If you want to download and use objects in these two classes, you need to retrieve the objects first; therefore, fees will be incurred for both data downloads and data retrievals.

<span id="jf4"></span>

### Traffic Fees

Traffic fees are calculated based on the accumulated traffic generated by storage data reads. The billing details for traffic fees are as follows:

<table>
   <tr>
      <th>Billable Item</th>
      <th>Applicable Storage Class</th>
      <th>Meaning</th>
      <th>Billing Description</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Public network upstream traffic</td>
      <td rowspan="6">Standard storage<br>Standard_IA storage<br>Archive storage</td>
      <td>Traffic generated by data transfer from client to COS over the internet</td>
      <td>Free</td>
   </tr>
   <tr>
      <td>Private network upstream traffic</td>
      <td>Traffic generated by data transfer from client to COS over the Tencent Cloud private network</td>
      <td>Free</td>
   </tr>
   <tr>
      <td>Public network downstream traffic</td>
      <td>Traffic generated by data transfer from COS to client over the internet</td>
      <td><li>Settled on a daily basis<br><li>Public network downstream traffic fees = unit price per GB * daily accumulated public network downstream traffic</td>
   </tr>
   <tr>
      <td>Private network downstream traffic</td>
      <td>Traffic generated by data transfer from COS to client over the Tencent Cloud private network</td>
      <td>Free</td>
   </tr>
   <tr>
      <td>CDN origin-pull traffic</td>
      <td>Traffic generated by data transfer from COS to Tencent Cloud CDN edge server</td>
      <td><li>Settled on a daily basis<br><li>CDN origin-pull traffic fees = unit price per GB * daily accumulated CDN origin-pull traffic</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Cross-region replication traffic</td>
      <td>Traffic generated by replication of data in a bucket in one region to another bucket in another region</td>
      <td nowrap="nowrap"><li>Settled on a daily basis <br><li>Cross-region replication traffic fees = unit price per GB * daily accumulated cross-region replication traffic</td>
   </tr>
</table>

> 
>
>- In the same region, Tencent Cloud products automatically communicate with one another over the private network and no traffic fees will be incurred. For more information on how to determine whether the Tencent Cloud private network is used for access, see [Creating Request Overview > COS Access via Private Network and Public Network](https://intl.cloud.tencent.com/document/product/436/30613).
>- Traffic generated by object downloads directly through **object links** and object browsing through **static website access node** is public network downstream traffic.
>- After CDN acceleration is enabled, traffic generated by browsing and downloading COS data from client through the **CDN accelerated domain name** is CDN origin-pull traffic.
>- Traffic generated by replication of data in a bucket in one region to another bucket in another region through the copy API or cross-region replication feature is cross-region replication traffic.

#### Traffic Trends

The figure below shows the traffic fees incurred by data transmitted from COS to end user with CDN acceleration enabled and disabled, respectively.
![](https://main.qcloudimg.com/raw/a09b897cf57944a2648dea7972ecb237.png)

#### Billing Restrictions

1. When archived data is read, the data is first restored to Standard storage class and then read there; therefore, the traffic is counted in the Standard storage class.
2. CDN origin-pull traffic refers to the traffic generated by data transfer from COS to Tencent Cloud CDN edge server. If traffic is forwarded from a third-party origin server to COS, public network downstream traffic will be generated.

<span id="jf5"></span>

### Administrative Feature Fees
Administrative feature fees refers to the cost incurred after the user starts and uses the administrative feature (such as inventory or select feature). At present, administrative feature fees include inventory feature costs and select feature costs.

| Billable Item | Applicable Storage Class | Meaning | Description |
| ---------- | ---------------------- | -------------------------------- | ------------------------------------------------------------ |
| Inventory Feature Cost | Standard storage<br>Standard_IA storage<br>Archive storage | When inventory feature is enabled, cost incurred by listing bucket objects | <li>Settled on a daily basis<br> <li>Billed by every one million objects |
| Select Feature Cost | Standard Storage | When select feature is enabled, cost incurred by scanning objects |<li>Settled on a daily basis<br> <li>Billed by total data size of the scanned objects |


## Billing Cycle

The billing cycle and sequence of the billable items in COS are as detailed below:

<table>
   <tr>
      <th>Billable Item</th>
      <th>Billing Cycle</th>
      <th>Description</th>
      <th>Billing Sequence</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Storage usage fees</td>
      <td rowspan="3">Monthly</td>
      <td rowspan="3">The fees for one month are calculated and billed on the 3rd to 5th day of the following month</td>
      <td nowrap="nowrap">Free tier > pay-as-you-go</td>
   </tr>
   <tr>
      <td>Request fees</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td  nowrap="nowrap">Data retrieval fees</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Traffic fees</td>
      <td>Daily</td>
      <td>The fees for one day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Inventory Feature Cost</td>
      <td>Daily</td>
      <td>The fees for one day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Select Feature Cost</td>
      <td>Daily</td>
      <td>The fees for one day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
</table>

> 
> - At the time of bill settlement, the system will settle in the order of **free tier > pay-as-you-go billing**.
> - By default, the system uses the pay-as-you-go billing method for bill settlement.


### Relevant Links

1. For COS pricing in each billing method, see COS [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
2. For more information on arrears processing in COS, data retention and purge schedule, and billing descriptions, see [Arrears](https://intl.cloud.tencent.com/document/product/436/10044).
3. In the pay-as-you-go billing mode, you can estimate the usage and calculate the fees using the COS [Price Calculator](https://intl.cloud.tencent.com/pricing/cos).

