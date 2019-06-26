Cloud Connect Network (CCN) provides services for interconnection among Virtual Private Clouds (VPCs) and between VPCs and local IDCs. You can join VPC and Direct Connect Gateway instances to CCN to realize single-point access and full-mesh resource interconnection, making it easy to build a simple, intelligent, secure and flexible hybrid cloud and globally interconnected network.

**Note:** CCN is currently in internal trial. To use it, please submit a [ticket](https://console.cloud.tencent.com/workorder). We will review your application as soon as possible and notify you of the result via SMS and internal message. Thank you for your support.

## Features

CCN has the following features:

**Full-mesh interconnection**

Through the automatic forwarding and learning of full-mesh multi-node multi-level routing and second-level routing convergence, all network instances on CCN can be interconnected in one step for easy management.

**Intelligent learning and scheduling**

Based on the multi-node and multi-link full-mesh interconnection, CCN helps you do away with cumbersome routing maintenance work. Its intelligent scheduling system is based on the unified detection of full-mesh multi-level network topology, routing and traffic and supports local access and shortest path routing for local businesses.

**Automatically distributed routes**
The multi-level routing of CCN is capable of autonomous learning, so when the network topology changes, the routing can automatically learn and update, without the necessity for tedious operations such as configuration and modification. Further, management of CCN is simple and straightforward, greatly improving the scalability and OPS efficiency of the network.

## Differences from Peering Connection/Direct Connect Tunnel

Without CCN, if you want to achieve interconnection among multiple VPCs or between IDCs and multiple VPCs, you need to establish a peering connection between any two VPCs and a Direct Connect tunnel between each IDC and each VPC, and the IP address ranges of the VPCs and IDCs cannot overlap; otherwise, connections cannot be established. And after the connections are established, you need to manage the routing tables of all instances and manually add routing policies to realize interconnection.

However, if CCN is used in the scenario above, you only need to create a CCN instance and join all the VPCs and IDCs that require interconnection to the instance. After that, interconnection among all the VPCs and between IDCs and VPCs is achieved. The routes of CCN is automatically forwarded and capable of learning, so that you can join the instances to CCN with no repeated operations required, eliminating the need to manually configure and manage the routing tables of different instances.

> For more information on how to migrate existing businesses to CCN, see the [Best Practices](https://intl.cloud.tencent.com/document/product/1003/30078).

![img](https://main.qcloudimg.com/raw/7ea188ff1d607fc0141fee39ca4b2841.png)

## Components

CCN has the following components:

- CCN instance

  CCN instance is a necessary step to manage your network resources using CCN.
  To achieve interconnection, you only need to associate the network instances to be interconnected with the CCN instance without having to set up connections one by one.

- Network instance

  Currently, CCN supports associating the following types of network instances: VPC and Direct Connect Gateway.
  For more information, see [What Is a VPC](https://intl.cloud.tencent.com/document/product/215) and [Direct Connect Access](https://intl.cloud.tencent.com/document/product/216).

## Ultra-high Bandwidth Supported

CCN provides you with high-bandwidth and high-quality network services.
The upper egress cross-region interconnection bandwidth in each region is 1 Gbps by default. You can apply for higher bandwidth for the peering connections among Shanghai, Guangzhou, Korea and Hong Kong by [submitting a ticket](https://console.cloud.tencent.com/workorder).

