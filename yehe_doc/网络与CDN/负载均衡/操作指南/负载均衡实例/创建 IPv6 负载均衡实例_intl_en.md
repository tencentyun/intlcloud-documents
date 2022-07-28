>?
>- The IPv6 CLB is in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1).
>- Currently, IPv6 CLB is only supported in the following regions: Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, and Virginia.
>- IPv6 CLB does not support classic CLB.
>- IPv6 CLB supports obtaining the client's IPv6 source address, which can be directly obtained by layer-4 IPv6 CLB or through the `X-Forwarded-For` header of HTTP layer-7 IPv6 CLB.
>- Currently, IPv6 CLB balances the load completely over the public network. Clients in the same VPC cannot access IPv6 CLB over the private network.
>- IPv6 implementations are still at the preliminary stage across the internet. In case of access failure, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1). SLA is not guaranteed during the beta test period.
>


## Overview
IPv6 load balancing is implemented based on the IPv6 single stack technology. It can collaborate with IPv4 CLB to implement IPv6/IPv4 dual-stack communication. An IPv6 CLB instance is bound to an IPv6 address of a CVM instance and provides an IPv6 VIP address.

### IPv6 CLB Advantages
Tencent Cloud IPv6 CLB has the following advantages when helping your business quickly connect to IPv6:
- **Quick connection:** CLB enables connection to IPv6 in a matter of seconds and is available upon purchase.
- **Ease of use:** IPv6 CLB is compatible with IPv4 CLB flowchart and easy to use with no additional learning costs incurred.
- End-to-end IPv6 communication: IPv6 CLB instances communicate with CVM instances over IPv6, which helps applications deployed on the CVM instances quickly upgrade to IPv6 and implement end-to-end IPv6 communication.

### IPv6 CLB Architecture
CLB supports creating IPv6 CLB instances. Tencent Cloud will assign an IPv6 public IP address, i.e., VIP of the IPv6 edition, to an IPv6 CLB instance, and the VIP will forward requests from IPv6 clients to the real IPv6 CVM instance.

An IPv6 CLB instance can support quick access of users from IPv6 public network and communicate with real servers over IPv6, which helps in-cloud applications quickly upgrade to IPv6 and implement end-to-end IPv6 communication.

The IPv6 CLB architecture is as shown below:
![](https://main.qcloudimg.com/raw/d86205a385506928dc13ef9646a91243.png)


## Step 1. Create an IPv6 CLB instance
1. Log in to the Tencent Cloud console and go to the [CLB purchase page](https://buy.intl.cloud.tencent.com/lb).
2. Select the following CLB configuration items as needed:
<dx-accordion>
::: Bill-by-IP account
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
Supports pay-as-you-go billing. IPv6 version is only supported in pay-as-you-go mode. For other restrictions, see IP versions instructed in <a href="https://intl.cloud.tencent.com/document/product/214/13629">Product Attribute Selection</a>.
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
Supports CLB instance type only. Starting from October 20, 2021, classic CLB instances can no longer be purchased. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/41387">[October 20, 2021] Classic CLB End-of-Sale Notice</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network Type</span></td>
<td>Supports public network and private network. For more information, see Network Types instructed in <a href="https://intl.cloud.tencent.com/document/product/214/13629">Product Attribute Selection</a>. Select a public network for IPv6 CLB.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">EIP</span></td>
<td>
	Don't select an EIP.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">IP Version</span></td>
<td>
Select the IPv6 version.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network</span></td>
<td>
Select an existing VPC or subnet. If the existing networks are inapplicable, you can <a href="https://intl.cloud.tencent.com/document/product/215/31805">Creating VPCs</a> or <a href="https://intl.cloud.tencent.com/document/product/215/31806">Creating Subnets</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Carrier Type</span></td>
<td>
BGP.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Instance Specification</span></td>
<td>Shared and LCU-supported instances are supported.
	<ul>
	<li>Multiple shared instances share resources, and a single instance doesn't provide guaranteed performance. By default, all instances are shared instances.</li>
	<li>An LCU-supported instance guarantees the performance and doesn't preempt resources like a shared instance. Its forwarding performance is not affected by other instances. A single instance can sustain up to 1 million concurrent connections, 100,000 new connections per second, and 50,000 queries per second. Currently, the LCU-supported specification is in beta. To use it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Dual-stack Binding</span></td>
<td>
After this feature is enabled, the layer-7 listener can be bound with both IPv4 and IPv6 backend servers. But layer-4 listeners only support binding of IPv6 backend server.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network Billing Mode</span></td>
<td>Supports bill by traffic and bill by bandwidth.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Bandwidth Cap</span></td>
<td>Value range: 1–2048 Mbps.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Project</span></td>
<td>Select a project.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Tag</span></td>
<td>Select a tag key and value. You can also create a tag as instructed in <a href="https://intl.cloud.tencent.com/document/product/651/41575">Creating Tags and Binding Resources</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Instance Name</span></td>
<td>The name can contain up to 60 characters, including letters, numbers, hyphens, underscores, and dots. If it is not specified, a name will be automatically generated by default.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Service Protocol</span></td>
<td>Check "I've read and agree to <a href="https://intl.cloud.tencent.com/document/product/301/12905">Tencent Cloud Terms of Service"</a>and<a href="https://intl.cloud.tencent.com/document/product/214/531">CLB Service Level Agreement</a>".
</td>
</tr>
</tbody></table>
:::
::: Bill-by-CVM account
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
Supports pay-as-you-go billing only.
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
Supports CLB instance type only. Starting from October 20, 2021, classic CLB instances can no longer be purchased. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/41387">[October 20, 2021] Classic CLB End-of-Sale Notice</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network Type</span></td>
<td>Supports public network and private network. For more information, see Network Types instructed in <a href="https://intl.cloud.tencent.com/document/product/214/13629">Product Attribute Selection</a>.
	<ul>
	<li>Public network: CLB is used to distribute requests from the public network.</li>
	<li>Private network: CLB is used to distribute requests from the Tencent Cloud private network. A private network instance doesn't support the following configuration items and doesn't display them by default: <strong>IP Version</strong>, <strong>Carrier Type</strong>, and <strong>Instance Specification</strong>.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">IP Version</span></td>
<td>
Select IPv6. For more information on the use limits, see IP Versions instructed in <a href="https://intl.cloud.tencent.com/document/product/214/13629">Product Attribute Selection</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network</span></td>
<td>
CLB supports classic network and VPC.
	<ul>
	<li>The classic network is a public network resource pool shared by all Tencent Cloud users. The private IPs of all CVMs are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses.</li>
	<li>The VPC is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies.</li>
	</ul>
	By contrast, VPC is more suitable for use cases requiring custom configurations. Besides, the overall classic network products will be officially discontinued on December 31, 2022. For details, see <a href="https://intl.cloud.tencent.com/document/product/215/45485">Ending Support for Classic Network</a>. It is recommended that you choose a VPC.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Carrier Type</span></td>
<td>
BGP.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Instance Specification</span></td>
<td>Shared and LCU-supported instances are supported.
	<ul>
	<li>Multiple shared instances share resources, and a single instance doesn't provide guaranteed performance. By default, all instances are shared instances.</li>
	<li>An LCU-supported instance guarantees the performance and doesn't preempt resources like a shared instance. Its forwarding performance is not affected by other instances. A single instance can sustain up to 1 million concurrent connections, 100,000 new connections per second, and 50,000 queries per second. Currently, the LCU-supported specification is in beta. To use it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network Billing Mode</span></td>
<td>Bill by bandwidth.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Bandwidth Cap</span></td>
<td>Value range: 1–1024 Mbps.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Project</span></td>
<td>Select a project.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Tag</span></td>
<td>Select a tag key and value. You can also create a tag as instructed in <a href="https://intl.cloud.tencent.com/document/product/651/41575">Creating Tags and Binding Resources</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Instance Name</span></td>
<td>The name can contain up to 60 characters, including letters, numbers, hyphens, underscores, and dots. If it is not specified, a name will be automatically generated by default.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Service Protocol</span></td>
<td>Check "I've read and agree to <a href="https://intl.cloud.tencent.com/document/product/301/12905">Tencent Cloud Terms of Service"</a>and<a href="https://intl.cloud.tencent.com/document/product/214/531">CLB Service Level Agreement</a>".
</td>
</tr>
</tbody></table>
:::
</dx-accordion>

3. After configuring the above items, click **Buy now**. On the "CLB order confirmation" pop-up window, click **Confirm order**. Then, return to [Instance Management](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1) page where you can view the IPv6 CLB instance you just purchased.


## Step 2. Create an IPv6 CLB listener
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3) and click the IPv6 CLB instance ID to enter the details page.
2. Select the **Listener Management** tab, click **Create**. For example, create a TCP listener.
>?CLB supports creating layer-4 (TCP/UDP/TCP SSL) and layer-7 (HTTP/HTTPS) IPv6 CLB listeners. For more information, please see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
>
3. In "Basic Configurations", configure the name, listening protocol port, and balancing method, and click **Next**.
![](https://main.qcloudimg.com/raw/dce7a8870add7556a229c10990444e78.png)
4. Configure health check and click **Next**.
![](https://main.qcloudimg.com/raw/7e425de32751160382b602752c302f19.png)
5. Configure session persistence and click **Submit**.
![](https://main.qcloudimg.com/raw/e4d910a5904e1c8fb890d594bb64ba72.png)
6. After the listener is created, select it and click **Bind** on the right.
>?Before binding the listener to a CVM instance, please make sure that the CVM instance has obtained an IPv6 address.
>
![](https://main.qcloudimg.com/raw/6c1a45bed978f944fcb34984849d5287.png)
7. In the pop-up box, select the IPv6 CVM instance that needs to be communicated with, configure the server port and weight, and click **OK**.
![](https://main.qcloudimg.com/raw/6c1a45bed978f944fcb34984849d5287.png)

## More Operations
### Binding IPv6 CLB with both IPv6 and IPv4 real servers
After enabling the dual-stack binding, the IPv6 CLB layer-7 listener can be bound with both IPv4 and IPv6 backend servers, and can obtain the source IP via XFF. But layer-4 listeners only support binding of IPv6 backend server.
1. Enable dual-stack binding.
 -  Enable dual-stack binding when purchasing IPv6 CLB on the purchase page.
![]()
 -  Enable dual-stack binding on the IPv6 CLB instance details page.
 ![]()
2. Create a layer-7 HTTP or HTTPS listener.
3. Bind the listener with a IPv6 or IPv4 backend server.
![]()

