## Free Tier

| Item |     Description    |
| -------- | ---------------- |
| Object | New users |
| Validity | Within one year after API Gateway is activated |
| Free tier | A certain number of calls and public network outbound traffic provided by API Gateway. For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/628/11784) |
| How to get | A free resource pack will be added to your account after API Gateway is activated. [Activate API Gateway now](https://console.cloud.tencent.com/apigateway/index) |


## Billing Modes

API Gateway supports the following billing modes: pay-as-you-go, resource pack, and dedicated instances. See below for details:

| Billing Mode                                                     | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/628/11771) | Default billing mode of API Gateway                                |
| [Resource Pack](https://intl.cloud.tencent.com/document/product/628/38407)                                             | Resource packs are only available to beta users now. If you want to use it, please contact your sales rep.|

## Billable Items

The billable items of API Gateway include the call count, instances, and public outbound traffic.
Call count: available for shared instances. For details, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/628/11771).
Public outbound traffic: available for both shared instances and dedicated instances. For details, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/628/11771).

>? For information on the difference between shared instances and dedicated instances, see [Instance Selection](https://intl.cloud.tencent.com/document/product/628/40305).

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
      <td>Call count</td>
      <td>Hourly</td>
      <td>Fees for an hour are calculated and billed in the next hour</td>
      <td>Free tier > resource pack > pay-as-you-go</td>
   </tr>
   <tr>
      <td>Public outbound traffic</td>
      <td>Hourly</td>
      <td>Fees for an hour are calculated and billed in the next hour</td>
      <td>Free tier > resource pack > pay-as-you-go</td>
   </tr>
</table>
