## Billable Items
CLB fees consist of instance fees and public network fees.

 <table>
 <tr>
 <th>Instance Type</th>
 <th>Account Type</th>
 <th>Instance Fees</th>
 <th>Public Network Fees</th>
 <th>Description</th>
 </tr>
 <tr>
 <td rowspan="2">Public network</td>
 <td >Non-bill-by-IP account</td>
 <td >&#10003; </td>
 <td >× </td>
 <td ><li>The instance fees will be charged by CLB.</li><li>
The public network fees will be charged by CVM instead of CLB.</li><li>For more information, please see <a href="https://intl.cloud.tencent.com/document/product/214/8848">Non-bill-by-IP Account Billing Description</a>.</li></td>
 </tr>
 <tr>
 <td >Bill-by-IP account</td>
 <td >&#10003; </td>
 <td >&#10003; </td>
 <td ><li>The instance fees and public network fees will be charged by CLB.</li><li>For more information, please see <a href="https://intl.cloud.tencent.com/document/product/214/36998">Bill-by-IP Account Billing Description</a>.</li></td>
 </tr>
 <tr>
 <td >Private network</td>
 <td >All accounts</td>
 <td >—</td>
 <td >— </td>
 <td >Private network is free of charge.</td>
 </tr>
 </table>

## Account Type
>? 
> - Tencent Cloud accounts registered on and after June 17, 2020 are bill-by-IP. For Tencent Cloud accounts registered before June 17, 2020, please check the account types in the console. For more information, please see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
> - Bill-by-IP is an attribute at the account level. An account can only be bill-by-IP or non-bill-by-IP.

### Non-bill-by-IP Account
- For a non-bill-by-IP account, public network fees are charged by CVM, and CLB is only used as the public network egress. The public network billing mode and bandwidth upper limit are specified when the CVM instance is created, and no network billing configuration is available when the public network CLB instance is created.
- Under a non-bill-by-IP account, neither the purchase page nor the list page of the public network CLB instance contains the bandwidth information.
 - **Purchase page**
![](https://main.qcloudimg.com/raw/002bfe22170790f2bebaa2840f274e3d.png)
 - **List page**
![](https://main.qcloudimg.com/raw/14521f3afe27876f866419c29168915d.png)

### Bill-by-IP Account
- For a bill-by-IP account, the public network fees are charged by the public IP or CLB instead of CVM. You can specify the public network billing mode and bandwidth upper limit in the public IP or CLB instance configuration.
- Under a bill-by-IP account, both the purchase page and the list page of the public network CLB instance contain the bandwidth information.
 - **Purchase page**
![](https://main.qcloudimg.com/raw/48da1dad2b1cc02a0c0165f0155d28a3.png)
 - **List page**
![](https://main.qcloudimg.com/raw/ae9f890d5c71a28920deed8cb0dfd536.png)

