Management feature fees are calculated based on the use of COS management features such as inventory and COS Select.

>?
>- For the unit prices of the management feature, see [COS Product Pricing](https://buy.cloud.tencent.com/price/cos).
>- For more information about storage classes, see [Storage Class Overview](https://cloud.tencent.com/document/product/436/33417).
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
<td>Inventory feature</td>
<td nowrap="nowrap">All</td>
<td>Fees incurred from listing bucket objects after the inventory feature is enabled</td>
<td>Pay-as-you-go</li></td>
</tr>
<tr>
<td>COS Select </td>
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
      <td nowrap="nowrap"><li>Daily billing cycle<br><li>Inventory fees = Number of objects listed/1 million x Unit price</td>
   </tr>
   <tr>
      <td>COS Select</td>
      <td nowrap="nowrap"><li>Daily billing cycle<br><li>COS Select fees = Unit price per GB x Daily accumulated extraction traffic</td>
   </tr>
   <tr>
      <td>Batch operation</td>
			<td nowrap="nowrap">Batch operation fees include job fees and object processing fees<li>Daily billing cycle<br><li>Job fees = Number of jobs created x Unit price<br><li>Object processing fees = number of objects processed/10,000 x Unit price</td>
   </tr>
   <tr>
      <td>Object tagging</td>
			<td nowrap="nowrap"><li>Daily billing cycle<br><li>Object tagging fees = Number of tags/10,000 x Unit price</td>
   </tr>
</table>

## Billing Example

>? Prices in the example below are for reference only. For the actual prices, please see [COS Pricing](https://buy.cloud.tencent.com/price/cos).
>


### Example: STANDARD storage usage fees + Object tagging fees + Request fees

Assume that on November 1, 2020, user A uploaded 10 GB of data to a bucket residing in the Guangzhou region in the STANDARD storage class and added tags for 100,000 objects on the same day, generating 100,000 requests. Apart from these operations, user A did not perform any other operations in November. As storage usage fees and request fees are calculated monthly, they will be billed on December 1, 2020. Tagging fees are calculated daily and will thus be billed on November 2, 2020. Therefore, the fees will be calculated as follows:

Pay-as-you-go:
 - STANDARD storage fees = 0.024 USD/GB/month x 10 GB = 0.24 USD
 - Object tagging fees = 0.01 USD/10,000 tags x 100,000 tags = 0.1 USD
 - STANDARD request fees = 0.002 USD/10,000 requests x 100,000 requests = 0.02 USD

In summary, the total bill for user A in November is calculated as follows: 0.24 + 0.1 + 0.02 = 0.36 USD.
