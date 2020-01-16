## Overview
As a complement to Cloud Virtual Machine (CVM), Tencent Cloud CVM Dedicated Host (CDH) provides you with exclusive physical server resources that meet the requirements for resource exclusivity, physical isolation, security and compliance. CDH is equipped with Tencent Cloud's virtualized system. Once purchased, CDH can help you flexibly create and manage multiple CVM instances with custom specs and plan the use of physical resources.

## Related Concepts

The following concepts are usually involved in CDH:

- [**Host type**](<https://intl.cloud.tencent.com/document/product/416/5068>): The type of host. Hardware configuration varies for different types of hosts.

- **Local disk type**: The type of disk on the host. Disk type varies for different types of hosts. Currently, there are two types of local disks: local HDD and local SSD.

- **CVM instance**: The dedicated CVM instance assigned on the host; referred to as dedicated instance in some documents.

- [**Cloud Block Storage**](https://intl.cloud.tencent.com/document/product/213/4953): Distributed persistent block storage device provided by Tencent Cloud that can be used as a system disk of an instance or an expansion data disk.

- [**Image**](<https://intl.cloud.tencent.com/document/product/213/4940>): A preset instance template that contains the instance's pre-configured environment (operating system and other installed software).

- [**Virtual Private Cloud**](<https://intl.cloud.tencent.com/document/product/215/535>): Custom virtual network space that is logically isolated from other resources.

- **IP address**: The internal and external service addresses of the CVM instance, i.e. [private IP address](<https://intl.cloud.tencent.com/document/product/213/5225>) and [public IP address](<https://intl.cloud.tencent.com/document/product/213/5224>).

- [**SSH key**](<https://intl.cloud.tencent.com/document/product/213/6092>): A way to log in to a Linux-based CVM instance more secure than regular passwords.

- [**Security group**](<https://intl.cloud.tencent.com/document/product/213/12452>): Security controls of the access to instances by specifying inbound and outbound IP, protocol and port rules.

- [**Region and availability zone**](<https://intl.cloud.tencent.com/document/product/213/6091>): The start-up location of the resources.


## **Relevant Services**

- CDH is used by assigning CVM instances on it. For more information about using CVM instances, see [CVM User Guide](https://intl.cloud.tencent.com/document/product/213/16918).

- You can use Cloud Load Balancer (CLB) to automatically distribute request traffic from clients across multiple CVM instances. For more information, see [CLB Product Documentation](https://intl.cloud.tencent.com/doc/product/214).
- You can deploy a relational database in the cloud or use a Tencent Cloud database. For more information, see [TencentDB for MySQL](https://intl.cloud.tencent.com/doc/product/236).
- You can write code to call the Tencent Cloud API to access Tencent Cloud products and services. For more information, see [Tencent Cloud API Documentation](<https://intl.cloud.tencent.com/document/api>).

## Using CDH

CDH has web-based UIs (i.e. console). If you have already signed up for a Tencent Cloud account, you can log in to the [CDH Console](https://console.cloud.tencent.com/cvm/cdh) to perform various operations on the CVM instances.

CDH also provides various APIs for host management. For more information about CDH API operations, see the [API Documentation](https://intl.cloud.tencent.com/document/api/213/16473)

You can use the SDK (with PHP, Python, Java, .NET and Node.js supported) for programming or use the Tencent Cloud Command Line Interface (CLI) to call the CVM API. 






