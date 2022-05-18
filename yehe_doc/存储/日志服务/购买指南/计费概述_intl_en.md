<span id="cls"></span>
CLS is a pay-as-you-go service which bills you according to actual resource usage and deduct fees on a daily basis. If an account has overdue payment, CLS will isolate its existing resources, prohibit operations such as log upload and query, and terminate related resources and data 15 days later.

>?
> - CLS was officially commercialized at 00:00:00 on August 3, 2020. After the commercialization, CLS still provides a [free tier](https://intl.cloud.tencent.com/document/product/614/37889) for all users in each region.
> - If you know the resource usage and need to know the cost estimate, use the [Price Calculator](https://buy.cloud.tencent.com/price/cls/calculator) to export the cost estimate list.
>

## Billing Mode

| Category     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Billing cycle | Daily. The fees generated for the current day will be settled at 00:00 on the next day. |
| Price | See CLS [Product Pricing](https://intl.cloud.tencent.com/document/product/614/37510). |


## Billable items

### Overview

CLS has the following billable items in different billing modes. The index traffic, log storage, and index storage fees are subject to the log storage class. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/614/42003).

![](https://qcloudimg.tencent-cloud.cn/raw/3e19ac671121afbf7b5054fb06668d5c.png)

Billable item in each step of log data processing in CLS are as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/1dc8c2a90dc3fb1b828f63a80f8f421b.png)


### Detailed description

#### Traffic fees

| Billable Item | Description | Billing Formula |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Write traffic | Write traffic fees will be incurred when a log is uploaded or processed data is shipped to the target log topic. They are calculated by the volume of the data received by CLS and don't distinguish between traffic over private and public networks. <br />**Note**: <br />If logs are compressed before upload, the fees will be calculated by the actual data volume after compression ([LogListener](https://intl.cloud.tencent.com/document/product/614/31578) compresses logs for upload by default). For example, if the raw log data volume is 4 GB and the compression ratio is 1:4 (which is subject to the actual log content and ranges from 1:4 to 1:10 generally), the write traffic after compression will be 1 GB. | Write traffic fees = unit price per GB * daily accumulative write traffic                       |
| Standard/IA index traffic | Index traffic fees incurred during standard/IA index generation are billed by the volume of data generated when CLS creates indexes.<br />**Note**: <br /><ul  style="margin: 0;"><li>Index traffic will be generated only after index is enabled.</li><li>In CLS, key-value indexes will be automatically created for built-in reserved fields such as `\_\_FILENAME\_\_` and `\_\_SOURCE\_\_`, but no index traffic will be calculated for them.</li><li>The index traffic is irrelevant to log compression during upload, and the volume of uncompressed raw log data shall prevail. For example, if the raw log data volume is 4 GB and the write traffic is 1 GB after compression (the compression ratio is 1:4), the index traffic will be 4 GB after full-text index is enabled.</li><li>If both full-text index and key-value index are enabled, the index traffic won't be calculated twice, and only the full-text index (i.e., full-text size of logs) will be used to calculate the index traffic. If only key-value index is enabled, the index traffic is subject to the number of fields with key-value index enabled and the size of the field values; for example, if the raw log data volume is 4 GB and the size of fields and field values with key-value index enabled is 2 GB, the corresponding index traffic will be 2 GB. You can [reduce the product costs](https://intl.cloud.tencent.com/document/product/614/45245) by appropriately configuring the key-value index field.</li><li>The standard traffic and IA traffic have different unit prices and are billed respectively.</li></ul> | Standard index traffic fees = unit price per GB * daily accumulative standard index traffic<br /><br />IA index traffic fees = unit price per GB * daily accumulative IA index traffic |
| Private network read traffic | Billed by the downstream traffic generated when the CLS private domain name is accessed.<br>For example, private network read traffic fees will be incurred when you consume logs or ship logs to COS or CKafka over the private network. Log search and analysis via the console or API don't incur any read traffic or fees. | Private network read traffic fees = unit price per GB * daily accumulated private network read traffic |
| Public network read traffic | Billed by the downstream traffic generated when the CLS public domain name is accessed.<br>For example, public network read traffic fees will be incurred when you download CLS logs, consume logs, or ship logs to COS or CKafka over the public network. Log search and analysis via the console or API does not incur any read traffic or fees. | Public network read traffic fees = unit price per GB * daily accumulated public network read traffic |


#### Storage fees

| Billable Item | Description | Billing Formula |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Standard/IA log storage | Such fees are charged by the standard/IA storage space occupied by the log data.<br />**Note:**<br />If logs are compressed before upload, the fees will be calculated by the actual data volume after compression ([LogListener](https://intl.cloud.tencent.com/document/product/614/31578) compresses logs for upload by default). For example, if the raw log data volume is 4 GB and the compression ratio is 1:4 (which is subject to the actual log content and ranges from 1:4 to 1:10 generally), the incremental log storage capacity will be 1 GB. | Standard log storage fees = unit price per GB * daily average standard log storage capacity<br /><br />IA log storage fees = unit price per GB * daily average IA log storage capacity |
| Standard/IA index storage | Such fees are billed by the standard/IA storage space occupied by the index data.<br />**Note:**<br />The index storage capacity is irrelevant to log compression during upload, and the volume of uncompressed raw log data shall prevail. For example, if the raw log data volume is 4 GB and the write traffic is 1 GB after compression (the compression ratio is 1:4), the index traffic will be 4 GB after full-text index is enabled, and the incremental index storage capacity will be 4 GB. | Standard index storage fees = unit price per GB * daily average standard index storage capacity<br /><br />IA index storage fees = unit price per GB * daily average IA index storage capacity |

1. Standard/IA logs and indexes have different storage prices and are billed separately.
2. Storage is billed based on average usage. Storage usage values are collected on each hour, and averaged per day.
3. The log data and index data are saved based on your configured storage cycle. Expired data does not incur storage fees and will be deleted on the hour. For example, assume that the storage cycle is set to 3 days and logs are uploaded at 12:15 on June 15. The logs will be saved between 12:15 on June 15 and 12:15 on June 18, and the expired data will be deleted at 13:00 on June 18. **Do not change the storage cycle frequently, and you can only change it once a day.**
   - **Extending the storage cycle**
   When you extend the storage cycle, CLS will save the data for a longer period. For example, if you extend the storage cycle from 7 days to 15 days at 12:30 on June 15, the data uploaded at 12:00 on June 8 will be saved until 13:00 on June 23, instead of being deleted at 13:00 on June 15.
   - **Shortening the storage cycle**
       When you shorten the storage cycle, CLS will save the data for a reduced period. For example, if you shorten the storage cycle from 15 days to 7 days at 12:30 on June 15, the data uploaded between 12:00 on June 1 and 13:00 on June 8 will be deleted at 13:00 on June 15.



#### Computing fees

| Billable Item | Description | Billing Formula |
| ------------ | ------------------------------------------------------------ | ------------------------------------ |
| Data processing | Such fees are billed by the data volume of logs processed by the data processing feature.<br />**Note:**<br />The log data volume is irrelevant to log compression during upload, and the volume of uncompressed raw log data shall prevail. For example, if the raw log data volume is 4 GB and the compression ratio is 1:4 (which is subject to the actual log content and ranges from 1:4 to 1:10 generally), the write traffic after compression will be 1 GB, but the data volume for data processing will still be 4 GB. | Data processing fees = unit price * processed data volume |



#### Other fees

| Billable Item | Description | Billing Formula |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Service request | Such fees are billed by the total number of CLS API calls, including those initiated in the Tencent Cloud console and via LogListener, APIs, and SDKs for log upload, search, and analysis. | Service request fees = unit price per one million requests * (daily accumulative number of requests / 1000000) |
| Topic partition | Such fees are billed by the number of topic partitions used, including the read-write topic partitions and read-only partitions. | Topic partition fees = unit price * daily accumulated number of topic partitions                      |

The service request and topic partition fees have low unit prices and only account for a very small part of the total fees if you use CLS normally. Such fees are mainly used to prevent abuse such as high numbers of meaningless concurrent API calls.



## Billing Examples

#### NGINX log query and analysis

Company A's website receives 100 million requests per day, and each request produces a 100-byte log on average. This results in 100 million logs per day for a total of approximately 9.31 GB. Company A decides to upload the NGINX access logs to the CLS service in the Beijing region and save them in the STANDARD storage class for 15 days. Log search, analysis, and alarming features are used, while data processing, download, consumption, and shipping features are not used.

<table>
<thead>
<tr><th>Billable Item</th><th>Description</th><th>Usage</th><th>Unit Price</th><th>Fees</th></tr>
</thead>
<tbody><tr>
<td>Write traffic</td>
<td>Logs are compressed at a compression ratio of about 1:4 when uploaded via LogListener, and the traffic after compression is about 2.33 GB.</td>
<td>9.31 GB * (1:4) = 2.33 GB</td>
<td>0.032 USD/GB/day</td>
<td>0.07456 USD/day</td>
</tr>
<tr>
<td>Standard index traffic</td>
<td>Full-text index is enabled, that is, index is enabled for all fields, which generates 9.31 GB index traffic.</td>
<td>9.31 GB * 100% = 9.31 GB</td>
<td>0.062 USD/GB/day</td>
<td>0.57722 USD/day</td>
</tr>
<tr>
<td>Standard log storage</td>
<td>9.31 GB logs are uploaded every day, which take up about 2.33 GB storage space after compression. The average volume of logs stored for 15 days is 34.95 GB.</td>
<td>9.31 GB * (1:4) * 15 = 34.95 GB</td>
<td>0.0024 USD/GB/day</td>
<td>0.08388 USD/day</td>
</tr>
<tr>
<td>Standard index storage</td>
<td>9.31 GB indexes are generated every day. The average storage capacity after 15 days is 139.65 GB.</td>
<td>9.31 GB * 15 = 139.65 GB</td>
<td>0.0024 USD/GB/day</td>
<td>0.33516 USD/day</td>
</tr>
<tr>
<td>Service request</td>
<td>LogListener is used to batch upload logs in groups, producing about 100,000 upload requests.</td>
<td>100,000 requests</td>
<td>0.026 USD/million requests/day</td>
<td>0.0026 USD/day</td>
</tr>
<tr>
<td>Topic partition</td>
<td>The business log peak is 8 MB/s, so two topic partitions are required.</td>
<td>2 partitions</td>
<td>0.007 USD/partition/day</td>
<td>0.014 USD/day</td>
</tr>
<tr>
<td>Total</td>
<td colspan=4>1.08742 USD/day</td>
</tr>
</tbody></table>


As you can see from the billable items, the index traffic and storage fees are the major fees for the following reasons:

- Index is the core of log search and analysis. Log data cannot be searched for if there are no indexes. Therefore, the unit price of the index traffic (0.062 USD/GB/day) is higher than that of the write traffic (0.032 USD/GB/day).
- If logs are compressed when uploaded, the write traffic and log storage capacity will be calculated based on the compressed log data volume, while the index traffic and storage capacity will be calculated based on the data volume of uncompressed raw logs. As the log compression ratio generally ranges from 1:4 to 1:10, the index traffic and storage capacity will be about 4–10 times the write traffic and log storage capacity respectively.

Therefore, to reduce the product costs, you can appropriately adjust the index configuration to reduce the index traffic and storage capacity.

If a raw log is:
```
10.20.20.10 ::: [Tue Jan 22 14:49:45 CST 2019 +0800] ::: GET /online/sample HTTP/1.1 ::: 127.0.0.1 ::: 200 ::: 647 ::: 35 ::: http://127.0.0.1/
```
The log will be captured as the following fields during log collection:
```
IP: 10.20.20.10
bytes: 35
host: 127.0.0.1
length: 647
referer: http://127.0.0.1/
request: GET /online/sample HTTP/1.1
status: 200
time: [Tue Jan 22 14:49:45 CST 2019 +0800]
```

- If full-text index is enabled, the index generated by the log will be 172 bytes in size (i.e., size of all field keys and values). The index traffic will be generated, and the storage capacity will be used accordingly.
- If you don't enable full-text index and only enable key-value index for the `request` and `status` fields, the indexes generated by the log will be 48 bytes in size (i.e., size of the key and value of `request` and `status`, which are 48 bytes / 172 bytes = 27.9% of all fields). In this way, the index traffic and storage capacity will be reduced to 27.9% of those for full-text index. However, you can only use the `request` and `status` fields to search for and analyze logs and view other fields in this case.

For more methods to reduce product costs, see [Saving Product Use Costs](https://intl.cloud.tencent.com/document/product/614/45245).

