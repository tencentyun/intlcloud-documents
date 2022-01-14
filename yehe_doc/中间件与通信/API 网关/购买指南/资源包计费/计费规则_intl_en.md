>?The API Gateway resource pack feature was launched at 23:59:59 on October 12, 2020. Resource packs are available through free tiers, purchases, and promotional campaigns.

API Gateway supports multiple billing modes. This document describes the resource pack (prepaid) mode. A resource pack is a fixed pack consisting of one or more billable items. After you obtain a resource pack of certain specifications, the resource usage can be deducted from the resource pack during the validity period of the resource pack. Currently, API Gateway resource packs are available through free tiers, purchases, and promotional campaigns.

## Resource Pack Classifications

- The following table classifies resource packs by type:
<table>
<thead>
<tr>
<th>Resource Pack Type</th>
<th>Description</th>
<th>Deduction and Settlement</th>
</tr>
</thead>
<tbody><tr>
<td>API call pack</td>
<td>Used to deduct the fees for API calls in <strong>shared instances</strong>.</td>
<td>Deducted and settled by hour</td>
</tr>
<tr>
<td>Public network outbound traffic pack</td>
<td>Used to deduct the fees for public network outbound traffic in <strong>shared instances</strong> and <strong>dedicated instances</strong>.</td>
<td>Deducted and settled by hour</td>
</tr>
</tbody></table>

- The following table classifies resource packs by source:
<table>
<thead>
<tr>
<th>Resource Pack Source</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Free tier</td>
<td>A resource pack is obtained free of charge after API Gateway is activated and is used to deduct the free tier usage. Unused resources do not accumulate to the next month, and refunds are not supported. For more information, see <a href="https://intl.cloud.tencent.com/document/product/628/38406">Free Tier</a>.</td>
</tr>
<tr>
<td>Operating campaign</td>
<td>A resource pack is purchased in the operating campaigns of API Gateway at a price lower than that of the postpaid mode. Resources in the resource pack are valid for a long time within the validity period. Refunds are supported if the conditions are met.</td>
</tr>
<tr>
<td>Purchase</td>
<td>A resource pack can be purchased in the API Gateway console at the price displayed on the purchase page.</td>
</tr>
</tbody></table>

- The classification of resource packs by region is as follows:

  Only the all regions type is supported. **Resource packs are applicable to all public cloud regions in the Chinese mainland and Hong Kong (China) and outside China.**

## Purchase Notes

- Currently, API Gateway resource packs are available only in public cloud regions but not in certain finance cloud regions and are applicable only to CNY accounts. For more information about regions, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/628/33133).
- A resource pack takes effect immediately on the day of purchase. A month in the validity period is equal to 30 days.
- Unused resources in a free tier resource pack do not accumulate to the next month, whereas resources in a resource pack from other sources are valid for a long time within the validity period.
- If you purchase an inappropriate resource pack by mistake, you can make a self-service refund if the refund conditions are met.
- **While the resource pack is effective, bills will be settled in the following sequence: free tier > resource pack > pay-as-you-go. Usage beyond the free tier and the resource pack's capacity will be billed using the pay-as-you-go mode.**
- If an account has overdue payments (the account's balance is below 0), the API Gateway service will be suspended after 24 hours, regardless of whether the resource pack is effective or not.
- Currently, a resource pack consists of only postpaid billable items (number of calls and public network outbound traffic). During the use of API Gateway, other fees (such as instance fees for performance guarantee clusters) may be incurred and will be charged based on billing standards.

## Resource Pack Validity Period

The resource pack's validity period of 1 month is equivalent to 30 days.

## Resource Pack Effective Scope

#### Examples

Suppose you get an API call pack that is valid for 3 months on October 12, 2020. This resource pack provides 5 million calls and is available in all regions.

From October 15 to October 31, 2020, 3 million calls and 10 GB of public network outbound traffic are used in the API Gateway in Guangzhou, and 0.5 million calls and 3 GB of public network outbound traffic are used in the API Gateway in Hong Kong (China). The following table describes the effective scope of this resource pack:

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
