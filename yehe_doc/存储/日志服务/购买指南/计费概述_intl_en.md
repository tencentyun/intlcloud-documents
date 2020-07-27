
>!
>- Cloud Log Service (CLS) is currently in beta test and available for free. **The billing is expected to officially start from August 3, 2020 00:00:00**. For more information about the billing rule and standard, see [Billing Mode](#cls) and other chapters below. You can go to the [CLS Console](https://console.cloud.tencent.com/cls) to view the current resource usage.
>- If you want to try out CLS during the beta test period, [click here](https://intl.cloud.tencent.com/apply/p/vi5fj9634if) to submit an application, and we will review your application within 7 business days.
> - Logs shipped to COS will be billed in COS. For more information, see [COS Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).




<span id="cls"></span>

CLS provides the pay-as-you-go billing option in all the supported regions. Users pay what they use daily.

## Billing Mode

| Category     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Billing cycle | Daily. The fees generated for the current day will be settled at 00:00 on the next day. |
| Price | See CLS [Product Pricing](https://intl.cloud.tencent.com/document/product/614/37510)     |



## Billable Items




### Description

#### Traffic billable items

| Traffic billable items   | Description                                                   | Billing formula                                     |
| -------------- | ------------------------------------------------------------ | -------------------------------------------- |
| Write traffic     | Billed by the data volume received by CLS. If you compress and upload logs, write traffic is the actual data volume after the compression ([LogListener](https://intl.cloud.tencent.com/document/product/614/31578) uploads compressed logs by default). | Write traffic fee = unit price per GB * daily accumulated write traffic         |
| Index traffic   | Billed by the data volume generated when CLS constructs an index. Index traffic is generated only after the index is enabled, which depends on the number of fields configured in the index. | Index traffic fee = unit price per GB * daily accumulated index traffic     |
| Private network read traffic | Billed by the downstream traffic generated when the CLS private domain name is accessed.<br>For example, the private network read traffic fee will be incurred when you download CLS logs, export logs, or ship logs to COS or Ckafka over a private network. | Private network read traffic fee = unit price per GB * daily accumulated private network read traffic |
| Public network read traffic | Billed by the downstream traffic generated when the CLS public domain name is accessed.<br>For example, the public network read traffic fee will be incurred when you download CLS logs, export logs, or ship logs to COS or Ckafka over a public network. | Public network read traffic fee = unit price per GB * daily accumulated public network read traffic |

 #### Restrictions

1. Uploading logs always incur the write traffic fee no matter you use a private network or public network.
2. Index traffic will be larger than the original log data since the metadata such as `\_\_FILENAME\_\_` and `\_\_SOURCE__` in CLS constructs indexes and calculates the index traffic.
3. Index traffic will be calculated only once if both the full-text index and key-value index are enabled.

  

#### Storage billable items

| Storage billable items | Description                               | Billing formula                                  |
| ------------ | ---------------------------------------- | ----------------------------------------- |
| Log storage | Billed by the storage usage of the log data. | Log storage fee = unit price per GB * daily average log storage |
| Index storage | Billed by the storage usage of the index data. | Index storage fee = unit price per GB * daily average index storage |

#### Restrictions

1. CLS calculates the log storage based on the data volume actually uploaded. For example, the raw log size is 100 GB,
	 - If **compression is enabled**, and the data volume actually uploaded is 25 GB, the log storage is increased by 25 GB.
	 - If **compression is not enabled**, and the data volume actually uploaded is 100 GB, the log storage is increased by 100 GB.
	 - Similarly, when **Log Index** is enabled and fields generate index traffic of 50 GB, the index storage is increased by 50 GB.
2. The log storage is calculated based on the average. The storage usage values will be collected once every minute, and then, these values will be averaged per day. The average is the daily storage by using the formula below:
 ```plaintext
 Daily log storage= “sum of the log storage values per minute for the day” / 1440
 Daily index storage= “sum of the index storage values per minute for the day” / 1440
 ```
3. The log data and index data are saved based on your configured storage cycle. The expired data no longer incurs a storage fee, and will be deleted on the hour. For example, you set the storage cycle to 3 days and upload logs on June 15 12:15, the logs will be saved during June 15 12:15 and June 18 12:15, and the storage usage will be released on June 18 13:00. (**Do not change the storage cycle frequently, and you can only change it once a day**)
 - **Extending the storage cycle**
After you extend the storage cycle, CLS saves valid data for a longer period. For example, if you extend the storage cycle from 7 days to 15 days on June 15 12:30, the data after June 8 12:00 will be saved to June 23 13:00, rather than being deleted on June 23 13:00.
 - **Shortening the storage cycle**
       After you shorten the storage cycle, CLS saves valid data for a shorter period. For example, you shorten the storage cycle from 15 days to 7 days on June 15, 12:30, the data stored during June 1 12:00 and June 8 13:00 will be deleted on June 15 13:00.


#### Other billable items (on demand)

| Other billable items | Description                                                   | Billing formula                                                     |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Service request | Billed by the total number of CLS API calls.                         | Service request fee = unit price per 1,000,000 requests * (daily accumulated number of requests) / 1000000) |
| Topic partition | Billed by the number of topic partitions occupied, including the read-write topic partitions and read-only partitions. | Topic partition fee = unit price * daily accumulated number of topic partitions                      |

#### Restrictions
1. The service request counts the requests from [LogListener](https://intl.cloud.tencent.com/document/product/614/31578), [API](https://intl.cloud.tencent.com/document/product/614/16907) or CLS API calls via SDK, including read and write requests such as upload and download, creation and deletion, search and analysis.
2. The number of service request will be counted regardless of the request result.

     

## Billing Example

#### Nginx logs query and analysis

Company A’s website receives 100 million requests per day, and each request produces a 100-byte log on average. So there are 100 million logs with a size of about 9.31 GB. Company A decided to upload the Nginx access logs to CLS in the Beijing region, and save them for 15 days for query and statistical analysis.

<table>
   <tr>
      <th colspan="2"><center>Billable Item</center></th>
      <th><center>Measure</center></th>
      <th><center>Quantity</center></th>
      <th nowrap="nowrap"><center>Unit Price (Beijing)</center></th>
      <th nowrap="nowrap"><center>Costs</center></th>
   </tr>
   <tr>
      <td rowspan="4">Traffic fees</td>
      <td>Write traffic</td>
      <td>Use LogListener to compress and upload logs, and consume a traffic of 2.33 GB</td>
      <td>2.33 GB</td>
      <td>0.032 USD/GB/day</td>
      <td>0.075 USD/day</td>
   </tr>
     <tr>
      <td>Index traffic</td>
      <td>After the full-text index is enabled, an index traffic of 11.2 GB will be generated (index traffic is larger than the write traffic)</td>
      <td>11.2 GB</td>
      <td>0.063 USD/GB/day</td>
      <td>0.7056 USD/day</td>
   </tr>
   <tr>
      <td>Private network read traffic</td>
      <td>There is no download or export via a private network. No private network read traffic is generated.</td>
      <td>0 GB</td>
      <td>0.032 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
   <tr>
      <td>Public network read traffic</td>
      <td>There is no download or export via a public network. No public network read traffic is generated.</td>
      <td>0 GB</td>
      <td>0.144 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
   <tr>
      <td rowspan="2">Storage fee</td>
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
      <td>Use Loglistener to batch upload logs and produce 100,000 upload requests</td>
      <td>100,000 requests</td>
      <td>0.027 USD/GB/day</td>
      <td>0.0027 USD/day</td>
   </tr>
   <tr>
      <td>Topic partition rental</td>
      <td>The peak bandwidth for business logs is 8 MB/sec. Two topic partitions are needed.</td>
      <td>2 partitions</td>
      <td>0.06 USD/partition/day</td>
      <td>0.0144 USD/day</td>
   </tr>
   <tr>
      <td colspan="2">Total amount</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>1.3095 USD/day</td>
   </tr>
</table>

