## Public IP

### How can a CVM without public IP access public network?
If you did not purchase the public IP when purchasing the CVM or have returned the public IP, you can apply for an EIP on the [EIP Console](https://console.cloud.tencent.com/cvm/eip) and bind it to your CVM to allow public network access.

### Can I change my public IP?

You can change the public IP of your CVM. For more information on specific operations, please see [Changing Instance Public IP](https://intl.cloud.tencent.com/document/product/213/16642).

### How do I keep a public IP unchanged?

If you need to retain a specific public IP under your account, you can convert it to an EIP, which can be bound to the device and used to access the public network. This EIP will be retained under your account until you **release** it.
For more information on the related operations, see [EIP](https://intl.cloud.tencent.com/document/product/213/16586).

### What is a public IP address?
A public IP address is an unreserved IP address on the Internet. A CVM with a public IP address can be accessible to and by other computers on the Internet.
For more information, see [Internet Access](https://intl.cloud.tencent.com/document/product/213/5224).

### How do I obtain the public IP address of an instance?
For details, see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).

### How do I change the public IP address of an instance?
For details, see [Changing Instance Public IP](https://intl.cloud.tencent.com/document/product/213/16642).

### What are the differences between public gateways and CVMs with public IP addresses?
Public gateways enable the public network traffic forwarding feature in the image. However, CVMs with public IP addresses do not have this feature by default. Therefore, CVMs created on Windows public image cannot function as public gateways because the Windows image has no traffic forwarding feature.

### Why can’t I change the public IP of my CVM?
Possible reasons include:
- The CVM instance is shut down and incurs no charges when shut down.
- The public IP of the CVM has been changed.


### How can I obtain the public IP address of an instance that has no public IP (IPv4) assigned during the instance creation?
- You can obtain the public IP of an instance by applying and binding an EIP to it. For the step-by-step operations, see [EIP](https://intl.cloud.tencent.com/document/product/213/16586).

## Private IP

### What is a private IP address?
A private IP address cannot be accessed through the Internet. That is how Tencent Cloud provides private network services.
For more information, please see [Private Network Access](https://intl.cloud.tencent.com/document/product/213/5225).

### How do I obtain the private IP address of an instance?
For details, see [Getting Private IP Addresses and Setting DNS](https://intl.cloud.tencent.com/document/product/213/17941).

### Can I change the private IP address of an instance in addition to its public IP address?
Yes, you can change the private IP of an instance. For operations, see [Modifying Private IP Addresses](https://intl.cloud.tencent.com/document/product/213/16561)

