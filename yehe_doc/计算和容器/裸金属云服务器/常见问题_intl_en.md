
[](id:Q1)
### What is CBM?

CBM is a high-performing bare metal instance built on the latest virtualization technology of Tencent Cloud. It combines the elasticity of a virtual machine with the stable and strong computing performance of a physical machine. It can be integrated seamlessly with all Tencent Cloud products such as networks and databases. In addition, it supports third-party virtualization platforms to help you quickly build dedicated and isolated physical machine clusters in the cloud. With the nested virtualization technology, it also supports efficient and advanced hybrid cloud deployment with AnyStack.

[](id:Q2)
### Which operating systems does CBM support?
CBM shares the image system with CVM and supports CentOS, Ubuntu, and Windows operating systems, with more to come.

[](id:Q3)
### Where can I purchase CBM instances?
You can purchase CBM instances on the official purchase page or through the API/SDK.

[](id:Q4)
### How is CBM billed?

Currently, CBM supports the pay-as-you-go billing mode.

- In pay-as-you-go mode, instances are billed by second and settled hourly, and you can purchase or release the instances at any time. They are suitable for scenarios where the demand for devices fluctuates greatly and instantaneously, such as ecommerce flash sales. For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/1171/52407).

[](id:Q5)
### Does CBM support instance configuration adjustment?

- **Computing resources**: CBM instances are physical machine instances, which means all resources are exclusive and the configuration cannot be adjusted.
- **Storage resources**: You cannot adjust the number or capacity of local disks. For certain instances to which cloud disks can be mounted, you can flexibly expand the cloud disk storage space. For more information, see [CBM Instance Specification](https://www.tencentcloud.com/document/product/1171/52405).
- **ENIs**: For certain instances to which ENIs can be mounted, you can flexibly adjust the number of ENIs. For more information, see [CBM Instance Specification](https://www.tencentcloud.com/document/product/1171/52405).


[](id:Q6)
### How long does it take to reinstall the system for a CBM instance?

System reinstallation takes about three minutes for CBM instances of the cloud disk edition and about 15 minutes for CBM instances of the local disk edition. The latter is subject to the image size.
