### How do I use the NAT Gateway and EIP?
- The NAT gateway is able to translate between private IP addresses and public IP addresses in a VPC. It is an ingress or egress for public network traffic in a VPC. For more information about how to use Tencent Cloud’s NAT Gateway service, see [NAT Gateway](https://cloud.tencent.com/document/product/215/4975).
- The NAT gateway and EIP are two ways for the CVM to access the Internet. You can use either or both of them to design your public network access architecture.

### How do I configure port mapping on a NAT Gateway in the VPC?
Currently, dynamic NAT port mapping is used within the network and writing a static NAT is not supported.


### Where can I find more information about security?
Tencent Cloud provides various network and security services such as security groups, encrypted login, and EIPs to ensure that your instance provides internal and external services securely and efficiently. For more information about CVM security, see [Network and Security Overview](https://intl.cloud.tencent.com/document/product/213/5220).

### How do I prevent others from viewing my system?
You have full control over the visibility of your system, and the CVM allows you to place running instances into any security group of choice. In [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup), you can specify inter-group communication and IP subnets on the network that can communicate with the CVM.

### How do I troubleshoot security issues?
For suspected security risks or security issues, see the [Security Help Guide] for troubleshooting, and see [Host Security] to resolve security issues. 
