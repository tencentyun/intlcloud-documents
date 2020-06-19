>?This product now supports dynamic pricing query and cost estimation. For more information, please go to the [Pricing Center](https://intl.cloud.tencent.com/pricing/cos/calculator).
## Free Tier

| User | Period | Free Tier     | How to Get |
|---------|---------|---------|------|
| New user | Six months after COS service activation | A certain amount of standard storage capacity is provided by COS free of charge. For more information, please see [Free Tier](https://intl.cloud.tencent.com/document/product/436/6240)     | [Activate COS](https://console.cloud.tencent.com/cos5)

>The free tier is not applicable to STANDARD_IA, ARCHIVE, requests, and traffic and any other non-STANDARD billable items.


## Billing Method

COS is billed on a pay-as-you-go basis as detailed below:

| Billing Method | Supported Regions |
| ------------------ | ------------------------------------------------------------ |
| [Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/436/32534) | For all the available regions, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224). |


## Billable Items

Billable items in COS include storage usage fees, request fees, data retrieval fees, traffic fees, and management feature fees as shown below. For more information, see [Billable Items](https://intl.cloud.tencent.com/document/product/436/33776).

![](https://main.qcloudimg.com/raw/06fa136554627a7df38cd4ffa1b17098.png)

## Billing Cycle

The billing cycle and sequence of the billable items in COS are as detailed below:

<table>
   <tr>
      <th>Billable Item</th>
      <th>Billing Cycle</th>
      <th>Description</th>
      <th>Billing Sequence</th>
   </tr>
   <tr>
      <td>Storage usage fees</td>
      <td rowspan="3">Monthly</td>
      <td rowspan="3">The fees for one month are calculated and billed on the 3rd to 5th day of the following month</td>
      <td>Free tier > pay-as-you-go</td>
   </tr>
   <tr>
      <td>Request fees</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td >Data retrieval fees</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Traffic fees</td>
      <td>Daily</td>
      <td>The fees for one day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Inventory feature fees</td>
      <td>Daily</td>
      <td>The fees for one day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Select feature fees</td>
      <td>Daily</td>
      <td>The fees for one day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Batch operation fees</td>
      <td>Daily</td>
      <td>The fees for one day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td>Object tagging fees</td>
      <td>Daily</td>
      <td>The fees for one day are calculated and billed on the following day</td>
      <td>Pay-as-you-go</td>
   </tr>
</table>



## Related Links


1. For more information on COS fee calculation and billing in different scenarios, please see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).
2. For more information on arrears processing in COS, data retention and purge schedule, and billing descriptions, see COS [Arrears](https://intl.cloud.tencent.com/document/product/436/10044).
3. If you still have any questions about COS billing, please see [FAQs About Billing](https://intl.cloud.tencent.com/document/product/436/32532) for answers.

