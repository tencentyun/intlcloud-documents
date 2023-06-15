This document explains how CLB instances are billed.


## Billable Items
The CLB cost involves the following four parts: instance fee, public network fee, cross-region binding fee and LCU (Loadbalancer Capacity Unit) fee.
<dx-alert infotype="explain" title="">
- Only LCU-supported CLB instances will incur LCU usage fees. 
- Tencent Cloud provides two types of accounts: bill-by-IP and bill-by-CVM. All Tencent Cloud accounts registered after 00:00:00, June 17, 2020 (UTC +8) are bill-by-IP accounts. If you have created an account before that time, you can check your account type at the top of the instance list on the <a href="https://console.cloud.tencent.com/cvm/eip">EIP console</a>.
- To use a dedicated CLB instance, please contact your sales rep. 
</dx-alert>
<table>
<tr>
<th>Instance Type</th>
<th>Account Type</th>
<th>Instance Fee</th>
<th>Public Network<br/>Fee </th>
<th>Cross-region<br/>Binding Fee </th>
<th>LCU Fee</th>
</tr>
<tr>
<td rowspan="2">Public network </td>
<td >Bill-by-IP account</td>
<td >&#10003; </td>
<td >&#10003; </td>
<td >&#10003; </td>
<td >&#10003;</td>
</tr>
<tr>
<td >Bill-by-CVM account </td>
<td >&#10003; </td>
<td >× </td>
<td >-</td>
<td >&#10003;</td>
</tr>
<tr>
<td >Private network</td>
<td >All accounts</td>
<td >&#10003;</td>
<td >-</td>
<td >-</td>
<td >&#10003;</td>
</tr>
</table>

## Bill-by-IP Account Billing Description
+ Private network CLB is free of public network fee but generates instance fee. For more details, see [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/zh/document/product/214/41565).
+ Public network CLB generates instance fee and public network fee.
+ If <a href="https://intl.cloud.tencent.com/zh/document/product/214/38441"> cross-region binding 2.0</a> is configured and enabled for public network CLB instances, the cross-region binding fee is included in the CNN bill.
+ LCU-supported CLB instances incur LCU charges, while shared CLB instances do not.

## Bill-by-CVM Account Billing Description
+ Private network CLB is free of public network fee but generates instance fee. For more details, see [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/zh/document/product/214/41565).
+ Public network CLB only generates instance fee. You can purchase public network on CVM. For more details, see [Public Network Fee](https://intl.cloud.tencent.com/zh/document/product/213/39743).
+ Bill-by-CVM accounts do not support cross-region binding and thus no binding fee generated.
+ LCU-supported CLB instances incur LCU charges, while shared CLB instances do not.

## References
- [Bill-by-IP Account Billing Description](https://intl.cloud.tencent.com/zh/document/product/214/36998)
- [Bill-by-CVM Account Billing Description](https://intl.cloud.tencent.com/zh/document/product/214/8848)
