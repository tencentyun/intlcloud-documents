## Billing Method

COS is pay-as-you-go. You only pay for what you use. 

The Pay-as-You-Go mode is applicable to all regions where COS provides services. For more information about COS regions, see [Region and Access Domain Name](https://intl.cloud.tencent.com/document/product/436/6224).

## Billing Cycle

COS billable items include storage capacity, number of requests, data retrieval and data traffic as shown below:

![](https://main.qcloudimg.com/raw/7b300699fde9e41d9035c7015f1e867f.png)

The storage capacity, number of requests and data retrieval are billed on a **monthly** basis. The billing is done between the third and fifth day of each month. During this time, the previous month's fee is calculated to generate the bill.

The data traffic is billed on a **daily** basis. The previous day’s fee is calculated to generate the bill.

The cost is billed in the order of **Free quota > Pay-as-you-go**.

-  The free quota is deducted first, and any exceeding usage is billed on a **Pay-as-you-go** basis.

### Free quota

Users who activated COS will receive a certain amount of free standard storage capacity. For more information about free quota, see [Free Quota](https://intl.cloud.tencent.com/document/product/436/6240).

### Related links

1. For more information about the COS product pricing for different billing methods, see [COS Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
2. About account arrears and COS service suspension: For more information about data retention, termination time, and related billing details, see [COS Arrears](https://intl.cloud.tencent.com/document/product/436/10044).
3. With pay-as-you-go, users can also estimate your usage and calculate the specific price with the [COS Price Calculator](https://buy.cloud.tencent.com/price/cos/calculator).

<a id="package"></a>

## Billing Items

COS billing items include storage capacity, number of requests, data retrieval and data traffic. The following shows the detailed description about billing items. For more information about pricing, see [COS Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).

### Storage capacity

Storage capacity refers to the actual storage space occupied by user data. Its fee is calculated based on the storage capacity consumed. Metric and billing description of storage capacity are shown as follows:

| Storage Capacity Metric | Applicable Storage Type | Metric Description | Billing Description |
| ---------------- | -------------- | -------------------------------------- | ------------------------------------------------------------ |
| Storage Capacity | All | Calculated based on the actual storage capacity occupied by user data | Monthly<br />Storage capacity cost = Unit price of storage capacity * Storage per month<br />Storage per month = The total of average storage per day / Number of days of the month<br/>Average storage per day = The total of average storage capacity every 5 minutes of the day / 288 (sampling points) |

#### Billing limits

1. COS Infrequent Access: Storage time less than 30 days is calculated as 30 days. Storage size less than 64 KB is calculated as 64 KB.
2. Archive Storage: Only in Mainland China. Storage time less than 90 days is calculated as 90 days. Storage size less than 48KB is calculated as 48KB.

### Number of requests

Users can perform upload, download, query, deletion and other operations on data via API, SDK, console or related tool programs by sending request instructions to Tencent COS. The fee is calculated based on the number of requests.

Requests are divided into read requests and write requests. The unit price of requests per month is the same for all request types and varies between different storage types. The more the requests, the higher the fee, and vice versa. The following shows the metric and billing description for requests:

| Request Metric | Applicable Storage Type | Metric Description | Billing Description |
| ------------ | -------------- | ------------------------------------ | ------------------------------------------------------------ |
| Number of requests | All | Calculated based on the number of request instructions sent | Monthly<br />The number of requests per month less than 10,000 is calculated by 10,000 requests.<br />Request cost = Price of 10,000 requests * Number of requests per month / 10,000 (rounded down) |

#### Billing limits

1. The request fee is billed at a minimum of 10,000 requests. The number of requests per month less than 10,000 is calculated by 10,000 requests.
2. To read Archive Storage data, restore the data to COS Standard and then read it from COS Standard. So the number of requests is counted into COS Standard.

### Data retrieval

The fee is calculated based on the amount of data retrieved. The larger the amount of data retrieved, the higher the fee, and vice versa. The following shows the metric and billing description for data retrieval:

| Data Retrieval Metric | Applicable Storage Type | Metric Description | Billing Description |
| ---------------- | ---------------------- | -------------------------------- | ------------------------------------------------------ |
| Data Retrieval | COS Infrequent Access<br />Archive Storage | Calculated based on the amount of data retrieved | Monthly<br />Data retrieval cost = Unit price per GB * Amount of data retrieved per month |

### Traffic

Traffic is the value of the data traffic accumulated when the user reads the stored data. The following shows the metric and billing description for traffic:

| Traffic Metric | Applicable Storage Type | Metric Description | Billing Description |
| -------------- | -------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| Public network upstream traffic | All | Traffic generated by sending data from a client to COS over the Internet | Free |
| Private network upstream traffic | All | Traffic generated by sending data from a client to COS through the private network of Tencent Cloud | Free |
| Public network downstream traffic | All | Traffic generated by sending data from COS to a client over the Internet | Daily<br />Public network downstream traffic = Unit price per GB * Public network downstream traffic accumulated per day |
| Private network downstream traffic | All | Traffic generated by sending data from COS to a client through the private network of Tencent Cloud | Free |
| CDN origin-pull traffic | All | Traffic generated by sending data from COS to a CDN edge server | Daily<br />CDN origin-pull traffic = Unit price per GB * CDN origin-pull traffic accumulated per day |
| Cross-region replication traffic | All | Traffic generated by sending data between buckets in different regions | Daily<br />Cross-region replication traffic = Unit price per GB * cross-region replication traffic accumulated per day |

-  Different Tencent Cloud products within the same region access each other over a private network by default and no traffic fee is charged for these connections. For more information about how to determine whether the private network is used, see [Private Network Access](https://cloud.tencent.com/document/product/436/31315#.E5.86.85.E7.BD.91.E4.B8.8E.E5.A4.96.E7.BD.91.E8.AE.BF.E9.97.AE).
-  Public network downstream traffic refers to the traffic generated by directly downloading an object through its **object link** or browsing an object through a **static website access node**.
-  CDN origin-pull traffic refers to traffic generated by browsing or downloading COS data from the client through **CDN acceleration domain name** after CDN acceleration is enabled.
-  Cross-region replication traffic refers to traffic generated by sending data between buckets in different regions through the replication API or cross-region replication feature.

#### Billing limits

To read Archive Storage data, restore the data to COS Standard and then read it from COS Standard. So the traffic is counted into COS Standard.

