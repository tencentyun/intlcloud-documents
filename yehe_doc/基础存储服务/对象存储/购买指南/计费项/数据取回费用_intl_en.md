Retrieving data stored in the MAZ_STANDARD_IA, STANDARD_IA, ARCHIVE, or DEEP ARCHIVE storage class incurs data retrieval fees, which will be charged by the size of the retrieved data.

>? For more information on storage classes, see [Storage Class Overview](https://www.tencentcloud.com/document/product/436/30925).
> 


## MAZ_STANDARD_IA/STANDARD_IA Data Retrieval Fees

| Billable Item Description | Applicable Storage Class | Applicable Billing Mode |
| ----------------------- | --------------- |------------------- |
| Data stored in MAZ_STANDARD_IA or STANDARD_IA can only be read/downloaded after it is restored. The data retrieval fees are calculated based on the size of the object.                            |      MAZ_STANDARD_IA</br>STANDARD_IA                             | Pay-as-you-go |

## ARCHIVE/DEEP ARCHIVE Data Retrieval Fees

| Billable Item Description | Applicable Storage Class | Applicable Billing Mode |
| ----------------------- | --------------- |------------------- |
| Data stored in ARCHIVE/DEEP ARCHIVE can only be read/downloaded after it is restored to the STANDARD storage class (i.e., generating a copy in STANDARD) </br></br>The following fees may be incurred for different storage classes and restoration modes: <ul style="margin: 0;"><li>ARCHIVE data retrieval fees (expedited)</li><li>ARCHIVE data retrieval fees (standard)</li><li>ARCHIVE data retrieval fees (bulk)</li><li>DEEP ARCHIVE data retrieval fees (standard)</li><li>DEEP ARCHIVE data retrieval fees (bulk)</li></ul> | ARCHIVE</br>DEEP ARCHIVE | Pay-as-you-go |


## Billing Mode and Calculation Formula

<table>
   <tr>
      <th>Billing Mode</td>
      <th>Applicable Billable Item</td>
      <th>Calculation Formula</td>
   </tr>
   <tr>
      <td rowspan=1>Pay-as-you-go</td>
      <td><ul style="margin: 0;"><li>MAZ_STANDARD_IA data retrieval</li><li>STANDARD_IA data retrieval</li><li>ARCHIVE data retrieval</li><li>DEEP ARCHIVE data retrieval</li></ul></td>
      <td><ul style="margin: 0;"><li>Daily billing cycle</li><li>Data retrieval fees = unit price per GB * daily amount of data retrieved</li></ul></td>
   </tr>
</table>


## Data Retrieval Pricing

For the unit prices of data retrieval, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).




## Billing Examples

>?
> - Prices in the following examples are for reference only. For the actual prices, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
> - The storage capacity is calculated in binary, for example, 1 TB = 1024 GB.
> 

### Example: STANDARD_IA storage usage fees + STANDARD_IA data retrieval fees + STANDARD_IA request fees + Public downstream traffic fees

Assume that on November 1, 2020, user B uploaded 5 GB of data to a bucket residing in Guangzhou region in the STANDARD_IA storage class, generating 100 requests. On November 2, user B read the data over the public network with CDN disabled, generating 100 requests. Apart from these operations, user B did not perform any other operations. As fees for a day were settled the next day, then:

- STANDARD_IA storage usage fees: Settled daily starting from November 2, 2020.
- STANDARD_IA Data retrieval fees: Settled on November 2, 2020.
- STANDARD_IA request fees: Settled on November 2 and 3, 2020.
- Public network downstream traffic fees: Settled on November 3, 2020.

As no resource packs are available for data retrievals, an analysis is performed as follows based on the pay-as-you-go billing mode:

Pay-as-you-go:
 - STANDARD_IA storage usage fees = 0.018 USD/GB/month / 30 * 5 GB * 30 days = 0.09 USD
 - STANDARD_IA data retrieval fees = 0.002 USD/GB x 5 GB = 0.01 USD
 - STANDARD_IA request fees = 0.01 USD/10,000 requests * 100 requests / 10,000 * 2 = 0.0002 USD
 - Public downstream traffic fees = 0.1 USD/GB x 5 GB = 0.5 USD

In summary, the total bill for user B in November is calculated as follows: 0.09 + 0.01 + 0.0002 + 0.5 = 0.6002 USD.

