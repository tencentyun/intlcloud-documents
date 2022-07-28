Private network CLB is used to distribute requests from Tencent Cloud's private network. It doesn't have a public IP and cannot communicate with the public network. If you need to use a private network CLB instance and want it to communicate with the public network, you can bind it to an EIP for public network access.

>?The feature of binding the EIP to the private network CLB is in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Limits
- **Region Limits**
  - Private network CLB instances are unavailable in Ji'nan, Fuzhou, Shijiazhuang, Wuhan, and Changsha regions.
- **Product Attribute Limits**
  - This feature is supported only for bill-by-IP accounts but not bill-by-CVM accounts.
  - This feature is supported only for CLB but not classic CLB.
  - This feature is supported only for private network CLB instances in VPCs but not in the classic network.
- **Feature limits**
  - Currently, private network CLB doesn't support port ranges.
  - A private network CLB instance can only be bound to an EIP that is in the same region and not bound to other resources.
  - Each private network CLB instance can only be bound to one EIP.
  - After a private network CLB instance is bound to an EIP, its features will be similar to those of a public network CLB instance, but public network CLB cannot be split into private network CLB and EIP.
- **Security Group Limits**
  - After a private network CLB instance is bound to an EIP, the security group of the instance takes effect for traffic from the instance but not from the EIP. After the "Allow by Default" feature is enabled in the security group, it will take effect for both types of traffic.

## How It Works

<dx-accordion>
::: Method 1: Choose EIP when purchasing CLB
1. Log in to the Tencent Cloud console and go to the [CLB purchase page](https://buy.intl.cloud.tencent.com/lb).
2. Select the following CLB configuration items as needed. For other configuration details, see [Purchase Methods](https://intl.cloud.tencent.com/document/product/214/8849).
<table>
<thead>
<tr>
<th width="18%">Parameter</th>
<th width="82%">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><span style="font-weight:bold">Billing Mode</span></td>
<td>
Select the <b>Pay-as-You-Go</b> mode.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Region</span></td>
<td>
Select a region. For more information on the regions supported by CLB, see Region List instructed in <a href="https://intl.cloud.tencent.com/document/product/214/33792">Common Params</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Instance Type</span></td>
<td>
Only CLB instance type is supported.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network Type</span></td>
<td>Select the <b>Public Network</b> type.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">EIP</span></td>
<td>Select <b>EIP</b>. Tencent Cloud will assign you an EIP and a private network CLB instance. Supported EIP types include general IP, accelerated IP, and static single-line IP.
</td>
</tr>
</tbody></table>
:::
::: Method 2: Bind private network CLB to EIP
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), and click **Instance Management** on the left sidebar.
2. Select a region in the top-left corner of the **Instance Management** page, select the target private network CLB instance in the instance list, and click **More** > **Bind EIP** in the **Operation** column on the right.
3. In the **Bind EIP** pop-up window, select the EIP to be bound and click **Submit** to bind the EIP to the instance.
<dx-alert infotype="explain"> 
The accelerated IPs and static single-line IPs are in beta test. To try them out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
</dx-alert> 
<img src="" width="60%">
4. (Optional) Select the target private network CLB instance in the instance list and click **More** > **Unbind EIP** in the **Operation** column on the right to unbind the instance from the EIP.
:::
</dx-accordion>


## References
- [AssociateAddress](https://intl.cloud.tencent.com/document/product/215/16700)
- [Purchase Methods](https://intl.cloud.tencent.com/document/product/214/8849)
- [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629)
