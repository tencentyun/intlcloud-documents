In order to host public-facing services on your CVM instance, which involves transmitting data over the Internet, you need a public IP address. Tencent Cloud provides Internet access via high-speed connected networks of Tencent Cloud IDC. The domestic multi-line BGP network covers more than 20 network operators and the public network egress can implement cross-region switchover in a matter of seconds. This ensures that your users can enjoy a high-speed and secure network no matter which networks they use.

## Public IP address
 - **Overview**: public IP addresses are non-reserved addresses on the Internet. A CVM with a public IP address can access other computers on the Internet and be accessed by other computers.
 - **Obtaining a public IP address**: set your bandwidth to more than 0 Mbps when creating your CVM instance. The system automatically picks a public IP address from the public IP address pool and assigns it to your instance. This address can be changed later. For details, refer to [Change Instance Public IP](https://intl.cloud.tencent.com/document/product/213/16642).
 - **Configuring your CVM instance**: you can log in to your CVM instance from a public network to configure it. For more information, refer to [Log in to Linux Instances](https://intl.cloud.tencent.com/document/product/213/5436) and [Log in to Windows Instances](https://intl.cloud.tencent.com/document/product/213/5435). 
 - **Translating your public IP address**: you can map your public IP address to [the private IP address](https://intl.cloud.tencent.com/document/product/213/5225) of your CVM instance using Network Address Translation (NAT). 
 - **Retrieving public IP address information**: all Tencent Cloud public network interfaces are managed by Tencent Gateway (TGW), which means all public network interfaces of all CVM instances are maintained by TGW. This process is imperceptible to CVM instances. Therefore, when you run the command `ifconfig` on your Linux CVM instance or `ipconfig` on your Windows CVM instance, you get [private IP address](https://intl.cloud.tencent.com/document/product/213/5225) information. For information regarding your public IP addresses, log in to your [CVM console](https://console.cloud.tencent.com/cvm) and check instance detail pages.
 - **Billing**: using public IP addresses to offer services may incur fees. For details, refer to [Public Network Billing Methods](https://intl.cloud.tencent.com/document/product/213/10578).

## Public IP Address Release
You cannot actively associate or release a public IP address that is already associated with an instance.
In the following cases, a public IP address associated with an instance is released or reassigned:
- **When you terminate an instance**. Tencent Cloud releases a public IP address when you terminate an on-demand CVM instance.
- When you associate or disassociate an [Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/5733) with an instance. When you associate an EIP with your instance, the existing public IP address is released back into the public IP pool. When you disassociate an EIP from your instance, Tencent Cloud assigns a new public IP address to your instance. You will not be able to use your old public IP address.

If you need a static public IP address, use an [Elastic Public IP (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).

## Operation Guide
For detailed instructions on how to obtain and change your public IP address, refer to:
- [Obtaining a Public IP Address of the Instance](https://intl.cloud.tencent.com/document/product/213/17940)
- [Changing Your Public IP Address](https://intl.cloud.tencent.com/document/product/213/16642)
