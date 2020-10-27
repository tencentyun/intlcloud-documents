## Free Tier

| User | Period         | Free Tier                                                     | How to Get                                                     |
| -------- | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| New user | Six months after COS service activation | A limited amount of STANDARD storage usage is provided by COS free of charge. For more information, please see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240) | [Activate COS](https://console.cloud.tencent.com/cos5) |

> !The free tier is not applicable to any other billable items, including STANDARD_IA/ARCHIVE storage usage, requests, and traffic, than STANDARD usage.


## Billing Method

COS is billed on a pay-as-you-go basis as detailed below:

| Billing Method                                                    | Supported Regions                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/436/32534) | For all the available regions, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). |

## Pricing

COS adopts **pay-as-you-go pricing**. For more information on COS pricing, see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).


## Billable Items
Billable items in COS include storage usage, requests, data retrievals, traffic, and management features as shown below. For more information, see [Billable Items](https://intl.cloud.tencent.com/document/product/436/33776).


![](https://main.qcloudimg.com/raw/b87a461353ac429b9ce4fb507f2a3367.png)





## Billing Cycle

The billing cycle and sequence of COS fees are as detailed below:

<table>
   <tr>
      <th>Billable Item</th>
      <th>Billing Cycle</th>
      <th>Description</th>
      <th>Billing Sequence</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Storage usage fees</td>
      <td rowspan="3">Monthly</td>
      <td rowspan="3">The fees for one month are calculated and billed on the 3rd to 5th day of the following month</td>
      <td nowrap="nowrap">Free tier > Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Request fees<br>(including retrieve requests to DEEP ARCHIVE)</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td  nowrap="nowrap">Data retrieval fees<br>(excluding DEEP ARCHIVE)</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td >Data retrieval fees in DEEP ARCHIVE</td>
      <td>Daily</td>
      <td>Fees for the day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Traffic</td>
      <td>Daily</td>
      <td>Fees for the day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
	 <tr>
      <td>Inventory feature fees</td>
      <td>Daily</td>
      <td>Fees for the day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Select feature fees</td>
      <td>Daily</td>
      <td>Fees for the day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Batch operation fees</td>
      <td>Daily</td>
      <td>Fees for the day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Object tagging fees</td>
      <td>Daily</td>
      <td>Fees for the day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
</table>





## Related Links


1. For more information on COS fee calculation and billing in different scenarios, please see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).
2. For more information on arrears processing in COS, data retention and purge schedule, see COS [Arrears](https://intl.cloud.tencent.com/document/product/436/10044).
3. In the pay-as-you-go billing mode, you can estimate the usage and calculate the fees using the COS [Price Calculator](https://buy.cloud.tencent.com/price/cos/calculator).
4. If you have any further questions about COS billing, please see [FAQs About Billing](https://intl.cloud.tencent.com/document/product/436/32532) for answers.