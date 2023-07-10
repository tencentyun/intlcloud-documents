
Management feature fees are calculated based on the use of COS management features such as inventory and COS Select.

>? For more information on storage classes, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).
> 

<table>
<thead>
<tr>
<th>Billable Item</th>
<th>Applicable Storage Class</th>
<th>Description</th>
<th>Billed By</th>
</tr>
</thead>
<tbody><tr>
<td>Inventory feature</td>
<td nowrap="nowrap">All</td>
<td>Fees incurred from listing bucket objects after the inventory feature is enabled</td>
<td>Pay-as-you-go</li></td>
</tr>
<tr>
<td>COS Select </td>
<td>STANDARD<br>STANDARD_IA</td>
<td>When you use the COS Select feature to extract the content of the specified object, fees will be charged based on the actual amount of data extracted.</td>
<td>Pay-as-you-go</td>
</tr>
<tr>
<td>Batch operation</td>
<td nowrap="nowrap">All</td>
<td>Once you enable the batch operation feature, COS will bill you based on the number of jobs created and objects processed</td>
<td>Pay-as-you-go</td>
</tr>
<tr>
<td>Object tagging</td>
<td nowrap="nowrap">All</td>
<td>Once you enable the object tagging feature, COS will bill you based on the number of object tags set</td>
<td>Pay-as-you-go</td>
</tr>
</tbody></table>



## Billing Mode and Calculation Formula

<table>
   <tr>
      <th>Billed By</th>
      <th>Billable Item</th>
      <th>Calculation Formula</th>
   </tr>
   <tr>
      <td rowspan=4>Pay-as-you-go</td>
      <td>Inventory feature</td>
      <td nowrap="nowrap"><ul  style="margin: 0;"><li>Daily billing cycle</li><li>Inventory fees = number of objects listed / 1 million * unit price</li></ul></td>
   </tr>
   <tr>
      <td>COS Select</td>
      <td nowrap="nowrap"><ul  style="margin: 0;"><li>Daily billing cycle</li><li>Extraction fees = unit price per GB * daily accumulated amount of data extracted</li></ul></td>
   </tr>
   <tr>
      <td>Batch operation</td>
			<td nowrap="nowrap">Batch operation fees include job fees and object processing fees.<ul  style="margin: 0;"><li>Daily billing cycle<br><li>Job fees = number of jobs created * unit price</li><li>Object processing fees = number of objects processed / 10,000 * unit price</li></ul></td>
   </tr>
   <tr>
      <td>Object tagging</td>
			<td nowrap="nowrap"><ul  style="margin: 0;"><li>Daily billing cycle</li><li>Object tagging fees = number of tags / 10,000 * unit price</li></ul></td>
   </tr>
</table>


## Management Feature Pricing

For the unit prices of management features, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).

>! On September 30, 2021, the list prices of the object tagging feature were reduced.
>1. The public cloud prices for regions in and outside the Chinese mainland were reduced to 0.00025817 USD/10,000 tags/day and 0.0003098 USD/10,000 tags/day, respectively.
>2. These prices have taken effect for bills generated starting from October 1, 2021 (i.e., fees incurred after September 30, 2021).
>




## Billing Examples

>? Prices in the following examples are for reference only. For the actual prices, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
>


### Example 1: STANDARD storage usage fees + object tagging fees + request fees

Assume that on November 1, 2020, user A uploaded 10 GB of data to a bucket residing in the Guangzhou region in the STANDARD storage class and added tags for 100,000 objects on the same day, generating 100,000 requests. Apart from these operations, user A did not perform any other operations. As fees for a day were settled the next day, then:

- STANDARD storage usage fees: Settled daily starting from November 2, 2020.
- STANDARD request fees: Settled on November 2, 2020.
- Object tagging fees: Settled on November 2, 2020.

Fees analysis:


- STANDARD storage usage fees = 0.024 USD/GB/month / 30 * 10 GB * 30 days = 0.24 USD
- STANDARD request fees = 0.002 USD/10,000 requests x 100,000 requests = 0.02 USD
- Object tagging fees = 0.00025817 USD/10,000 tags/day * 30 * 100,000 tags = 0.077451 USD

In summary, the total bill for user A in November is calculated as follows: 0.24 + 0.02 + 0.077451 = 0.337451 USD.


### Example 2: STANDARD storage usage fees + extraction fees + request fees

Assume that on November 1, 2020, user A uploaded 10 GB of data to a bucket residing in Guangzhou region in the STANDARD storage class and extracted data of 5 GB on the same day, generating 100,000 requests. Apart from these operations, user A did not perform any other operations. As fees for a day were settled the next day, then:

- STANDARD storage usage fees: Settled daily starting from November 2, 2020.
- STANDARD request fees: Settled on November 2, 2020.
- Extraction fees: Settled on November 2, 2020.

Fees analysis:

- STANDARD storage usage fees = 0.024 USD/GB/month / 30 * 10 GB * 30 days = 0.24 USD
- STANDARD request fees = 0.002 USD/10,000 requests x 100,000 requests = 0.02 USD
 - Extraction fees = 0.0018 USD/GB * 5 GB = 0.009 USD


In summary, the total bill for user A in November is calculated as follows: 0.24 + 0.02 + 0.009 = 0.269 USD.

