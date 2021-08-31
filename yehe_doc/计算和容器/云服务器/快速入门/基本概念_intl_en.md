
### Instance
An instance is a Cloud Virtual Machine (CVM), which is a virtual computing resource containing CPU, memory, OS, network, disks, and other basic computing components.
CVM instances provide secure, reliable and elastic computing services in the cloud to meet computing requirements. As business demands change, computing resources can be scaled in real time to lower your software and hardware costs and simplify IT OPS work.

### Instance Type
Tencent Cloud provides various configurations of CPU, MEM, storage, and networking capacity for CVM instances. For more information, please see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).

### Image
An image is a pre-configured template containing an operating system and applications that CVM instances run on. Tencent Cloud CVM provides pre-configured images for Windows, Linux, etc.

### Cloud Block Storage
Cloud Block Storage (CBS) is a highly available, highly reliable, low-cost, and customizable block storage device. It can be used as a standalone and expandable disk for CVM, providing efficient and reliable [storage](https://intl.cloud.tencent.com/document/product/213/4952) devices.

### VPC
A VPC is a logically isolated virtual network space in Tencent Cloud.

### IP Addresses
Tencent Cloud provides [private IP address](https://intl.cloud.tencent.com/document/product/213/5225) and [public IP address](https://intl.cloud.tencent.com/document/product/213/5224). Private IP address is for the interconnection of CVM instances within the same LAN, while public IP address is for public-facing services.

### Elastic IP
Elastic IP (EIP) is static public network IP addresses designed especially for dynamic networks to meet the demands for fast troubleshooting.
An EIP is a public IP address that can be applied for independently. It supports dynamic binding and unbinding. You can bind it to or unbind it from the CVM (or NAT Gateway instances) under your account. Its main uses are:
- To retain an IP. ICP domain name filing is required for Chinese mainland IP and DNS.
- To mask an instance failure. For example, a DNS name is mapped to an IP address through dynamic DNS mapping. It may take up to 24 hours to propagate this mapping to the entire Internet, while an elastic IP enables quick remapping of an IP from one CVM to another. When one CVM fails, you can just start and remap another instance to quickly respond to instance failures.

### Security Group
A security group is a virtual firewall that features stateful data packet filtering. It is used to configure the network access control of CVMs. You can add CVM instances with the same network security isolation requirements in the same region to the same security group, to filter the inbound and outbound traffic of the CVM through the network policies of the security group.

### Login Method
The password is a unique login credential for the CVM instance. To ensure instance security, Tencent Cloud provides the following two encrypted login methods:
- [SSH key pairs](https://intl.cloud.tencent.com/document/product/213/6092) are easier to use. You can log in to instances remotely with a few simple configuration steps on the console and your local client, and do not need to enter a password when you log in again.
- [Login password](https://intl.cloud.tencent.com/document/product/213/6093) allows anyone with the password to log in to the CVM instance remotely through a public network address allowed by the security group.

### Regions and Availability Zones
Physical locations where CVM instances and other resources reside and are launched.
- A region refers to a geographical location where data centers hosted by Tencent Cloud are located. Each region has multiple availability zones.
- An availability zone is a Tencent Cloud IDC with an independent power supply and network in the above region. It can ensure business stability, as failures in one AZ are isolated without affecting other AZs in the same region.



