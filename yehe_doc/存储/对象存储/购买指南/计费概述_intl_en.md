## Free Tier

| Target User | Free Period         | Free Tier                                                     | How to Get It                                                     |
| -------- | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| New user | Six months after COS service activation | A limited amount of STANDARD storage usage is provided automatically by COS free of charge after COS service activation. For more information, please see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240) | [Activate COS](https://console.cloud.tencent.com/cos5) |

> !The free tier only applies to STANDARD storage. It is not applicable to other billable items, including STANDARD_IA/ARCHIVE storage, requests and traffic.


## Billing Method

COS is billed on a pay-as-you-go basis as detailed below:

| Billing Method                                                    | Description                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/436/32534) | This is the default COS billing method. For all the available regions, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) |

## Pricing

COS adopts **pay-as-you-go pricing**. For more information on COS pricing, please see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).


## Billable Items
Billable items in COS include storage usage, requests, data retrievals, traffic, and management features as shown below. For more information, please see [Billable Items](https://intl.cloud.tencent.com/document/product/436/33776).


![](https://main.qcloudimg.com/raw/0fa513bdc13eca45712fb9db34d3b232.png)





## Billing Cycles

The billing cycle and sequence of COS fees are as detailed below:

<table>
   <tr>
      <th colspan=2>Billable Item</td>
      <th>Billing Cycle</td>
      <th>Description</td>
      <th>Billing Sequence</td>
   </tr>
   <tr>
      <td colspan=2>Storage usage fees</td>
      <td>Monthly</td>
      <td rowspan=4>The fees for one month are deducted on the 1st day of the following month and billed on the 3rd to 5th day of the following month</td>
      <td>Free tier > Pay-as-you-go, or only pay-as-you-go in case of no free tier</td>
   </tr>
   <tr>
      <td rowspan=3>Request fees</td>
      <td>Read/Write request fees</td>
      <td rowspan=3>Monthly</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Retrieve request fees in DEEP ARCHIVE</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Object monitoring fees in INTELLIGENT TIERING</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td rowspan=3>Data retrieval fees</td>
      <td>STANDARD_IA</td>
      <td rowspan=2>Monthly</td>
      <td rowspan=2>The fees for one month are deducted on the 1st day of the following month and billed on the 3rd to 5th day of the following month</td>
      <td rowspan=2>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
   </tr>
   <tr>
      <td>DEEP ARCHIVE</td>
      <td>Daily</td>
      <td>Fees for the day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=2>Traffic fees</td>
      <td>Daily</td>
      <td>Fees for the day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td rowspan=4>Management feature fees</td>
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
2. For more information on the COS overdue policy, data retention and the purge schedule, please see COS [Payment Overdue](https://intl.cloud.tencent.com/document/product/436/10044).
3. You can estimate the usage of and calculate your pay-as-you-go COS fees using the COS [Price Calculator](https://buy.cloud.tencent.com/price/cos/calculator).
4. If you have any further questions about COS billing, please see [Billing FAQs](https://intl.cloud.tencent.com/document/product/436/32532) for answers.
