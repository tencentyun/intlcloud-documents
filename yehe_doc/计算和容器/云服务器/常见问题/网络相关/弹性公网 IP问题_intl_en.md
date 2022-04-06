### What are EIPs used for?
ElPs are applicable to the following scenarios:
- Disaster recovery. We strongly recommend you use EIPs for disaster recovery. For example, when one of your servers fails, you can unbind the EIP from this server and then bind it to a healthy server to quickly resume services.
- Retaining a specific public IP. If you need to retain a specific public IP under your account, you can convert it to an EIP, which can be bound with or unbound from the device and used to access the public network. This EIP will be retained under your account until you "release" it.
- Other special cases. When you need to change an IP in some cases, you can convert the public IP to an EIP and then bind the EIP to or unbind from your device. But the EIP resource under an account is limited in each region, please plan and use EIPs accordingly.

### How is an EIP billed?

1. The fee displayed on the console applies to EIPs that have been idle for more than 1 hour. EIPs can be billed accurately to seconds. EIPs that have been bound/unbound multiple times are billed based on the total duration (in sec) for which they are unbound.
2. EIPs that have been idle for less than 1 hour are billed for resource occupation fee on a pro rata basis.

### When is an EIP billed?
You can apply for, bind, unbind or release EIPs. With limited EIP resources available, an EIP is billed for a small resource occupation fee only when it is unbound.

### How do I stop EIP billing?
- When you no longer need an EIP, you can release it to stop the billing.
For more information on the specific operations, see [Releasing EIPs](https://intl.cloud.tencent.com/document/product/213/16586).
- If you need to retain an EIP but want to stop the billing, bind it to a device (such as CVM or NAT). A bound EIP will not be billed.

### Can an EIP be converted back to a public IP?

An EIP cannot be converted back to a public IP.

### Can an EIP be retrieved?
You can retrieve public IPs that have not been assigned to other users. For details, see [Retrieving the Public IP Address](https://intl.cloud.tencent.com/document/product/213/32719).

