## Billing Method

COS is pay-as-you-go, so you only pay for what you use. 

Pay-as-you-go is applicable to all COS service regions. To learn more about COS service regions, see [Region and Access Domain Name](https://intl.cloud.tencent.com/document/product/436/6224).

## Billing Cycle

You can see from the following graph that COS billing includes storage capacity cost, request cost, data retrieval cost and traffic cost.

![](https://main.qcloudimg.com/raw/2e2c45b9c4752c0c5ea5e49ad335b23f.png)

Storage capacity cost, request cost and data retrieval cost are calculated on a monthly basis. The previous month's bill will be generated between the 3rd and 5th day of each month.

Traffic cost is billed on a **daily** basis. The previous day's usage is calculated for the bill.

Free quota will be applied before pay-as-you-go billing.

### Free quota

Users who activated COS will receive a certain amount of free standard storage capacity. For more information about free quota, see [Free Quota](https://intl.cloud.tencent.com/document/product/436/6240).

### Related links

1. For more information about the COS product pricing for different billing methods, see [COS Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
2. Account arrears and COS service suspension: to learn more about data retention, termination time and related billing descriptions, see [COS Arrears](https://intl.cloud.tencent.com/document/product/436/10044).
3. You can estimate your pay-as-you-go usage and prices using [COS Price Calculator](https://buy.cloud.tencent.com/price/cos/calculator).

<a id="package"></a>

## Billing Items

COS billing includes storage capacity cost, request cost, data retrieval cost and traffic cost. Their detailed descriptions are shown below. To learn more about pricing, see [COS Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).

### Storage capacity cost

Storage capacity cost is billed based on storage capacity consumed. Storage capacity refers to the actual usage occupied by user data. See below for its metric and billing description.

| Storage Capacity Metric | Applicable Storage Type | Metric Description | Billing Description |
| ---------------- | -------------- | -------------------------------------- | ------------------------------------------------------------ |
| Storage Capacity | All | Calculated based on the actual storage capacity occupied by user data | Monthly<br />Storage capacity cost = Unit price of storage capacity * Storage per month<br />Storage per month = The total of average storage per day / Number of days of the month<br/>Average storage per day = The total of average storage capacity every 5 minutes of the day / 288 (sampling points) |

#### Billing limits

1. COS Infrequent Access: Storage time less than 30 days is calculated as 30 days. Storage size less than 64 KB is calculated as 64 KB.
2. Archive Storage: Only in Mainland China. Storage time less than 90 days is calculated as 90 days. Storage size less than 48KB is calculated as 48KB.

### Requests cost

Requests cost is billed based on the number of requests. Users can perform upload, download, query, deletion and other data-related operations via API, SDK, console or related tool programs by sending request instructions to Tencent COS. 

Requests are divided into read requests and write requests. The unit price of requests per month is the same for all request types and varies between different storage types. The more the requests, the higher the fee, and vice versa. The following shows the metric and billing description for requests:

| Request Metric | Applicable Storage Type | Metric Description | Billing Description |
| ------------ | -------------- | ------------------------------------ | ------------------------------------------------------------ |
| Number of requests | All | Calculated based on the number of request instructions sent | Monthly<br />The number of requests per month less than 10,000 is calculated by 10,000 requests.<br />Request cost = Price of 10,000 requests * Number of requests per month / 10,000 (rounded down) |

#### Billing limits

1. The request fee is billed at a minimum of 10,000 requests. Requests less than 10,000 per month  is calculated as 10,000.
2. To read Archive Storage data, restore the data to COS Standard and then read it from COS Standard. So the number of requests is counted into COS Standard.

### Data retrieval cost

The fee is calculated based on the amount of data retrieved. The larger the amount of data retrieved, the higher the fee, and vice versa. The following shows the metric and billing description for data retrieval:

| Data Retrieval Metric | Applicable Storage Type | Metric Description | Billing Description |
| ---------------- | ---------------------- | -------------------------------- | ------------------------------------------------------ |
| Data Retrieval | COS Infrequent Access<br />Archive Storage | Calculated based on the amount of data retrieved | Monthly<br />Data retrieval cost = Unit price per GB * Amount of data retrieved per month |

### Traffic cost

Traffic is the accumulated data traffic when user reads stored data. The following shows its metric and billing description:

| Traffic Metric | Applicable Storage Type | Metric Description | Billing Description |
| -------------- | -------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| Public network upstream traffic | All | Traffic generated by sending data from a client to COS over the Internet | Free |
| Private network upstream traffic | All | Traffic generated by sending data from a client to COS through the private network of Tencent Cloud | Free |
| Public network downstream traffic | All | Traffic generated by sending data from COS to a client over the Internet | Daily<br />Public network downstream traffic = Unit price per GB * Public network downstream traffic accumulated per day |
| Private network downstream traffic | All | Traffic generated by sending data from COS to a client through the private network of Tencent Cloud | Free |
| CDN origin-pull traffic | All | Traffic generated by sending data from COS to a CDN edge server | Daily<br />CDN origin-pull traffic = Unit price per GB * CDN origin-pull traffic accumulated per day |
| Cross-region replication traffic | All | Traffic generated by sending data between buckets in different regions | Daily<br />Cross-region replication traffic = Unit price per GB * cross-region replication traffic accumulated per day |


-  Public network downstream traffic refers to the traffic generated by directly downloading an object through its **object link** or browsing an object through a **static website access node**.
-  CDN origin-pull traffic refers to traffic generated by browsing or downloading COS data from the client through **CDN acceleration domain name** after CDN acceleration is enabled.
-  Cross-region replication traffic refers to traffic generated by sending data between buckets in different regions through the replication API or cross-region replication feature.

#### Billing limits

To read Archive Storage data, restore the data to COS Standard and then read it from COS Standard. So the traffic is counted into COS Standard.

