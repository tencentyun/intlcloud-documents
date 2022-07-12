Billable requests include **user requests** and **backend requests** generated after you configure a feature. The request fees are billed by the number of requests sent to COS.

- User requests: Include requests sent to COS to upload, download, query, delete, and perform other operations via APIs, SDKs, or the console.
- Backend requests: Include requests to delete STANDARD copies (when the restored archived objects expired or after a lifecycle transition), read/write data for cross-bucket replication, and deliver inventory reports.

Requests that incur fees include read/write requests, INTELLIGENT TIERING object monitoring, and requests that are sent to retrieve DEEP ARCHIVE data. The following fees will be incurred if you use relevant services:
- Object monitoring fees: Incurred if you upload an object in the INTELLIGENT TIERING storage class to an INTELLIGENT TIERING-enabled bucket, which will be billed by the number of uploaded objects.
- Data retrieval request fees: Incurred if you send requests to restore DEEP ARCHIVE data.


>? For more information on storage classes, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).
> 

## Read/Write Request Fees

<table>
<thead>
<tr><th style="width: 65%;">Billable Item Description</th><th style="width: 16%;">Applicable Storage Class</th><th style="width: 19%;">Applicable Billing Mode</th></tr>
</thead>
<tbody>
<tr>
<td>Fees incurred by the monthly total number of sent read/write requests. <ul  style="margin: 0;"><li>Both successful and failed requests are billed. </li><li>The minimum number of requests for billing is 10,000. </li><ul style="margin: 0;"><li>If the monthly number of requests is less than 10,000, fees will be calculated based on the actual number of requests. </li><li>If the monthly request fees don't reach the minimum deduction value, the request fees will be 0 on the bill. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/10373">FAQs</a>. </li></ul></li><li>Data in ARCHIVE and DEEP ARCHIVE storage classes cannot be directly read or downloaded. <ul style="margin: 0;"><li>If you directly access ARCHIVE or DEEP ARCHIVE data not restored yet, a request error will be reported, but the request will still be billed as an ARCHIVE/DEEP ARCHIVE read/write request. For more information, see <a href="https://buy.cloud.tencent.com/price/cos">Pricing | Cloud Object Storage</a>. </li><li>If you restore an object in ARCHIVE, a copy will be generated in the STANDARD storage class, which will be billed at the STANDARD storage usage price. If you access the copy, a read/write request will be generated, which will be billed at the STANDARD read/write request price. </li><li>If you restore an object in DEEP ARCHIVE, a copy will be generated in the STANDARD storage class, which will be billed at the STANDARD storage usage price. If you access the copy, a read/write request will be generated, which will be billed at the DEEP ARCHIVE read/write request price. </li></ul></td>
<td>All</td>
<td>Pay-as-you-go</td>
</tr>
</tbody></table>


## INTELLIGENT TIERING Object Monitoring Fees

<table>
<thead>
<tr><th style="width: 65%;">Billable Item Description</th><th style="width: 16%;">Applicable Storage Class</th><th style="width: 19%;">Applicable Billing Mode</th></tr>
</thead>
<tbody>
<tr>
<td>Fees incurred by monitoring the access to INTELLIGENT TIERING objects.</td>
<td>INTELLIGENT TIERING</td>
<td>Pay-as-you-go</td>
</tr>
</tbody></table>

## DEEP ARCHIVE Data Retrieval Request Fees

<table>
<thead>
<tr><th style="width: 65%;">Billable Item Description</th><th style="width: 16%;">Applicable Storage Class</th><th style="width: 19%;">Applicable Billing Mode</th></tr>
</thead>
<tbody><tr>
<td>Restoring DEEP ARCHIVE data will incur request fees by the number of retrieval requests sent.<br/>The fees for the following two restoration modes are different. You can select one as needed:<ul  style="margin: 0;"><li>Standard</li><li>Bulk</li></ul></td>
<td>DEEP ARCHIVE</td>
<td>Pay-as-you-go</td>
</tr>
</tbody></table>


## Billing Mode and Calculation Formulas

| Billing Mode  | Applicable Billable Items | Calculation Formula |
|-----|--------|------|
|  Pay-as-you-go   |    Read/Write requests </br> INTELLIGENT TIERING object monitoring </br> DEEP ARCHIVE object retrieval requests  </br>      |  <ul  style="margin: 0;"><li>Monthly  </li><li>Request fees = unit price per 10,000 requests (or monitored objects) * monthly accumulated number of requests (or monitored objects) / 10,000 </li></ul>       |


## Request Pricing

For the unit prices of requests, see [Pricing | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos).

## Billing Examples

>?
> - Prices in the example below are for reference only. For the actual prices, see [Pricing | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos).
> - Both successful and failed requests are billed.
> - The minimum number of requests for billing is 10,000. Therefore, if the number of monthly accumulated requests is less than 10,000, you will still be billed for 10,000 requests.
>

### Example: STANDARD storage usage fees + STANDARD request fees

Assume that on November 1, 2020, user A uploaded 10 GB of data to a bucket residing in Guangzhou region in the STANDARD storage class and called the `Bucket API` API to query the object list 50,000 times on the same day. Apart from these operations, user A did not perform any other operations in November. As storage usage fees and request fees are calculated and billed on the first day in the next month, they will be calculated and billed on December 1, 2020 as follows:

Pay-as-you-go:
  -  STANDARD storage usage fees = 0.024 USD/GB/month * 10 GB = 0.24 USD
  -  STANDARD request fees = 0.002 USD/10,000 requests * 50,000 requests = 0.01 USD


In summary, the total bill for user A in November is calculated as follows: 0.24 + 0.01 = 0.25 USD.
