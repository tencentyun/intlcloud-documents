This document describes COS billing modes, billable items, billing cycles, and prices.

## Billing Modes

COS supports two billing modes: pay-as-you-go (postpaid) and resource pack (prepaid).

| Billing Mode                                                    | Description                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Pay-as-you-go (postpaid) | This is the default billing mode of COS supported in all regions as described in [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224), where you use resources first and pay later. Fees of various billable items are calculated, settled, deducted, and billed daily. For more information, see [Pay-As-You-Go](https://www.tencentcloud.com/document/product/436/32534). |
| Resource pack (prepaid) | COS offers different types of prepaid resource packs for different billable items. Your actual usage will be first deducted from your resource packs, and any excess will be billed in a pay-as-you-go manner. Resource packs are available only in public cloud regions, not in finance cloud regions. For more information, see [Resource Pack (Prepaid)](https://www.tencentcloud.com/document/product/436/54353). |



## Billable Items

COS billable items include [storage usage](https://intl.cloud.tencent.com/document/product/436/40099), [requests](https://intl.cloud.tencent.com/document/product/436/40100), [data retrievals](https://intl.cloud.tencent.com/document/product/436/40097), [traffic](https://intl.cloud.tencent.com/document/product/436/33776), and [management features](https://intl.cloud.tencent.com/document/product/436/40098). The details are as shown below:



![](https://qcloudimg.tencent-cloud.cn/raw/f122045a434978ab26cb7c276723fc9d.png)


## Billing Cycle

The billing cycles and sequence of COS billable items are as detailed below:

> ?
>- For more information on the validity period of COS resource packs and usage deduction, see [Resource Pack (Prepaid)](https://www.tencentcloud.com/document/product/436/54353).
>- Starting from September 1, 2022, COS storage usage, request, and data retrieval fees are settled daily. For more information, see [Daily Billing for COS Storage Usage, Request, and Data Retrieval](https://intl.cloud.tencent.com/document/product/436/47593).

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
      <td rowspan=1>Fees for a day are billed and settled the next day.</td>
      <td>Free tier > Resource pack > Pay-as-you-go, or only pay-as-you-go in case of no free tier and resource packs</td>
   </tr>
   <tr>
      <td rowspan=3>Request fees</td>
      <td colspan=1>Read/Write request fees</td>
      <td rowspan=3>Daily</td>
      <td rowspan=3>Fees for a day are billed and settled the next day.</td>
      <td>Resource pack > Pay-as-you-go</td>
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
      <td rowspan=3>Daily</td>
      <td rowspan=3>Fees for a day are billed and settled the next day.</td>
      <td rowspan=3>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=1>ARCHIVE data retrieval fees</td>
   </tr>
   <tr>
      <td colspan=1>DEEP ARCHIVE data retrieval fees</td>
   </tr>
   <tr>
      <td colspan=2>Traffic fees</td>
      <td>Daily</td>
      <td>Fees for a day are billed and settled the next day.</td>
      <td>Resource pack > Pay-as-you-go</td>
   </tr>
   <tr>
      <td rowspan=4>Management feature fees</td>
      <td colspan=1>Inventory fees</td>
      <td rowspan=4>Daily</td>
      <td rowspan=4>Fees for a day are billed and settled the next day.</td>
      <td rowspan=4>Pay-as-you-go</td>
   </tr>
   <tr>
      <td colspan=1>COS Select fees</td>
   </tr>
   <tr>
      <td colspan=1>Batch operation fees</td>
   </tr>
   <tr>
      <td colspan=1>Object tagging fees</td>
   </tr>
</table>


## Pricing

You can check the prices of COS billable items at [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=). Details are as follows:
- Pay-as-you-go pricing: Public cloud pricing applies to public cloud regions, and finance cloud pricing applies to finance cloud regions. For more information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
- Resource pack pricing: The prices of public cloud resource packs apply to regions in the Chinese mainland and regions outside the Chinese mainland. For more information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=) or the [resource pack purchase page](https://buy.intl.cloud.tencent.com/cos?packageType=std).


## Price calculator

You can estimate the usage of billable items based on your own business needs and then use the [price calculator](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=) to calculate fees and export the cost estimate.

## Related documentation


1. For more information on COS fees calculation and billing in different scenarios, see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).
2. For more information on the COS overdue policy (data retention and destruction), see COS [Payment Overdue](https://www.tencentcloud.com/document/product/436/10044).
3. For more information on the use of resource packs, see [Notes on Purchase of COS Resource Packs](https://www.tencentcloud.com/document/product/436/54353).
4. For more information on billing cycles, see [Bill Management](https://www.tencentcloud.com/document/product/555/7430?lang=en&pg=).
5. If you have more questions about COS billing, see [FAQs](https://www.tencentcloud.com/document/product/436/32532) or [contact us](https://www.tencentcloud.com/contact-us).

