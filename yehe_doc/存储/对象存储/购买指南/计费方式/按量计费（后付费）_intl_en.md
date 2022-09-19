Pay-as-you-go (postpaid) is the default billing mode of COS supported in all regions as described in [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224), where you use resources first and pay later. Fees of various billable items are calculated, settled, deducted, and billed daily.


## Pricing

For pay-as-you-go pricing of COS, see [Pricing | Cloud Object Storage](https://intl.cloud.tencent.com/pricing/cos).

## Billable Items

COS billable items are calculated as follows:
<table>
   <tr>
      <th>Billable Item</th>
      <th>Description</th>
      <th>Calculation Formula</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Storage usage fees</td>
      <td>Calculated based on the storage usage at a unit price that varies by storage class.</td>
      <td nowrap="nowrap"><ul style="margin: 0;"><li>Storage usage fees = monthly unit price / 30 * daily storage usage * number of days</li><li>Daily storage usage = sum of "5-minute usage" / 288 (number of statistical points)</li></ul></td>
   </tr>
   <tr>
      <td>Request fees</td>
      <td>Calculated based on the number of requests at a unit price that varies by storage class.</td>
      <td nowrap="nowrap">Request fees = unit price per 10,000 requests * daily accumulated number of requests / 10,000</td>
   </tr>
   <tr>
      <td>Data retrieval fees</td>
      <td>Calculated based on the volume of data retrieved at a unit price that varies by storage class. This billable item applies when data in the STANDARD_IA or ARCHIVE storage class is downloaded.</td>
      <td nowrap="nowrap">Data retrieval fees = unit price per GB * daily amount of data retrieved</td>
   </tr>
   <tr>
      <td>Traffic fees</td>
      <td>Calculated based on the public network downstream traffic, CDN origin-pull traffic, cross-region replication traffic, and global acceleration traffic at a unit price that varies by traffic type.</td>
      <td nowrap="nowrap">Traffic fees = unit price per GB * daily accumulated traffic</td>
   </tr>
   <tr>
      <td rowspan=4>Management feature fees</td>
      <td rowspan=4>Fees incurred by management features that you enabled and used, including inventory, extraction, batch operation, and object tagging.
      <td nowrap="nowrap">Inventory fees = unit price per million objects listed * number of objects listed / 1 million</td>
   </tr>
   <tr>
      <td nowrap="nowrap">COS extraction fees = unit price per GB * daily accumulated amount of data extracted</td>
   </tr>
   <tr>
			<td nowrap="nowrap">Batch operation fees include job fees and object processing fees.<ul style="margin: 0;">
				<li>Job fees = unit price per job * number of jobs created </li><li>Object processing fees = unit price per 10,000 objects processed * number of objects / 10,000</li></ul></td>
   </tr>
   <tr>
			<td nowrap="nowrap">Object tagging fees = unit price per 10,000 tags * number of tags / 10,000</td>
   </tr>
</table>


> ?For more information on billable items and billing restrictions, see [Traffic Fees](https://intl.cloud.tencent.com/zh/document/product/436/33776).


## Billing Cycle

COS billable items are billed daily as detailed below:

| Billable Item  | Billing Cycle | Description        |
| ------------ | -------- | -------------------------------------- |
| Storage usage fees | Daily | Fees incurred between 00:00 and 23:59:59 on a day are settled the next day.       |
| Request fees | Daily | Fees incurred between 00:00 and 23:59:59 on a day are settled the next day.       |
| Data retrieval fees | Daily | Fees incurred between 00:00 and 23:59:59 on a day are settled the next day.       |
| Traffic fees | Daily | Fees incurred between 00:00 and 23:59:59 on a day are settled the next day.       |
| Management feature fees | Daily | Fees incurred between 00:00 and 23:59:59 on a day are settled the next day.       |

>? Bills in the system may have a certain delay. Daily bills are generated at around 08:00 AM.
>

## Examples

Assume that on March 1, 2019, user A activated COS and uploaded 100 GB of files to the STANDARD storage class in a bucket in Beijing region. On March 15, the user downloaded 10 GB of data over the public network. 10,000 STANDARD read/write requests were generated. Apart from these operations, the user did not perform any other operations in March.

Therefore, the following fees were incurred in March:
- STANDARD storage usage fees: The storage usage fees for 100 GB of data in the month.
- Traffic fees: The public network downstream traffic fees for 10 GB of data in the month.
- Request fee: The request fees for 10,000 STANDARD read/write requests in the month. Among them, uploading data generated STANDARD write requests, and downloading data generated STANDARD read requests.