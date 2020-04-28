Tencent Cloud Virtual Machine (CVM) is a scalable cloud computing service that frees you from having to estimate your resources usage and up-front investment. With Tencent Cloud CVM, you can start CVMs and deploy applications immediately.
Tencent Cloud CVM instances allow you to customize all resources, including CPU, memory, disk, network and security. It also allows the easy adjustment of the resources to cope with any change in demand.

## Concepts

Before using Tencent Cloud CVM, you should be familiar with the following concepts:
- **Instance**: a virtualized cloud computing resource, which includes CPU, OS, network, disks, and other basic components.
- **Instance type**: configurations of CPU, RAM, storage, and networking capacity for CVM instances. For more information, please see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
- **Image**: a template containing an operating system and applications that CVM instances run on. Tencent Cloud provides Windows, Linux, and other images.
- **Local disk**: a device that can be used for persistent storage by an instance on the same physical server as the disk.
- **Cloud disk**: a distributed and persistent block storage device provided by Tencent Cloud that can serve as the system disk or an expandable data disk of an instance.
- **VPC**: a virtual and isolated network space provided by Tencent Cloud that is logically separated from other resources.
- **IP address**: Tencent Cloud provides [Private Network Access](https://intl.cloud.tencent.com/document/product/213/5225) and [Public Network Access](https://intl.cloud.tencent.com/document/product/213/5224). Private network access is for traffic between CVM instances within the same LAN. Public network access is for public-facing services.
- **Elastic Public IP (EIP)**: static public network IP addresses designed especially for dynamic networks to meet demands for fast troubleshooting.
- **Security group**: security groups serve as virtual firewalls that are capable of status monitoring and packet filtering. They can be associated with one or more CVM instances to control network access. Security groups are an important aspect of network security measures.
- **Login**: you can log in to CVM instances using your [Login Password](https://intl.cloud.tencent.com/document/product/213/6093) or the more secure [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092).
- **Region and Availability Zone**: physical locations where CVM instances and other resources reside and are launched.
- **Tencent Cloud Console**: a web-based UI for managing resources.


## How do I use CVM instances? 

Tencent Cloud allows you to configure and manage CVM instances in the following ways:

- **Console**: a web-based UI for configuring and managing CVM instances.
- **API**: Tencent Cloud also provides APIs for configuring and managing CVM instances. For more information, refer to [API Overview](https://intl.cloud.tencent.com/document/api/213/15689).



## Purchasing and configuring CVM instances

If you are using a personal account and purchasing CVM instances for the first time, we recommend the following to get you started:
- [Quick Configuration for Windows CVMs](https://intl.cloud.tencent.com/document/product/213/2764).
- [Quick Configuration for Linux CVMs](https://intl.cloud.tencent.com/document/product/213/2936).

If you have specific needs that our standard CVM specifications cannot meet, use the following guides to learn how to obtain custom configurations:
- [Custom Configurations for Windows CVMs](https://intl.cloud.tencent.com/document/product/213/10516).
- [Custom Configurations for Linux CVMs](https://intl.cloud.tencent.com/document/product/213/10517).

## CVM Prices

CVM supports pay-as-you-go. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/213/2176).
For pricing information on CVM instances and other resources, refer to [Pricing](https://buy.cloud.tencent.com/price/cvm/overview).

## Relevant Products

- Auto Scaling lets you scale service clusters using pre-defined criteria such as time or load. For more information, refer to the [Auto Scaling documentation](https://intl.cloud.tencent.com/document/product/377).
- Cloud Load Balancer allows you to automatically distribute client traffic among multiple CVM instances. For more information, refer to the [Cloud Load Balancer documentation](https://intl.cloud.tencent.com/document/product/214).
- Tencent Kubernetes Engine enables you to manage the lifecycle of applications. For more information, refer to the [Tencent Kubernetes Engine documentation](https://intl.cloud.tencent.com/document/product/457).
- Cloud Monitor keeps track of your CVM instances and their system disks. For more information, refer to the [Cloud Monitor documentation](https://intl.cloud.tencent.com/document/product/248).
- You can deploy relational databases or use Tencent Cloud Databases. For more information, refer to the [TencentDB for MySQL documentation](https://intl.cloud.tencent.com/document/product/236).


