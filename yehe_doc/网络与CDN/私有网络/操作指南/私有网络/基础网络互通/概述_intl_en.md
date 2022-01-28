The Classiclink feature allows VPC-based resources to communicate with classic network-based CVMs.  For example,
+ The classic network-based CVMs can communicate with VPC resources such as CVM, TencentDB, private network CLB, Redis/CMEM, etc.
+ VPC resources can only access classic network-based CVMs, but not other resources in the classic network, like TencentDB and CLB 
![](https://main.qcloudimg.com/raw/5c4c66605c6ecd04591dfff5236231df.png) 

## Use Limits
- A VPC can only be interconnected with the classic network **in the same region**.
- The VPC IP range must be within `10.0.0.0/16-10.47.0.0/16` (including subsets), otherwise there may be IP conflicts, which may cause failure while associating and communicating with the classic network-based CVMs.
- A classic network-based CVM can only be associated with one VPC at a time.
- One VPC supports associating with up to 100 classic network-based CVMs.
- After the classic network-based CVMs are associated with a VPC, classic network-based CVMs can only communicate with resources in primary CIDR block rather than secondary CIDR block of the VPC.
- CLB instances within a VPC cannot be bound to a classic network-based CVM that interconnects with the same VPC.
- In Classiclink situations, the CVM traffic can only be routed to private IP addresses within the VPC rather than destinations outside the VPC.
>? The classic network-based CVM cannot access the public or private network resources outside the current VPC through network devices such as VPN gateway, direct connect gateway, public gateway, peering connection, and NAT Gateway.  Likewise, the peer of a VPN gateway, direct connect gateway, and peering connection cannot access classic network-based CVMs.



## Notes
- Changing the private IP of a classic network-based CVM will invalidate its association with the VPC, and cause the configurations to become invalid.  To associate them, you need to add a Classiclink again on the VPC console.
- The Classiclink will not be affected by actions taken regarding the CVM such as isolation due to overdue payment, security isolation, cold migration, failover, configuration modification, and operating system switching.
- The CVM will be automatically disassociated from the VPC if the CVM is returned.


## Reference
For more information on Classiclink, see [Managing Classiclink](https://intl.cloud.tencent.com/document/product/215/41419).

