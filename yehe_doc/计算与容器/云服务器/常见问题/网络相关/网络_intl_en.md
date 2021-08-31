### There is no network connection after I log in to the CVM. How to troubleshoot this problem?
This may be caused by the incorrect configuration of your CVM security groups. Please check the inbound and outbound rules of the security groups. Check whether your destination, protocol ports and policies are prohibited.

### Can a VPC instance interconnect with the basic network instance?

#### Yes, but it has the following restriction:

The VPC IP address range (CIDR) must be 10.0.0.0/16 - 10.0.47.0/16 (including subsets). Otherwise, there will be conflicts.

#### Directions

Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1), click the VPC ID/name to enter its details page, and then click the **Classiclink** tab to associate the basic network CVM to be interconnected. 

### How do I view basic network CVMs that are interconnected with VPC CVMs?

Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1), click the VPC ID/name to enter its page, and view basic network CVMs interconnected with VPC CVMs in **Classiclink".

### Can the CVM be switched to an overseas network?

The network cannot be changed for CVM after purchase. If you need an overseas network, we recommend that you return the CVM and purchase an overseas CVM.

### How do I configure a private network DNS?

Please see [Private Network DNS](https://intl.cloud.tencent.com/document/product/213/5225).

### Within the same IP range, the VPN can obtain the IP address of an IP range but cannot access the internet. How do I solve this problem?

Please check that the following configurations are correct:

1. Are the manually added IP and the automatically obtained IP in the same IP subnet? Are the subnet masks the same? Is the default gateway configured? Is the default gateway address correct?
2. Is DNS configured and is the DNS address correct?
3. If all of the configurations above are correct, check if the statically configured IP address has an IP conflict.
  
If none of the above works, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.
