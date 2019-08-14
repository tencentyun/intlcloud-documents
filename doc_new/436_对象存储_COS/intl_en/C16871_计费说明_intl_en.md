## Billing Method

COS is pay-as-you-go, so you only pay for what you use. 

Pay-as-you-go is applicable to all COS service regions. To learn more about COS service regions, see [Region and Access Domain Name](https://intl.cloud.tencent.com/document/product/436/6224).

## Billing Cycle

You can see from the following graph that COS billing includes storage capacity cost, request cost, data retrieval cost and traffic cost.

![](https://main.qcloudimg.com/raw/41bce47bb77bf1b44b0076388a4a8e7f.png)

Storage capacity cost, request cost and data retrieval cost are calculated on a monthly basis. The previous month's bill will be generated between the 3rd and 5th day of each month.

Traffic cost is billed on a **daily** basis. The previous day's usage is calculated for the bill.

The cost is billed in the order of Free quota > Pay-as-you-go by default.

### Free quota

Users who activated COS will receive a certain amount of free standard storage capacity. For more information about free quota, see [Free Quota](https://intl.cloud.tencent.com/document/product/436/6240).

### Related links

1. For more information about the COS product pricing for different billing methods, see [COS Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
2. Account arrears and COS service suspension: to learn more about data retention, termination time and related billing descriptions, see [COS Arrears](https://intl.cloud.tencent.com/document/product/436/10044).
3. Under pay-as-you-go billing method, users can estimate the usage by themselves and calculate the approximate cost via [COS Cost Calculator](https://buy.cloud.tencent.com/price/cos/calculator).


<a id="package"></a>

## Billing Items

COS billing includes storage capacity cost, request cost, data retrieval cost and traffic cost. Their detailed descriptions are shown below. To learn more about pricing, see [COS Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).

### Storage capacity cost

Storage capacity cost is billed based on storage capacity consumed. Storage capacity refers to the actual usage occupied by user data. See below for its metric and billing description.

| Storage Capacity Metric | Applicable Storage Type | Metric Description | Billing Description |
| ---------------- | -------------- | -------------------------------------- | ------------------------------------------------------------ |
| Storage Capacity | All | Calculated based on the actual storage capacity occupied by user data | Monthly<br />Storage capacity cost = Unit price of storage capacity * Storage per month<br />Storage per month = The total of average storage per day / Number of days of the month<br/>Average storage per day = The total of average storage capacity every 5 minutes of the day / 288 (sampling points) |

#### Billing limits

1. COS Infrequent Access: Storage time less than 30 days is calculated as 30 days. If an object is less than 64KB, it is calculated as 64KB. If not, it is calculated as its actual size.
2. Archive Storage: Storage time less than 90 days is calculated as 90 days. If an object is less than 64KB, it is calculated as 64KB. If not, it is calculated as its actual size.
3. If you upload an object with the **same name** in infrequent or archive storage class without the version control feature enabled, COS will delete the existed object of the same name after you upload it successfully. The **object deleted in advance** will still be billed as the minimum storage time.

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

#### Billing limits
**Infrequent storage** and **archive storage** are storage classes for cold data. You need to retrieve objects first if you want to download and use the objects in these two storage classes. Therefore, both traffic cost for downloading data and data retrieval cost incurred.   

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

>- Tencent Cloud products within the same region access each other over a private network by default and no traffic fee is charged for these connections. For details about how to determine whether it is an access via private network, please see [COS Access via Private Network and Public Network](https://intl.cloud.tencent.com/document/product/436/30613#cos-access-via-private-network-and-public-network). 
>- Public network downstream traffic refers to the traffic generated by directly downloading an object through its object link or browsing an object through a static website access node.
>- CDN origin-pull traffic refers to traffic generated by browsing or downloading COS data from the client through CDN acceleration domain name after CDN acceleration is enabled.
>- Cross-region replication traffic refers to traffic generated by sending data between buckets in different regions through the replication API or cross-region replication feature.

#### Traffic trends
The traffic costs incurred when data transfer from COS to users with or without CDN acceleration enabled are shown below. 
![](https://main.qcloudimg.com/raw/af94a944fd1d9fb71be295f8db0f10f3.png)

#### Billing limits

To read Archive Storage data, restore the data to COS Standard and then read it from COS Standard. So the traffic is counted into COS Standard.
