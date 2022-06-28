
Management feature fees are calculated based on the use of COS management features such as inventory and COS Select.

>? For more information on storage classes, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).
> 

<table>
<thead>
<tr>
<th>Billable Item</th>
<th>Applicable Storage Class</th>
<th>Description</th>
<th>Billing Mode</th>
</tr>
</thead>
<tbody><tr>
<td>Inventory</td>
<td nowrap="nowrap">All</td>
<td>Fees incurred from listing bucket objects after the inventory feature is enabled</td>
<td>Pay-as-you-go</li></td>
</tr>
<tr>
<td >COS Select</td>
<td>STANDARD<br>STANDARD_IA</td>
<td>Fees incurred from extracting objects when the COS Select feature is enabled</td>
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
      <th>Billing Mode</th>
      <th>Billable Item</th>
      <th>Calculation Formula</th>
   </tr>
   <tr>
      <td rowspan=4>Pay-as-you-go</td>
      <td>Inventory</td>
      <td nowrap="nowrap"><li>Daily billing cycle<br><li>Inventory fees = number of objects listed/1 million * unit price</td>
   </tr>
   <tr>
      <td>COS Select</td>
      <td nowrap="nowrap"><li>Daily billing cycle<br><li>COS Select fees = unit price per GB * daily accumulated extraction traffic</td>
   </tr>
   <tr>
      <td>Batch operation</td>
			<td nowrap="nowrap">Batch operation fees include job fees and object processing fees<li>Daily billing cycle<br><li>Job fees = number of jobs created * unit price<br><li>Object processing fees = number of objects processed / 10,000 * unit price</td>
   </tr>
   <tr>
      <td>Object tagging</td>
			<td nowrap="nowrap"><li>Daily billing cycle<br><li>Object tagging fees = number of tags / 10,000 * unit price</td>
   </tr>
</table>


## Management Feature Pricing

For the unit prices of management features, see [Pricing | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos).

>! On September 30, 2021, the list prices of the object tagging feature were reduced.
>1. The public cloud prices for regions in and outside the Chinese mainland were reduced to 0.00025817 USD/10,000 tags/day and 0.0003098 USD/10,000 tags/day, respectively.
>2. These prices have taken effect for bills generated starting from October 1, 2021 (i.e., fees incurred after September 30, 2021).
>




## Billing Examples

>? Prices in the example below are for reference only. For the actual prices, see [Pricing | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos).
>


### Example: STANDARD storage usage fees + object tagging fees + request fees

Assume that on November 1, 2020, user A uploaded 10 GB of data to a bucket residing in the Guangzhou region in the STANDARD storage class and added tags for 100,000 objects on the same day, generating 100,000 requests. Apart from these operations, user A did not perform any other operations in November. As storage usage fees and request fees are calculated monthly, they will be billed on December 1, 2020. Tagging fees are calculated daily and will thus be billed on November 2, 2020. Therefore, the fees will be calculated as follows:

-  Pay-as-you-go:
 -  STANDARD storage usage fees = 0.024 USD/GB/month * 10 GB = 0.24 USD
 - Object tagging fees = 0.00025817 USD/10,000 tags/day * 30 * 100,000 tags = 0.077451 USD
 - STANDARD request fees = 0.002 USD/10,000 requests * 100,000 requests = 0.02 USD

In summary, the total bill for user A in November is calculated as follows: 0.24 + 0.077451 + 0.02 = 0.337451 USD.
