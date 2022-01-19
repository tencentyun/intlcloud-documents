Private network CLB is used to distribute requests from Tencent Cloud's private network. It doesn't have a public IP and cannot communicate with the public network. If you need to use a private network CLB instance and want it to communicate with the public network, you can bind it to an EIP for public network access.

>?The feature of binding private network CLB with EIP is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Use Limits
- This feature is supported only for standard accounts but not traditional accounts.
- This feature is supported only for CLB but not classic CLB.
- This feature is supported only for private network CLB instances in VPCs but not in the classic network.
- There are no private network CLB instances in Ji'nan, Hangzhou, Fuzhou, Shijiazhuang, Wuhan, and Changsha regions, so this feature is not supported in these regions.
- After a private network CLB instance is bound to an EIP, the security group of the instance takes effect for traffic from the instance but not from the EIP. After the "Allow by Default" feature is enabled in the security group, it will take effect for both types of traffic.
- Currently, private network CLB doesn't support port ranges.
- A private network CLB instance can only be bound to an EIP that is in the same region and not bound to other resources.
- Each private network CLB instance can only be bound to one EIP.
- After a private network CLB instance is bound to an EIP, its features will be similar to those of a public network CLB instance, but public network CLB cannot be split into private network CLB and EIP.


## Directions

<dx-accordion>
::: Method 1: choose EIP when purchasing CLB
1. Log in to the [CLB purchase page](https://buy.intl.cloud.tencent.com/lb).
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
Select a region. For more information on the regions supported by CLB, see <a href="https://intl.cloud.tencent.com/document/product/214/33792">Region List</a>.
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
::: Method 2: bind private network CLB to EIP
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb) and click **Instance Management** on the left sidebar.
2. Select a region in the top-left corner of the **Instance Management** page, select the target private network CLB instance in the instance list, and click **More** > **Bind EIP** in the **Operation** column on the right.
3. In the **Bind EIP** pop-up window, select the EIP to be bound and click **Submit** to bind the EIP to the instance.
<img src="https://qcloudimg.tencent-cloud.cn/raw/201e56b830bc8e165070b8963fe72cb3.png" width="60%">
4. (Optional) Select the target private network CLB instance in the instance list and click **More** > **Unbind EIP** in the **Operation** column on the right to unbind the instance from the EIP.
:::
</dx-accordion>


## Relevant Documentation
- [AssociateAddress](https://intl.cloud.tencent.com/document/product/215/16700)
- [Purchase Methods](https://intl.cloud.tencent.com/document/product/214/8849)
- [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629)
