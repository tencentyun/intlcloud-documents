>!
> - Cloud Log Service (CLS) was officially commercialized at 00:00:00 on August 03, 2020. After the commercialization, CLS still provides a free tier for all users in each region. For more information, please see [Free Tier](https://intl.cloud.tencent.com/document/product/614/37889).
> - For more information about the billing rules and standards, please see [Billing Mode](#.E8.AE.A1.E8.B4.B9.E6.96.B9.E5.BC.8F) and other chapters below. To view the current resource usage, go to the [CLS console](https://console.cloud.tencent.com/cls/overview?region=ap-guangzhou).  
> - If you know the resource usage and need to know the cost estimate, use the [Price Calculator](https://buy.cloud.tencent.com/price/cls/calculator) to export the cost estimate list.
> 

<span id="cls"></span>
CLS is a pay-as-you-go service which bills you according to actual resource usage and deduct fees on a daily basis. Pay-as-you-go billing applies to all available regions. If an account has overdue payment, CLS will isolate its existing resources, prohibit operations such as log upload and query, and terminate related resources and data 15 days later.

## Billing Mode

| Category     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Billing cycle | Daily. The fees generated for the current day will be settled at 00:00 on the next day. |
| Price | See CLS [Product Pricing](https://intl.cloud.tencent.com/document/product/614/37510)     |



## Billable Items

### Overview


![](https://main.qcloudimg.com/raw/177d97d23b8bccc5190dc9cec01bc6af.png)

### Graphic illustration

![](https://qcloudimg.tencent-cloud.cn/raw/ddc794095b1a38f57fb076342216facf.png)


### Description

#### Traffic billable items

| Traffic billable items   | Description                                                   | Billing formula                                     |
| -------------- | ------------------------------------------------------------ | -------------------------------------------- |
| Write traffic     | Billed by the data volume received by CLS. If you compress and upload logs, write traffic will be the actual data volume after the compression. [LogListener](https://intl.cloud.tencent.com/document/product/614/31578) uploads compressed logs by default. | Write traffic fees = unit price per GB * daily accumulated write traffic         |
| Index traffic   | Billed by the data volume generated when CLS constructs an index. Index traffic is generated only after the index is enabled, and is dependent on the number of fields configured in the index. | Index traffic fees = unit price per GB * daily accumulated index traffic     |
| Private network read traffic | Billed by the downstream traffic generated when the CLS private domain name is accessed.<br>For example, private network read traffic fees will be incurred when you download CLS logs, consume logs, or ship logs to COS or CKafka over a private network. Log search and analysis via the console or API does not incur any read traffic or fees. | Private network read traffic fees = unit price per GB * daily accumulated private network read traffic |
| Public network read traffic | Billed by the downstream traffic generated when the CLS public domain name is accessed.<br>For example, public network read traffic fees will be incurred when you download CLS logs, consume logs, or ship logs to COS or CKafka over a public network. Log search and analysis via the console or API does not incur any read traffic or fees. | Public network read traffic fees = unit price per GB * daily accumulated public network read traffic |

 #### Restrictions

1. Uploading logs always incurs write traffic fees regardless of whether you use a private or public network. In addition to network traffic, a large volume of data processing and calculation is involved in log writing and index construction, regardless of private or public network. Therefore, these fees are included in the traffic fees.
2. In CLS, metadata such as `\_\_FILENAME\_\_` and `\_\_SOURCE\_\_` constructs indexes but no index traffic is calculated.
3. Index traffic will be calculated only once if both the full-text index and key-value index are enabled.

  

#### Storage billable items

| Storage billable items | Description                               | Billing formula                                  |
| ------------ | ---------------------------------------- | ----------------------------------------- |
| Log storage | Billed by log data storage usage. | Log storage fees = unit price per GB * daily average log storage |
| Index storage | Billed by index data storage usage. | Index storage fees = unit price per GB * daily average index storage |

#### Restrictions

1. CLS calculates log storage based on the uploaded data volume. For example, suppose the raw log size is 100 GB:
	 - If **compression is enabled**, and the data volume uploaded is 25 GB, the log storage is increased by 25 GB.
	 - If **compression is not enabled**, and the data volume uploaded is 100 GB, the log storage is increased by 100 GB.
	 - Similarly, when **Log Index** is enabled and fields generate index traffic of 50 GB, the index storage is increased by 50 GB.
2. Log storage is billed based on average usage. Storage usage values are collected per minute, and averaged per day. The calculation formula is as follows:
 - Daily log storage= "sum of the log storage values per minute for the day" / 1440
 - Daily index storage= "sum of the index storage values per minute for the day" / 1440
3. The log data and index data are saved based on your configured storage cycle. Expired data does not incur storage fees and will be deleted on the hour. For example, suppose the storage cycle is set for 3 days and logs are uploaded on June 15 12:15. The logs will be saved between June 15 12:15 and June 18 12:15, and the data will be deleted on June 18 13:00. **Do not change the storage cycle frequently, and you can only change it once a day**
 - **Extending the storage cycle**
When you extend the storage cycle, CLS will save the data for a longer period. For example, if you extend the storage cycle from 7 days to 15 days on June 15 12:30, the data uploaded on June 8 12:00 will be saved to June 23 13:00, instead of being deleted on June 15 13:00.
 - **Shortening the storage cycle**
       When you shorten the storage cycle, CLS saves data for a reduced period. For example, if you shorten the storage cycle from 15 days to 7 days on June 15, 12:30, the data uploaded between June 1 12:00 and June 8 13:00 will be deleted on June 15 13:00.


#### Other billable items (on demand)

| Other billable items | Description                                                   | Billing formula                                                     |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Service request | Billed by the total number of CLS API calls.                         | Service request fees = unit price per 1,000,000 requests * (daily accumulated number of requests / 1000000) |
| Topic partition | Billed by the number of topic partitions used, including the read-write topic partitions and read-only partitions. | Topic partition fees = unit price * daily accumulated number of topic partitions                      |

#### Restrictions
1. Service request counts the requests from [LogListener](https://intl.cloud.tencent.com/document/product/614/31578), [API](https://intl.cloud.tencent.com/document/product/614/42757) or CLS API calls via SDK. This includes read and write requests such as upload and download, creation and deletion, search and analysis.
2. Service requests will be counted regardless of the request result.

     

## Billing Example

#### NGINX logs query and analysis

Company A's website receives 100 million requests per day, and each request produces a 100-byte log on average. This results in 100 million logs with a total size of approximately 9.31 GB per day. Company A decides to upload the NGINX access logs to CLS in the Beijing region, and save them for 15 days for query and statistical analysis.

<table>
   <tbody><tr>
      <th colspan="2"><center>Billable Item</center></th>
      <th><center>Measurement Description</center></th>
      <th width="13%">Measurement Amount</th>
      <th width="20%">Unit Price (Beijing)</th>
      <th nowrap="nowrap"><center>Fees</center></th>
   </tr>
   <tr>
      <td rowspan="4">Traffic fees</td>
      <td>Write traffic</td>
      <td>LogListener is used to compress and upload logs, resulting in 2.33 GB traffic consumption</td>
      <td>2.33 GB</td>
      <td>0.032 USD/GB/day</td>
      <td>0.075 USD/day</td>
   </tr>
     <tr>
      <td>Index traffic</td>
      <td>Full-text index is enabled, generating an index traffic of 11.2 GB (index traffic is larger than the write traffic)</td>
      <td>11.2 GB</td>
      <td>0.063 USD/GB/day</td>
      <td>0.7056 USD/day</td>
   </tr>
   <tr>
      <td>Private network read traffic</td>
      <td>There is no download or consumption via a private network. No private network read traffic is generated.</td>
      <td>0 GB</td>
      <td>0.032 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
   <tr>
      <td>Public network read traffic</td>
      <td>There is no download or consumption via a public network. No public network read traffic is generated.</td>
      <td>0 GB</td>
      <td>0.144 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
   <tr>
      <td rowspan="2">Storage fees</td>
      <td>Log storage</td>
      <td>Logs of 2.33 GB are uploaded every day. The average storage capacity after 15 days is 34.95 GB (2.33 GB * 15 days)</td>
      <td>34.95 GB</td>
      <td nowrap="nowrap">0.0025 USD/GB/day</td>
      <td nowrap="nowrap">0.088 USD/day</td>
   </tr>
   <tr>
      <td>Index storage</td>
      <td>Indexes of 11.2 GB are generated every day. The average storage capacity after 15 days is 168 GB (11.2 GB * 15 days)</td>
      <td>168 GB</td>
      <td>0.0025 USD/GB/day</td>
      <td nowrap="nowrap">0.42 USD/day</td>
   </tr>
   <tr>
      <td rowspan="2">Other fees</td>
      <td>Service request</td>
      <td>LogListener is used to upload logs in batches, producing 100,000 upload requests</td>
      <td>100,000 requests</td>
      <td>0.027 USD/million requests/day</td>
      <td>0.0027 USD/day</td>
   </tr>
   <tr>
      <td>Topic partition tenant fees</td>
      <td>The peak bandwidth for business logs is 8 MB/sec. Two topic partitions are needed.</td>
      <td>2 partitions</td>
      <td>0.0072 USD/partition/day</td>
      <td>0.0144 USD/day</td>
   </tr>
   <tr>
      <td colspan="2">Total amount</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>1.3095 USD/day</td>
   </tr>
</tbody></table>

