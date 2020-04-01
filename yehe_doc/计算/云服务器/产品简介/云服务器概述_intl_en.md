Tencent Cloud CVM provides scalable compute capacity in the cloud, freeing you from estimation of resource usage and upfront investment. With Tencent Cloud CVM, you can launch CVM instances and deploy applications faster.
Tencent Cloud CVM allows you to customize all resources, such as CPU, memory, storage, networking, security, etc. You can also adjust them easily when demand changes.

## Concepts

Before using Tencent Cloud CVM, you should be familiar with the following concepts:
- **Instance**: Virtual computing resources on the cloud, including CPU, operating system, networking, disk and other basic computing components.
- **Instance type**: Configurations of CPU, RAM, storage, and networking capacity for CVM instances. For more information, please see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
- **Image**: A preset instance template, including environment preconfiguration for the server (operating system and other installed software). Tencent Cloud CVM provides preset images for Windows, Linux, etc.
- **Local disk**: A device on the same physical server as the instance and can be used for persistent storage by the instance.
- **Cloud disk**: A distributed and persistent block storage device, which can be used as the system disk or expandable data disk of an instance.
- **Virtual Private Cloud**: Virtual networks provided by Tencent Cloud that are logically isolated from other resources.
- **IP address**: Tencent Cloud provides [Private IP](https://intl.cloud.tencent.com/document/product/213/5225?from_cn_redirect=1) and [Public IP](https://intl.cloud. tencent.com/document/product/213/5224). Private IP provides local area network (LAN) where CVM instances can access each other. Public IP is used when users access Internet services on the CVM instance.
- **Elastic IP**: Static public IP designed for dynamic networks to meet demands for fast troubleshooting.
- **Security group**: Virtual firewall for monitoring status and filtering packets. Security group can be associated with one or multiple CVM instances to control network access. It is an important measure for network security and isolation.
- **Login method**: Use standard [login password](https://intl.cloud.tencent.com/document/product/213/6093) or the highly secure [SSH key](https://intl.cloud.tencent.com/document/product/213/6092).
- **Region and availability zone**: Locations of instances and other resources.
- **Tencent Cloud Console**: Web-based user interfaces.


## How do I use CVMs? 

Tencent Cloud allows you to configure and manage the CVM in the following ways:

- **Console**: Web-based user interface provided by Tencent Cloud to configure and manage the CVM.
- **API**: Tencent Cloud also provides API for you to manage the CVM. For API description, please see [API Overview](https://intl.cloud.tencent.com/document/api/213/15689?from_cn_redirect=1).
- **SDK**: You can use [SDK Programming](https://intl.cloud.tencent.com/document/product/494) or Tencent Cloud [Command Line CLI](https://intl.cloud.tencent.com/document/product/1013) to call the CVM API.



## CVM purchase and quick configuration

If you are a new user of Tencent Cloud CVM, we recommend you use quick configuration, please see:
- [Quick Configuration for Windows CVM](https://intl.cloud.tencent.com/document/product/213/2764)
- [Quick Configuration for Linux CVM](https://intl.cloud.tencent.com/document/product/213/2936)

If you have higher requirements for CVM configuration, such as custom configurations for storage, capacity, network bandwidth, and security group, please see:
- [Custom Configuration for Windows CVM](https://intl.cloud.tencent.com/document/product/213/10516)
- [Custom Configuration for Linux CVM](https://intl.cloud.tencent.com/document/product/213/10517)

## CVM Pricing

For pricing details of CVM and other resources, see [Product Pricing](https://buy.cloud.tencent.com/price/cvm/overview).

## Other related products

- You can use auto scaling to automatically increase and decrease the number of server clusters based on configured policies or business needs. For more information, please see [Auto Scaling](https://intl.cloud.tencent.com/document/product/377?from_cn_redirect=1) product documentation.
- You can use Cloud Load Balancer to automatically distribute request traffic from the client among multiple CVM instances. For more information, please see [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214?from_cn_redirect=1) product documentation.
- You can use Tencent Kubernetes Engine to manage the lifecycles of containerized applications in CVM. For more information, please see [Tencent Kubernetes Engine](https://intl.cloud.tencent.com/document/product/457?from_cn_redirect=1) product documentation.
- You can use Cloud Monitor to monitor CVM instances and their system disks. For more information, please see [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248?from_cn_redirect=1) product documentation.
- You can deploy a relational database on the cloud or use TencentDB. For more information, please see [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236?from_cn_redirect=1) product documentation.


