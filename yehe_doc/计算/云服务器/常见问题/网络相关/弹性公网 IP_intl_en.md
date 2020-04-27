### What are EIPs used for?
ElPs are applicable to the following scenarios:
- Disaster recovery. We strongly recommend you use EIPs for disaster recovery. For example, when one of your servers fails, you can unbind the EIP from this server and then bind it to a healthy server to quickly resume services.
- Retaining a specific public IP. If you need to retain a specific public IP under your account, you can convert it to an EIP, which can be unbound/bound with the device and used to access the public network. This EIP will be retained under your account until you "release" it.
- Other special cases. When you need to change an IP in some cases, you can convert the public IP to an EIP and then bind/unbind the EIP. With limited EIP resources available, however, each account has an EIP quota for each region. Please use and plan accordingly.

### How is an EIP billed?

1. The fee displayed on the console applies to EIPs that have been idle for more than 1 hour. EIPs can be billed with an accuracy down to seconds. EIPs that have been bound/unbound multiple times are billed based on the total duration (in sec) for which they are unbound.
2. EIPs that have been idle for less than 1 hour are billed for resource occupation fee on a pro rata basis.

### When is an EIP billed?
You can apply for, bind, unbind and release EIPs. With limited EIP resources available, an EIP is billed for a small usage fee only when it is unbound.

### How do I stop EIP billing?
- When you no longer need an EIP, you can release it to stop the billing.
For more information on the specific operations, see [Releasing EIPs](https://intl.cloud.tencent.com/document/product/213/16586).
- If you need to retain an EIP but want to stop the billing, bind it to a device (CVM, NAT). A bound EIP will not be billed.

### How can a CVM without public IP access public network?
If you did not purchase the public IP when purchasing the CVM or have returned the public IP, you can apply for an EIP on the [ElP Console](https://console.cloud.tencent.com/cvm/eip) and bind it to your CVM to allow public network access.

### Can I change my public IP?

You can change the public IP of your CVM. For more information on the specific operations, please see [Change Instance Public IP](https://intl.cloud.tencent.com/document/product/213/16642).

### How do I keep a public IP unchanged?

If you need to retain a specific public IP under your account, you can convert it to an EIP, which can be bound to the device and used to access the public network. This EIP will be retained under your account until you **released** it.
For more information on the related operations, see [Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/16586).

### Can an EIP be converted back to a public IP?

An EIP cannot be converted back to a public IP.

### Can an EIP be retrieved?
You can retrieve public IPs that have not been assigned to other users. For details, see [Retrieve the public network IP address](https://intl.cloud.tencent.com/document/product/213/32719).

