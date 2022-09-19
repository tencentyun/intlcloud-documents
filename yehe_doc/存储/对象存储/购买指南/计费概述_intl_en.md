This document describes COS billing modes, billable items, billing cycles, and prices.

## Billing Mode

COS is billed on a pay-as-you-go basis as detailed below:

| Billing Mode                                                    | Description                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Pay-as-you-go (postpaid) | This is the default billing mode of COS supported in all regions as described in [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224), where you use resources first and pay later. Fees of various billable items are calculated, settled, deducted, and billed daily. For more information, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/436/32534). |




## Billable Items

Billable items in COS include storage usage, requests, data retrieval, traffic, and management features. For more information, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776).


![](https://qcloudimg.tencent-cloud.cn/raw/f122045a434978ab26cb7c276723fc9d.png)





## Billing Cycle

The billing cycles and sequence of COS billable items are as detailed below:

> ?
>Starting from September 1, 2022, COS storage usage, request, and data retrieval fees are settled daily. For more information, see [Daily Billing for COS Storage Usage, Request, and Data Retrieval](https://intl.cloud.tencent.com/document/product/436/47593).

<table>
   <tr>
      <th colspan=2>Billable Item</td>
      <th>Billing Cycle</td>
      <th>Description</td>
      <th>Billing Sequence</td>
   </tr>
   <tr>
      <td colspan=2>Storage usage fees</td>
      <td>Daily</td>
      <td rowspan=4>Fees for a day are settled and billed the next day.</td>
      <td>Free tier > pay-as-you-go, or only pay-as-you-go in case of no free tier.</td>
   </tr>
   <tr>
      <td rowspan=3>Request fees</td>
      <td colspan=1>Read/Write request fees</td>
      <td rowspan=3>Daily</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=1>DEEP ARCHIVE data retrieval request fees</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=1>INTELLIGENT TIERING object monitoring fees</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td rowspan=3>Data retrieval fees</td>
      <td colspan=1>STANDARD_IA data retrieval fees</td>
      <td rowspan=2>Daily</td>
      <td rowspan=2>Fees for a day are settled and billed the next day.</td>
      <td rowspan=2>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=1>ARCHIVE data retrieval fees</td>
   </tr>
   <tr>
      <td colspan=1>DEEP ARCHIVE data retrieval fees</td>
      <td>Daily</td>
      <td>Fees for a day are settled and billed the next day.</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=2>Traffic fees</td>
      <td>Daily</td>
      <td>Fees for a day are settled and billed the next day.</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td rowspan=4>Management feature fees</td>
      <td colspan=1>Inventory fees</td>
      <td>Daily</td>
      <td>Fees for a day are settled and billed the next day.</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=1>Extraction fees</td>
      <td>Daily</td>
      <td>Fees for a day are settled and billed the next day.</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=1>Batch operation fees</td>
      <td>Daily</td>
      <td>Fees for a day are settled and billed the next day.</td>
      <td>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=1>Object tagging fees</td>
      <td>Daily</td>
      <td>Fees for a day are settled and billed the next day.</td>
      <td>Pay-as-you-go</td>
   </tr>
</table>


## Pricing

You can check the prices of COS billable items at [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).


## References


1. For more information on COS fees calculation and billing in different scenarios, see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).
2. For more information on the COS payment overdue policy (data retention and destruction), see [Payment Overdue](https://intl.cloud.tencent.com/document/product/436/10044).
3. For more information on billing cycles, see [Bill Management](https://www.tencentcloud.com/document/product/555/7430?lang=en&pg=).
4. If you have more questions about COS billing, see [FAQs](https://intl.cloud.tencent.com/document/product/436/32532) or [contact us](https://www.tencentcloud.com/contact-us).

