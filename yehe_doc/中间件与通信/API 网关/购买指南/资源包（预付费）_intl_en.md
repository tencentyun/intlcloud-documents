> ?The API Gateway resource pack feature was launched at 23:59:59 on October 12, 2020. Resource packs are available through free tiers, purchases, and promotional campaigns.

API Gateway supports multiple billing modes. This document describes the resource pack (prepaid) mode. A resource pack is a fixed pack consisting of one or more billable items. After you obtain a resource pack of certain specifications, the resource usage can be deducted from the resource pack during the validity period of the resource pack. Currently, API Gateway resource packs are available through free tiers, purchases, and promotional campaigns.

## Resource Pack Classifications

The following table classifies resource packs by type:

| Resource Pack Type | Description                   | Deduction and Settlement       |
| ---------- | ---------------------- | ---------------- |
| Call count pack | Deducts call fees   | By hour |
| Outbound traffic pack   | Deducts public network outbound traffic fees | By hour |

The following table classifies resource packs by source:

| Resource Pack Source | Description                                                         |
| ---------- | ------------------------------------------------------------ |
| Free tier   | A resource pack is obtained free of charge after API Gateway is activated and is used to deduct the free tier usage. Unused resources do not accumulate to the next month, and refunds are not supported. For more information, please see [Free Tier](https://intl.cloud.tencent.com/document/product/628/11784). |
| Operating campaign   | A resource pack is purchased in the operating campaigns of API Gateway at a price lower than that of the postpaid mode. Resources in the resource pack are valid for a long time within the validity period. Refunds are supported if the conditions are met. |

The classification of resource packs by region is as follows:
Only the all regions type is supported. Resource packs are applicable to all public cloud regions in the Chinese mainland and Hong Kong (China) and outside China.

## Purchase Notes

- Currently, API Gateway resource packs are available only in public cloud regions and applicable only to USD accounts. For more information about regions, please see [Regions and AZs](https://intl.cloud.tencent.com/document/product/628/33133).
- A resource pack takes effect immediately on the day of purchase. A month in the validity period is equal to 30 days.
- Unused resources in a free tier resource pack do not accumulate to the next month, whereas resources in a resource pack from other sources are valid for a long time within the validity period.
- If you purchase an inappropriate resource pack by mistake, you can make a self-service refund if the refund conditions are met.
- During the validity period of a resource pack, bills are settled in the following sequence: free tier > resource pack > pay-as-you-go. The usage beyond the free tier and resource pack usage limits is billed on a pay-as-you-go basis.
- If a user account has overdue payment (the balance is below 0), API Gateway will be suspended after 24 hours, regardless of whether the resource pack is within the validity period.
- Currently, a resource pack consists of only postpaid billable items (number of calls and public network outbound traffic). During the use of API Gateway, other fees (such as instance fees for performance guarantee clusters) may be incurred and will be charged based on billing standards.

## Resource Pack Validity Period

A month in the validity period of a resource pack is equal to 30 days.

## Resource Pack Effective Scope

### Example

Assume that you obtain a call count pack that will be valid for 3 months on October 12, 2020. This resource pack provides 5 million calls and is available in all regions.

From October 15 to October 31, 3 million calls and 10 GB of public network outbound traffic are used in the API Gateway in Guangzhou, and 0.5 million calls and 3 GB of public network outbound traffic are used in the API Gateway in Hong Kong (China). The following table describes the effective scope of this resource pack:

<table>
   <tr>
      <th>Generated Billable Item</th>
      <th>Whether the Resource Pack Is Effective</th>
   </tr>
   <tr>
      <td>Fees for 3 million calls in Guangzhou</td>
      <td>Yes. The fees for 3 million calls will be deducted from the resource pack</td>
   </tr>
   <tr>
      <td>Fees for 10 GB of public network outbound traffic in Guangzhou</td>
      <td>No. The resource pack cannot be used to deduct fees for public network outbound traffic. The fees will be charged on a pay-as-you-go basis</td>
   </tr>
   <tr>
      <td>Fees for 0.5 million calls in Hong Kong (China)</td>
      <td>Yes. The fees for 0.5 million calls will be deducted from the resource pack</td>
   </tr>
   <tr>
      <td>Fees for 3 GB of public network outbound traffic in Hong Kong (China)</td>
      <td>No. The resource pack cannot be used to deduct fees for public network outbound traffic. The fees will be charged on a pay-as-you-go basis</td>
   </tr>
</table>

## Self-service Refund

API Gateway supports self-service refund for resource packs. You can perform self-service resource termination/return in the API Gateway console. The system will automatically refund your money and terminate/return cloud resources.

### Refund rules

- Vouchers used for purchasing a resource pack are not refundable. Non-voucher fees will be fully refunded to the payer's Tencent Cloud account in accordance with the payment mode (cash or gift card). For more information, please see [Order Management](https://console.cloud.tencent.com/expense/deal).
- Self-service refund is supported if the API Gateway resource pack meets the following four conditions:
   - The source of the resource pack is not the free tier.
   - The order type is **Purchase**.
   - Resources in the resource pack have not been used.
   - The resource pack is in the validity period.

### Refund procedure

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Resource Pack** to access the resource pack list page.
3. Click **Refund** in the "Operation" column in the row of the target resource pack. In the pop-up dialog box, confirm and submit the information.
![](https://main.qcloudimg.com/raw/e75ee450d18ac55e19f85ff1764186be.png)
