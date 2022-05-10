### How do I bind a CVM?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc) to bind your CVM. For more information, see [Binding CVM](https://intl.cloud.tencent.com/document/product/576/18535).

### How do I configure an ENI on the CVM?
After being bound in the console, the ENI needs to be configured on the CVM before it can be used. For more information, see [Binding and Configuring an ENI](https://intl.cloud.tencent.com/document/product/576/41740).

### How do I assign private IPs?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc) to assign private IPs to an ENI that is bound to the CVM, and configure them to take effect. For more information, see [Requesting Secondary Private IPs](https://intl.cloud.tencent.com/document/product/576/32938).

### How do I delete an ENI?
You can only delete the ENIs that are not bound to a CVM. For more information, see [Deleting an ENI](https://intl.cloud.tencent.com/document/product/576/18536).

### How do I unbind an ENI from a CVM?
You can log in to the [VPC Console](https://console.cloud.tencent.com/vpc) to unbind the ENI from the CVM. For more information, see [Unbinding an ENI from a CVM](https://intl.cloud.tencent.com/document/product/576/18537).

### How do I release private IPs?
You can only release secondary private IPs. For more information, see [Releasing Secondary Private IPs](https://intl.cloud.tencent.com/document/product/576/18538).

### How do I bind EIPs?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc) to bind EIPs. For more information, see [Binding EIPs](https://intl.cloud.tencent.com/document/product/576/18539).

### How do I unbind EIPs?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc) to unbind EIPs. For more information, see [Unbinding EIPs](https://intl.cloud.tencent.com/document/product/576/18540).

### How do I modify primary private IPs?
You can modify the primary private IP of a CVM’s primary ENI, but the primary private IP of a secondary ENI cannot be modified. For more information, see [Modifying Primary Private IPs](https://intl.cloud.tencent.com/document/product/576/18541).

### How do I modify the subnet of an ENI?
You can only modify the subnet of the primary ENI. For more information, see [Modifying the Subnet of an ENI](https://intl.cloud.tencent.com/document/product/576/18542).

[](id:1)

### When I create an ENI and use it as the secondary ENI of a CVM, is the secondary ENI in the same subnet with the primary ENI of the instance?
The secondary ENI bound to a CVM instance can be in a different subnet with the primary ENI. However, the secondary ENI and the primary ENI must be under the same availability zone in the same VPC.
