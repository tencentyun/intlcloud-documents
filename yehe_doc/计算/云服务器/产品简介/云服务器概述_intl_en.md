## CVM Overview

Tencent Cloud Virtual Machine (CVM) is a scalable cloud computing service that frees you from having to estimate your resources usage and investing up-front. With Tencent Cloud CVM, you can start CVMs and deploy applications immediately.
Tencent Cloud CVM instances allow you to customize all resources, including CPU, memory, disk, network, and security. They also allow you to easily adjust the resources in response to any change in demand.

## Using CVM instances

Tencent Cloud allows you to configure and manage CVM instances in the following ways:
- **Console**: a web-based UI for configuring and managing CVM instances.
- **API**: Tencent Cloud also provides APIs for configuring and managing CVM instances. For more information, see [API Category](https://intl.cloud.tencent.com/document/api/213/15689).
- **SDK**: You can use [SDK] (https://intl.cloud.tencent.com/document/product/494) or [Tencent Cloud CLI](https://intl.cloud.tencent.com/document/product/1013) to call CVM APIs.

## Key Concepts

Before using Tencent Cloud CVM, you should familiarize yourself with the following concepts:
- **Instance**: a virtual cloud computing resource that includes CPU, memory, OS, network, disks, and other basic components.
- **Instance type**: configurations of CPU, RAM, storage, and networking capacity for CVM instances. For more information, please see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
- **Image**: a pre-configured template containing an operating system and applications that CVM instances run on. Tencent Cloud CVM provides pre-configured images for Windows, Linux, etc.
- **Local disk**: a device that can be used for persistent storage by an instance on the same physical server as the disk.
- **Cloud disk**: a distributed and persistent block storage device provided by Tencent Cloud that can serve as the system disk or an expandable data disk of an instance.
- **VPC**: a virtual and isolated network space provided by Tencent Cloud that is logically separated from other resources.
- **IP address**: Tencent Cloud provides [private network access](https://intl.cloud.tencent.com/document/product/213/5225) and [public network access](https://intl.cloud.tencent.com/document/product/213/5224). Private network access is for traffic between CVM instances within the same LAN, while public network access is for public-facing services.
- **Elastic IP (EIP)**: static public network IP addresses designed especially for dynamic networks to meet the demands for fast troubleshooting.
- **Security group**: security groups serve as virtual firewalls that are capable of status monitoring and packet filtering. They can be associated with one or more CVM instances to control network access. Security groups are an important measure for network security and isolation.
- **Login**: you can log in to CVM instances using your [login password](https://intl.cloud.tencent.com/document/product/213/6093) or the more secure [SSH key](https://intl.cloud.tencent.com/document/product/213/6092).
- **Region and availability zone**: physical locations where CVM instances and other resources reside and are launched.
- **Tencent Cloud Console**: a web-based UI for managing resources.




## Customizing CVM Configurations

If you have specific needs that our standard CVM specifications cannot meet, use the following guides to learn how to obtain custom configurations:
- [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516)
- [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517)

## CVM Prices

CVM supports pay-as-you-go. For more information, see [Price Overview of CVM Instances](https://intl.cloud.tencent.com/document/product/213/2176).
For pricing information on CVM instances and other resources, refer to [Product Pricing](https://buy.cloud.tencent.com/price/cvm/overview).

## Relevant Products

- Auto Scaling lets you scale server clusters using pre-defined criteria such as time or load. For more information, refer to the [Auto Scaling documentation] (https://intl.cloud.tencent.com/document/product/377).
- Cloud Load Balancer allows you to automatically distribute client traffic among multiple CVM instances. For more information, refer to the [Cloud Load Balancer documentation](https://intl.cloud.tencent.com/document/product/214).
- Tencent Kubernetes Engine allows you to manage the lifecycle of applications in a CVM. For more information, refer to the [Tencent Kubernetes Engine documentation](https://intl.cloud.tencent.com/document/product/457).
- Cloud Monitor keeps track of your CVM instances and their system disks. For more information, refer to the [Basic Cloud Monitor documentation](https://intl.cloud.tencent.com/document/product/248).
- You can deploy a relational database on the cloud or use TencentDB. For more information, refer to the [TencentDB for MySQL documentation](https://intl.cloud.tencent.com/document/product/236).


