Tencent Cloud allows you to purchase a CLB instance on the official purchase page or via API. The two methods are detailed below:

## [Purchasing at Official Website](id:Official-Purchase)
You can purchase a CLB instance on the [Tencent Cloud official website](https://buy.cloud.tencent.com/lb). There are two types of Tencent Cloud accounts, namely the bill-by-IP accounts and bill-by-CVM accounts. The accounts created after 00:00:00 on June 17, 2020 (Beijing time) are of the bill-by-IP type. If you have created your account before that time, you can check your account type in the console as instructed in [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).

1. Log in to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
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
Pay-as-You-Go billing is supported.
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
Only the CLB instance type is supported. Starting from October 20, 2021, classic CLB instances can no longer be purchased. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/41387">Classic CLB End-of-Sale Notice</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network Type</span></td>
<td>There are two network types: public network and private network. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/13629#network-type">Network Types</a>.
	<ul>
	<li>Public network: CLB is used to distribute requests from the public network.</li>
	<li>Private network: CLB is used to distribute requests from the Tencent Cloud private network. A private network instance doesn't support the following configuration items and doesn't display them by default: <strong>EIP</strong>, <strong>IP Version</strong>, <strong>ISP Type</strong>, <strong>Instance Specification</strong>, <strong>Network Billing Mode</strong>, and <strong>Bandwidth Cap</strong>.</li>
	</ul>
	The supported network types vary by billing mode:
	<ul>
	<li>In pay-as-you-go billing mode, both the public and private network types are supported.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">EIP</span></td>
<td>
	<ul>
	<li>If EIP is not selected, Tencent Cloud will assign you a public network CLB instance whose public IP cannot be changed.</li>
	<li>If EIP is selected, Tencent Cloud will assign you an EIP and a private network CLB instance, which has the similar features of public network CLB (only pay-as-you-go public network CLB instances allow you to select an EIP).
</li>
	</ul>
	This feature is currently in beta test. To use it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application. For the use limits, see <a href="https://intl.cloud.tencent.com/document/product/214/44336">Use Limits</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">IP Version</span></td>
<td>
The following CLB IP versions are supported: IPv4, IPv6, and IPv6 NAT64. Only pay-as-you-go instances support the IPv6 version. For more information on other restrictions, see <a href="https://intl.cloud.tencent.com/document/product/214/13629#IP-type">IP Versions</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network</span></td>
<td>
CLB supports classic network and VPC.
	<ul>
	<li>The classic network is a public network resource pool for all Tencent Cloud users. The private IPs of all CVMs are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses.</li>
	<li>By contrast, the VPC is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies.</li>
	</ul>
	Between the two options, VPC is more suitable for scenarios requiring custom network configurations, and the classic network product will be officially discontinued on December 31, 2022. We recommend you select VPC.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">ISP Type</span></td>
<td>
The following ISP types are supported: BGP, China Mobile, China Telecom, and China Unicom.
	<ul>
	<li>In pay-as-you-go billing mode, all of the above four options are supported.
Currently, the static single-line IP is supported only in Guangzhou, Shanghai, Nanjing, Jinan, Hangzhou, Fuzhou, Beijing, Shijiazhuang, Wuhan, Changsha, Chengdu, and Chongqing. For its support in other districts, see the console. If you want to try it out, contact the sales rep for application. Once you are accepted, you can select an ISP (China Mobile, China Unicom, or China Telecom) on the purchase page.
	</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Primary/Secondary Availability Zone</span></td>
<td>The primary availability zone (AZ) is an AZ that currently sustains the traffic. The secondary AZ doesn't sustain traffic by default and will be used only when the primary AZ is unavailable. Currently, only IPv4 CLB instances in the Guangzhou, Shanghai, Nanjing, Beijing, Hong Kong (China), and Seoul regions support primary/secondary AZs.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Instance Specification</span></td>
<td>Shared and LCU-supported instances are supported.
	<ul>
	<li>Multiple shared instances share resources, and a single instance doesn't provide guaranteed performance. By default, all instances are shared instances.</li>
	<li>An LCU-supported instance guarantees the performance and doesn't preempt resources like a shared instance. Its forwarding performance is not affected by other instances. A single instance can sustain up to 1 million concurrent connections, 100,000 new connections per second, and 50,000 queries per second. Currently, the LCU-supported specification is in beta. To use it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network Billing Mode</span></td>
<td>The following network billing modes are supported: bill-by-bandwidth (monthly subscription and hourly bandwidth), bill-by-traffic, and bandwidth package.
	<ul>
	<li>A pay-as-you-go instance supports three network billing modes: bill-by-bandwidth (hourly bandwidth), bill-by-traffic, and bandwidth package. Currently, the bandwidth package billing mode is in beta. To use it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li>
	</ul>
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
<td>The name can contain up to 60 letters, digits, hyphens, underscores, and dots. If it is not specified, a name will be automatically generated by default.
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
Only pay-as-you-go billing is supported.
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
Only the CLB instance type is supported. Starting from October 20, 2021, classic CLB instances can no longer be purchased. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/41387">Classic CLB End-of-Sale Notice</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network Type</span></td>
<td>There are two network types: public network and private network. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/13629#network-type">Network Types</a>.
	<ul>
	<li>Public network: CLB is used to distribute requests from the public network.</li>
	<li>Private network: CLB is used to distribute requests from the Tencent Cloud private network. A private network instance doesn't support the following configuration items and doesn't display them by default: <strong>IP Version</strong>, <strong>ISP Type</strong>, and <strong>Instance Specification</strong>.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">IP Version</span></td>
<td>
The following CLB IP versions are supported: IPv4, IPv6, and IPv6 NAT64. For more information on the use limits, see <a href="https://intl.cloud.tencent.com/document/product/214/13629#IP-type">IP Versions</a>.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">Network</span></td>
<td>
CLB supports classic network and VPC.
	<ul>
	<li>The classic network is a public network resource pool for all Tencent Cloud users. The private IPs of all CVMs are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses.</li>
	<li>By contrast, the VPC is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies.</li>
	</ul>
	Between the two options, VPC is more suitable for scenarios requiring custom network configurations, and the classic network product will be officially discontinued on December 31, 2022. We recommend you select VPC.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">ISP Type</span></td>
<td>
The following ISP types are supported: BGP, China Mobile, China Telecom, and China Unicom.<br/>
Currently, the static single-line IP is supported only in Guangzhou, Shanghai, Nanjing, Jinan, Hangzhou, Fuzhou, Beijing, Shijiazhuang, Wuhan, Changsha, Chengdu, and Chongqing. For its support in other districts, see the console. If you want to try it out, contact the sales rep for application. Once you are accepted, you can select an ISP (China Mobile, China Unicom, or China Telecom) on the purchase page.

</td>
</tr>
<tr>
<td><span style="font-weight:bold">Instance Specification</span></td>
<td>Shared and LCU-supported instances are supported.
	<ul>
	<li>Multiple shared instances share resources, and a single instance doesn't provide guaranteed performance. By default, all instances are shared instances.</li>
	<li>An LCU-supported instance guarantees the performance and doesn't preempt resources like a shared instance. Its forwarding performance is not affected by other instances. A single instance can sustain up to 1 million concurrent connections, 100,000 new connections per second, and 50,000 queries per second. Currently, the LCU-supported specification is in beta. To use it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li>
	</ul>
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
<td>The name can contain up to 60 letters, digits, hyphens, underscores, and dots. If it is not specified, a name will be automatically generated by default.
</td>
</tr>
</tbody></table>
:::
</dx-accordion>

4. After completing the above configuration, confirm the quantity and fees and click **Buy Now**.
 - Pay-as-You-Go billing mode: in the **Confirm** pop-up window, click **OK**.
5. After successful purchase, CLB will be activated and you can configure and use the CLB instance.

### [Shared instance purchase method](id:Shared-CLB-Instance)
1. Log in to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. Set the shared instance configuration items by referring to the steps in [Purchasing at Official Website](#Official-Purchase) and select **Shared** for **Instance Specification**.
![]()
3. Complete the subsequent operations by referring to the steps in [Purchasing at Official Website](#Official-Purchase).

### [LCU-Supported instance purchase method](id:LCU-CLB-Instance)
1. Log in to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. Set the LCU-supported instance configuration items by referring to the steps in [Purchasing at Official Website](#Official-Purchase) and select **LCU-supported** for **Instance Specification**.
<dx-tabs>
::: Pay-as-You-Go LCU-supported instance
![]()
:::
</dx-tabs>
3. Complete the subsequent operations by referring to the steps in [Purchasing at Official Website](#Official-Purchase).


## [Purchasing via API](id:API-Purchase)
To purchase a CLB instance via API, see [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/33841).

## Subsequent Operations
- You can create a listener for a CLB instance as instructed in [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
- You can bind a CLB listener to a real server as instructed in [Real Server Overview](https://intl.cloud.tencent.com/document/product/214/32388).

## Relevant Documentation
[Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629)
