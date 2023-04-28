Service migration is free to use. However, it may involve fees for **relay instances** and **network traffic**. This document describes the billable items and billing modes that may be involved when you use service migration.

## Relay Instances
- If the migration destination is a Cloud Virtual Machine (CVM) image, a relay instance named `do_not_delete_csm_instance` will be created under your account after the migration starts. The instance incurs instance fees and cloud disk fees.
- Billing mode: [pay-as-you-go](https://intl.cloud.tencent.com/document/product/213/2180)
- Do not reinstall, shut down, or terminate the relay instance or reset its password. It will be automatically terminated by the system after the migration ends.


## Network Traffic
Network traffic is generated during online migration, which is billed as follows:
- For migration over the public network, if your source server has a bandwidth plan, no additional fees will incur on the source server. The inbound traffic on the destination CVM does not incur fees.
- For migration over the public network, if your source server is billed by traffic, traffic fees will incur on the source server. The inbound traffic on the destination CVM does not incur fees.
- For migration through another channel, such as [a VPC peering connection](https://www.tencentcloud.com/document/product/553), [a VPN connection](https://www.tencentcloud.com/document/product/1037), [Cloud Connect Network](https://www.tencentcloud.com/document/product/1003), or [Direct Connect](https://www.tencentcloud.com/document/product/216), refer to the billing rules of the corresponding network service.
