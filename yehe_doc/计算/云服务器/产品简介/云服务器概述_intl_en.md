## CVM Overview

Tencent Cloud Virtual Machine (CVM) is a scalable cloud computing service that frees you from estimation of resource usage and upfront investment. With Tencent Cloud CVM, you can start CVMs and deploy applications immediately.
You can customize all resources of a CVM instance, including CPU, memory, disk, network, and security policies. You can also easily adjust the resources in response to any change in demand.

## Working with CVM Instances

You can configure and manage CVM instances in the following ways:
- **Console**: A web-based UI for configuring and managing CVM instances.
- **API**: Tencent Cloud also provides APIs for configuring and managing CVM instances. For more information, see [API Category](https://intl.cloud.tencent.com/document/api/213/15689).
- **SDK**: You can use [SDK](https://intl.cloud.tencent.com/document/product/494) or [Tencent Cloud CLI](https://intl.cloud.tencent.com/document/product/1013) to call CVM APIs.

## Key Concepts

Before using Tencent Cloud CVM, you should familiarize yourself with the following concepts:
<table>
<tr>
<th width="12%">Concept</th><th>Description</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4939">Instance</a></td>
<td>A virtual computing resource containing basic computing components such as CPU, memory, OS, network, and disks. Tencent Cloud provides various configurations of CPU, MEM, storage, and networking capacity for CVM instances. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/11518">Instance Types</a>.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">Image</a></td>
<td>A pre-configured template containing an operating system and applications that CVM instances run on. Tencent Cloud CVM provides pre-configured images for Windows, Linux, etc.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4953">Cloud Block Storage</a></td>
<td>A distributed and persistent block storage device provided by Tencent Cloud that can serve as the system disk or an expandable data disk of an instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/215/535">Virtual Private Cloud</a></td>
<td>A logically isolated virtual network space in Tencent Cloud.</td>
</tr>
<tr>
<td>IP address</td>
<td>Tencent Cloud provides <a href="https://intl.cloud.tencent.com/doc/product/213/5225">Private IP</a> and <a href="https://intl.cloud.tencent.com/document/product/213/5224">Public IP</a> addresses. Private IP addresses are for the interconnection of CVM instances within the same LAN, while public IP addresses are for public-facing services.</td>
</tr>
<tr>
<td>Elastic IP</td>
<td>Static public network IP addresses designed especially for dynamic networks to meet the demands for fast troubleshooting.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/12452">Security group</a></td>
<td>A virtual firewall that features stateful data packet filtering. It is used to configure the network access control of CVMs. Security groups are an important measure for network security and isolation.</td>
</tr>
</table>

## Purchasing and Customizing CVM Instances

If you have specific needs that our standard CVM specifications cannot meet, use the following guides to learn how to obtain custom configurations:
- [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516)
- [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517)

## CVM Pricing

CVM supports pay-as-you-go. For more information, see [Price of CVM Instance](https://intl.cloud.tencent.com/document/product/213/2176).
For pricing information on CVM instances and other resources, refer to [Product Pricing](https://buy.cloud.tencent.com/price/cvm/overview).

## Relevant Products

- Auto Scaling lets you scale server clusters using pre-defined criteria such as time or load. For more information, refer to the [Auto Scaling documentation](https://intl.cloud.tencent.com/document/product/377).
- Cloud Load Balancer allows you to automatically distribute client traffic among multiple CVM instances. For more information, refer to the [Cloud Load Balancer documentation](https://intl.cloud.tencent.com/document/product/214).
- Tencent Kubernetes Engine allows you to manage the lifecycle of applications in a CVM. For more information, refer to the [Tencent Kubernetes Engine documentation](https://intl.cloud.tencent.com/document/product/457).
- Cloud Monitor keeps track of your CVM instances and their system disks. For more information, refer to the [Basic Cloud Monitor documentation](https://intl.cloud.tencent.com/document/product/248).
- You can deploy a relational database on the cloud or use TencentDB. For more information, refer to the [TencentDB for MySQL documentation](https://intl.cloud.tencent.com/document/product/236).


