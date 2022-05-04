Billable requests include **backend requests** generated due to a feature configured and **user requests**. The request fees are billed according to the number of requests sent to COS.

- User requests: include requests sent to COS to upload, download, query, delete, and perform other operations via APIs, SDKs, or the console.
- Backend requests: include requests to delete STANDARD copies (when the restored archived objects expired or after a lifecycle transition), read/write data for cross-bucket replication, and deliver inventory reports.

Requests that incur fees include read/write requests, INTELLIGENT TIERING object monitoring, and requests that are sent to retrieve DEEP ARCHIVE data. The following fees will be incurred if you use the relevant services:

- Object monitoring fees: incurred if you upload an object in the INTELLIGENT TIERING storage class to an INTELLIGENT TIERING−enabled bucket.
- Data retrieval request fees: incurred if you send requests to restore DEEP ARCHIVE data.



>?
>- For the unit prices of requests and request package prices, please see [COS Product Pricing](https://buy.cloud.tencent.com/price/cos).
>- For more information about storage classes, please see [Storage Class Overview](https://cloud.tencent.com/document/product/436/33417).
>

## Read/Write Requests


| Billable Item Description | Applicable Storage Class | Applicable Billing Mode |
| ------------------------------------------------------------ | -------------- | -------------- |
| The number of read/write requests are calculated monthly based on the number of requests sent.</br></br><li>Both successful and failed requests will be counted.</li><li>The minimum number of billable requests is 10,000. Therefore, if the number of monthly accumulated requests is less than 10,000, you will still be billed for 10,000 requests. </li><li>Objects in ARCHIVE and DEEP ARCHIVE cannot be read or downloaded. If you restore objects from ARCHIVE to STANDARD, you will be billed at STANDARD rates; if you restore objects in the DEEP ARCHIVE storage class, you will be billed at DEEP ARCHIVE rates. | All | Pay-as-you-go |

## INTELLIGENT TIERING Object Monitoring Fees

| Billable Item Description | Applicable Storage Class | Applicable Billing Mode |
| ------------------------------------------------------------ | -------------- | -------------- |
| Fees incurred for monitoring the object access patterns. | INTELLIGENT TIERING | Pay-as-you-go |


## Request Fees for Retrieving DEEP ARCHIVE Data



| Billable Item Description | Applicable Storage Class | Applicable Billing Mode |
| ------------------------------------------------------------ | -------------- | -------------- |
| Restoring DEEP ARCHIVE data will incur request fees according to the number of retrieval requests sent.</br></br>The fees for the following two restoration modes are different. You can select one as needed:</br></br><li>Standard</li><li>Bulk</li> | DEEP ARCHIVE | Pay-as-you-go |


## Billing Mode and Calculation Formulas

| Billing Mode | Applicable Billable Item | Calculation Formula |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Pay-as-you-go | Read/Write requests </br> Object monitoring fees (for INTELLIGENT TIERING) </br> Request fees for retrieving DEEP ARCHIVE data</br> | <li>Monthly billing cycle </br><li>Request fees = Unit price per 10,000 requests (or the monitoring count) x Monthly accumulated number of requests/10,000 |


## Billing Example

>?
>- Prices in the example below are for reference only. For the actual prices, please see [COS Pricing](https://buy.cloud.tencent.com/price/cos).
>- Both successful and failed requests are billed.
>- The minimum number of billable requests is 10,000. Therefore, if the number of monthly accumulated requests is less than 10,000, you will still be billed for 10,000 requests.
>

### Example: STANDARD storage usage fees + STANDARD request fees

Assume that on November 1, 2020, user A uploaded 10 GB of data to a bucket residing in the Guangzhou region in the STANDARD storage class and called the `Bucket API` API to query the object list 50,000 times on the same day. Apart from these operations, user A did not perform any other operations in November. As storage usage fees and request fees are calculated and billed on the 1st in the next month, they will be calculated and billed on December 1, 2020 as follows:

 -  Pay-as-you-go:
  -  STANDARD storage usage fees = 0.024 USD/GB/month x 10 GB = 0.24 USD
  -  STANDARD request fees = 0.002 USD/10,000 requests x 50,000 requests = 0.01 USD


In summary, the total bill for user A in November is calculated as follows: 0.24 + 0.01 = 0.25 USD.
