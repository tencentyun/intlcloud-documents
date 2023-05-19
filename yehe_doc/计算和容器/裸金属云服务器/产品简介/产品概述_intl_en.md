## CBM overview

Cloud Bare Metal (CBM) is a bare metal cloud service combining the elasticity of virtual machines and the performance of physical machines. It can be seamlessly integrated with all Tencent Cloud products such as networks, storage, and databases to sustain dedicated, high-performance, and isolated physical machine clusters in the cloud.

CBM's CPU and memory can be directly accessed by your business applications without incurring virtualization costs. With CBM, you only need to add or remove physical machines based on business characteristics and can get physical machines within just minutes. CBM frees you from troublesome capacity management and Ops, so that you can focus more on business innovation.

## Concepts

Before using CBM, you should familiarize yourself with the following concepts:

<table>
<tr>
<th width="16%"><b>Concept</b></th>
<th><b>Description</b></th>
</tr>
<tr>
<td><b><a href="https://intl.cloud.tencent.com/document/product/213/4939">Instance</a></b></td>
<td>A public cloud computing resource containing basic computing components such as CPU, memory, operating system, network, and disk.</td>
</tr>
<tr>
<td><b><a href="https://www.tencentcloud.com/document/product/1171/52405">Instance specification</a></b></td>
<td>Different CPU, memory, storage, and network configurations coming with different Tencent Cloud servers.</td>
</tr>
<tr>
<td><b><a href="https://intl.cloud.tencent.com/document/product/213/4940">Image</a></b></td>
<td>CBM is fully compatible with the CVM image system and provides preconfigured Windows and Linux images.</td>
</tr>
<tr>
<td><b><a href="https://intl.cloud.tencent.com/document/product/213/5798">Local disk</a></b></td>
<td>A device on the physical machine that can be used for persistent storage by an instance.</td>
</tr>
<tr>
<td><b><a href="https://intl.cloud.tencent.com/document/product/213/4953">Cloud disk</a></b></td>
<td>A distributed and persistent block storage device provided by Tencent Cloud that can serve as the system disk or an expandable data disk of an instance.</td>
</tr>
<tr>
<td><b><a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a></b></td>
<td>A logically isolated virtual network space in Tencent Cloud.</td>
</tr>
<tr>
<td><b>IP</b></td>
<td>Tencent Cloud provides <a href="https://intl.cloud.tencent.com/document/product/213/5225">private</a> and <a href="https://intl.cloud.tencent.com/document/product/213/5224">public</a> IPs. Simply put, a private IP provides a LAN service for access between CBM instances, while a public IP is used for you to access an internet service on a CBM instance.</td>
</tr>
<tr>
<td><b>EIP</b></td>
<td>Static public network IP addresses designed especially for dynamic networks to meet the demands for fast troubleshooting.</td>
</tr>
<tr>
<td><b><a href="https://intl.cloud.tencent.com/document/product/213/12452">Security group</a></b></td>
<td>A virtual firewall that can check the status and filter data packets. As an important means for network security isolation, it can be used to set network access controls for one or more CBM instances.</td>
</tr>
<tr>
<td><b>Login method</b></td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/6093">Login password</a> or the more secure <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH key pair</a>.</td>
</tr>
<tr>
<td><b><a href="https://intl.cloud.tencent.com/document/product/213/6091">Region and AZ</a></b></td>
<td>The startup location of instances and other resources. CBM instances in the same VPC are interconnected over the private network, which means they can communicate through private IPs, even if they are in different AZs of the same region.</td>
</tr>
<tr>
<td><b>Tencent Cloud console</b></td>
<td>Web-based UIs.</td>
</tr>
</table>



## Usage

Tencent Cloud allows you to configure and manage CBM instances in the following ways:
* **Console**: You can configure and manage CBM instances on the web UIs of CVM.
* **API**: Tencent Cloud provides APIs for configuring and managing CBM instances. For more information, see [API Category](https://www.tencentcloud.com/document/api/213/15689).
* **SDK**: You can use the SDK or TCCLI to call APIs.


<dx-alert infotype="explain" title="">
If you have never used CBM, you can try it out as instructed in [Getting Started](https://www.tencentcloud.com/document/product/1171/52410).
</dx-alert>



## Billing overview
For CBM billing details, see [Billing Overview](https://www.tencentcloud.com/document/product/1171/52407).
