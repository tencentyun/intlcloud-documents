Retrieving data stored in STANDARD_IA, ARCHIVE, or DEEP ARCHIVE incurs data retrieval fees, which will be charged according to the size of the data retrieved.

>?
>- For the unit prices of data retrievals, please see [COS Product Pricing](https://buy.cloud.tencent.com/price/cos).
>- For more information about storage classes, please see [Storage Class Overview](https://cloud.tencent.com/document/product/436/33417).
>


## STANDARD_IA Data Retrieval Fees

| Billable Item Description | Applicable Storage Class | Applicable Billing Mode |
| ------------------------------------------------------------ | -------------- | -------------- |
| Data stored in STANDARD_IA can only be read/downloaded after it is restored. The data retrieval fees are calculated based on the size of the object. | STANDARD_IA | Pay-as-you-go |

## ARCHIVE/DEEP ARCHIVE Data Retrieval Fees

| Billable Item Description | Applicable Storage Class | Applicable Billing Mode |
| ------------------------------------------------------------ | ------------------------- | -------------- |
| Data stored in ARCHIVE/DEEP ARCHIVE can only be read/downloaded after it is restored to the STANDARD storage class (i.e. generating a replica in STANDARD) </br></br>The following fees might be incurred for different storage classes and restoration modes: <li>ARCHIVE data retrieval fees (expedited)<br><li>ARCHIVE data retrieval fees (standard)</li><li>ARCHIVE data retrieval fees (bulk)</li><li>DEEP ARCHIVE data retrieval fees (standard)</li><li>DEEP ARCHIVE data retrieval fees (bulk)</li> | ARCHIVE</br>DEEP ARCHIVE | Pay-as-you-go |


## Billing Mode and Calculation Formula

<table>
   <tr>
      <th>Billing Mode</td>
      <th>Applicable Billable Item</td>
      <th>Calculation Formula</td>
   </tr>
   <tr>
      <td rowspan=2>Pay-as-you-go</td>
      <td><li>STANDARD_IA data retrievals</li><li>ARCHIVE data retrievals</li></td>
      <td><li>Monthly billing cycle<br><li>Data retrieval fees = Unit price per GB x Monthly amount of data retrieved</td>
   </tr>
   <tr>
      <td>DEEP ARCHIVE data retrievals</td>
      <td><li>Daily billing cycle<br><li>Data retrieval fees = Unit price per GB x Daily amount of data retrieved</td>
   </tr>
</table>


## Billing Example

>?
>- Prices in the example below are for reference only. For the actual prices, please see [COS Pricing](https://buy.cloud.tencent.com/price/cos).
>- The storage capacity is calculated in binary, for example, 1 TB = 1,024 GB.
>- The minimum number of billable requests is 10,000. Therefore, if the number of monthly accumulated requests is less than 10,000, you will still be billed for 10,000 requests, regardless of whether the request succeeds or fails.
>

### Example: STANDARD_IA storage usage fees + STANDARD_IA data retrieval fees + STANDARD_IA request fees + Public downstream traffic fees

Assume that on November 1, 2020, user B uploaded 5 GB of data to a bucket residing in the Guangzhou region in the STANDARD_IA storage class. On November 2, user B read the data over a public network with CDN disabled. A total of 100 requests were generated. Apart from these operations, user B did not perform any other operations in November. As storage usage fees, request fees, and data retrieval fees are calculated monthly, they will be billed on December 1, 2020. Traffic fees are calculated daily and will thus be billed on November 3, 2020. Therefore, the fees are calculated as follows:

Pay-as-you-go:
 - STANDARD_IA storage usage fees = 0.018 USD/GB/month x 5 GB = 0.09 USD
 - STANDARD_IA data retrieval fees = 0.002 USD/GB x 5 GB = 0.01 USD
 - STANDARD_IA request fees = 0.01 USD/10,000 requests x 10,000 requests = 0.01 USD
 - Public downstream traffic fees = 0.1 USD/GB x 5 GB = 0.5 USD

In summary, the total bill for user B in November is calculated as follows: 0.09 + 0.01 + 0.01 + 0.5 = 0.65 USD.
