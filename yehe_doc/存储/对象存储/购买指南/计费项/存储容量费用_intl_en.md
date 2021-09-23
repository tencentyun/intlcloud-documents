Storage usage refers to the storage used. The rate you are charged depends on the objects′ size and how long you stored them. For different storage classes, the unit price, minimum object size, and minimum storage duration period are different, which will be described below. The actual costs depend on the use case and storage class of the object.

>?
>- For the unit prices of storage usage and storage package prices, please see [COS Product Pricing](https://buy.cloud.tencent.com/price/cos).
>- For more information about storage classes, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).
>



## Storage Usage Fees


### STANDARD storage usage fees     

| Billable Item Description | Applicable Region | Applicable Billing Mode |
| ------------------------------------------------------------ | -------- | -------------- |
| STANDARD storage usage refers to the size of your data stored in the STANDARD storage class. You will be charged depending on the actual STANDARD storage usage and how long you store the data. | All regions | Pay-as-you-go |




### STANDARD_IA storage usage fees  

| Billable Item Description | Applicable Region | Applicable Billing Mode |
| ------------------------------------------------------------ | -------- | -------------- |
| STANDARD_IA storage usage refers to the size of your data stored in the STANDARD_IA storage class. You will be charged depending on the actual use case:<br><br><li>Objects stored less than 30 days will be calculated as 30 days. A single object smaller than 64 KB will be calculated as 64 KB, while objects larger than or equal to 64 KB will be billed based on their actual sizes.<br><li>If you successfully uploaded an object to STANDARD_IA without enabling Versioning, COS will delete the existing object (if any) that has the same name. In this case, storage usage fees will be incurred for the **early deletion of the object**. | All regions | Pay-as-you-go |



### INTELLIGENT TIERING storage usage fees   

| Billable Item Description | Applicable Region | Applicable Billing Mode |
| ------------------------------------------------------------ | ---------------------- | -------------- |
| INTELLIGENT TIERING storage usage refers to the size of your data stored in the INTELLIGENT TIERING storage class. You will be charged depending on the actual use case:<br><br><li>The storage usage fees vary depending on the tier your objects are stored. If your objects are stored in the frequent access tier, you will be charged at STANDARD rates. Alternatively, if your objects are stored in the infrequent access tier, you will be charged at STANDARD_IA rates.<br><li>Objects smaller than 64 KB will always be stored in the frequent access tier.<br><li>Objects stored less than 30 days will be calculated as 30 days. All objects, regardless of their sizes, will be billed based on their actual sizes. | Beijing, Shanghai, Guangzhou, Chongqing | Pay-as-you-go |




### ARCHIVE storage usage fees       

| Billable Item Description | Applicable Region | Applicable Billing Mode |
| ------------------------------------------------------------ | ---------- | -------------- |
| ARCHIVE storage usage refers to the size of your data stored in the ARCHIVE storage class. You will be charged depending on the actual use case:<br><br><li>Objects stored less than 90 days will be calculated as 90 days. A single object smaller than 64 KB will be calculated as 64 KB, while objects larger than or equal to 64 KB will be billed based on their actual sizes.<br><li>If you successfully uploaded an object to ARCHIVE without enabling Versioning, COS will delete the existing object (if any) that has the same name. In this case, storage usage fees will be incurred for the **early deletion of the object**. | All regions | Pay-as-you-go |


### DEEP ARCHIVE storage usage fees  

| Billable Item Description | Applicable Region | Applicable Billing Mode |
| ------------------------------------------------------------ | ---------------------- | -------------- |
| DEEP ARCHIVE storage usage refers to the size of your data stored in the DEEP ARCHIVE storage class. You will be charged depending on the actual use case:<br><br><li>Objects stored less than 180 days will be calculated as 180 days. A single object smaller than 64 KB will be calculated as 64 KB, while objects larger than or equal to 64 KB will be billed based on their actual sizes.<br><li>If you successfully uploaded an object to DEEP ARCHIVE without enabling Versioning, COS will delete the existing object (if any) that has the same name. In this case, storage usage fees will be incurred for the **early deletion of the object**. | Beijing, Shanghai, Guangzhou, Chengdu | Pay-as-you-go |


## Billing Mode and Calculation Formula

| Billing Mode | Calculation Formula |
| -------- | ------------------------------------------------------------ |
| Pay-as-you-go | <li>Monthly billing cycle<br><li>Storage usage fees = Unit price x Monthly storage usage<br><li>Monthly storage usage = Sum of the "daily storage usage" in the month/Number of days in the month<br><li>Daily storage usage = Sum of the "5-minute usage"/288 (number of statistical points) |




## Billing Examples

>?
>- Prices in the examples below are for reference only. For the actual prices, please see [COS Pricing](https://buy.cloud.tencent.com/price/cos).
>- The storage capacity is calculated in binary. For example, 1 TB = 1,024 GB.
>- The minimum number of billable requests is 10,000. Therefore, if the number of monthly accumulated requests is less than 10,000, you will still be billed for 10,000 requests, regardless of whether the request succeeds or fails.

### Example 1: STANDARD storage usage fees + STANDARD request fees

Assume that on November 1, 2020, user A uploaded 10 GB of data to a bucket residing in the Guangzhou region in the STANDARD storage class, generating 100 requests. Apart from this, user A did not perform any other operations in November. As storage usage fees and request fees are calculated and billed on the 1st in the next month, the storage usage and request fees will be calculated and billed on December 1, 2020, as follows:

- Pay-as-you-go:
 - STANDARD storage usage fees = 0.024 USD/GB/month x 10 GB = 0.24 USD
 - STANDARD request fees = 0.002 USD/10,000 requests x 10,000 requests = 0.02 USD

In summary, the total bill for user A in November is calculated as follows: 0.24 + 0.02 = 0.26 USD.


### Example 2: STANDARD_IA storage usage fees + STANDARD_IA request fees

Assume that on November 1, 2020, user B uploaded 10 GB of data (i.e. 10,000 pieces of 34 KB objects) to a bucket residing in the Guangzhou region in the STANDARD_IA storage class, generating 100 requests. Apart from this, user B did not perform any other operations in November. As storage usage fees and request fees are calculated on the 1st in the next month, the storage usage fees and request fees will be calculated and billed on December 1, 2020 as follows:

- Pay-as-you-go:
   - STANDARD_IA storage usage = 10 GB + 10,000 x 30 KB = 10.286 GB
   - STANDARD_IA storage usage fees = 0.018 USD/GB/month x 10.286 GB = 0.19 USD
   - STANDARD_IA request fees = 0.01 USD/10,000 requests x 10,000 requests = 0.01 USD


In summary, the total bill for user B in November is calculated as follows: 00.19 + 0.01 = 0.2 USD.
