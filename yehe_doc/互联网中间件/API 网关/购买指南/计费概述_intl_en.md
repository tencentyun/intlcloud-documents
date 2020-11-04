## Free Tier

| Item |     Description    |                                    
| -------- | ---------------- |
| Object | New users |
| Free usage period | One year after API Gateway is activated | 
| Free tier | A certain number of calls and public network outbound traffic provided by API Gateway. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/628/11784) |
| How to obtain the free tier | The system automatically issues the free tier in the form of a resource pack after API Gateway is activated. [Activate API Gateway now](https://console.cloud.tencent.com/apigateway/index) |
 

## Billing Modes

API Gateway supports the following billing modes: pay-as-you-go, resource pack, and performance guarantee cluster. The following table describes the billing modes.

| Billing Mode                                                     | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Pay-as-You-Go (Postpaid)](https://intl.cloud.tencent.com/document/product/628/11771) | Default billing mode of API Gateway                                |
| [Resource Pack (Prepaid)](https://intl.cloud.tencent.com/document/product/628/38407)                                             | Preferential pack for API Gateway. It can be used to deduct fees for certain billable items. Currently, resource packs can be obtained only through free tiers or operating campaigns, and cannot be purchased |

## Billable Items

The billable items of API Gateway include the number of calls and public network outbound traffic. For more information about billable items and prices, see [Pay-as-You-Go (Postpaid)](https://intl.cloud.tencent.com/document/product/628/11771).

## Billing Cycles

The following table describes the billing cycles and sequences of API Gateway billable items.

<table>
   <tr>
      <th>Billable Item</th>
      <th>Billing Cycle</th>
      <th>Description</th>
      <th>Billing Sequence</th>
   </tr>
   <tr>
      <td>Number of calls</td>
      <td>Hourly</td>
      <td>Fees for an hour are calculated and billed in the next hour</td>
      <td>Free tier > resource pack > pay-as-you-go</td>
   </tr>
   <tr>
      <td>Public network outbound traffic</td>
      <td>Hourly</td>
      <td>Fees for an hour are calculated and billed in the next hour</td>
      <td>Free tier > resource pack > pay-as-you-go</td>
   </tr>
</table>
