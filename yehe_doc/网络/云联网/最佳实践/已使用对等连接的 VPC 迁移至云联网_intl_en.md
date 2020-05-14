This article describes how to migrate a VPC with peering connections to Cloud Connect Network (CCN).
1. Create a CCN instance.
2. Associate the VPC with peering connections with the CCN instance.
3. Check the route table of the CCN instance.
4. Disable the peering connections in the VPC subnet route table and enable CCN routing.

## Example
VPC1 and VPC2 are peer connected and you want to migrate them to CCN so all VPCs can communicate with one another on the public and private network.
- VPC1 (Guangzhou): 192.168.0.0/16, Subnet A: 192.168.0.0/24, Subnet B: 192.168.1.0/24.

- VPC2 (Shanghai): 10.0.0.0/16, Subnet C: 10.0.0.0/24, Subnet D: 10.0.1.0/24.
  
  ![](https://main.qcloudimg.com/raw/4419a9270e5b57cc4d305e8c2164c21a.jpg)
  
  Follow these steps:

1. Create a CCN instance, or use an existing one. For more information, see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062)。
2. Associate VPC1 and VPC2 with the CCN instance. For more information, see [Associating a Network Instance](https://intl.cloud.tencent.com/document/product/1003/30064).
3. In the CCN instance route table, you should see routing policies with VPC1 and VPC2 subnets as targets. There are four routing policies in this example, pointing to subnets A, B, C, and D.
4. Check the subnet route tables of VPC1 and VPC 2 to make sure routing policies are enabled. CCN routing policies are distributed to subnets, but they may not take effect. Enable or disable necessary routing policies to complete the migration.

## Possible Results
- Result 1: routing policies from CCN do not conflict with existing peering connections. Disable existing peering connections and let CCN routing policies take over.
- Result 2: routing policies from CCN overlap or conflict with existing peering connections. CCN routing policies are ignored by default and cannot be enabled. You need to **disable** routing policies with peering connection as the next hop and **enable** policies with CCN routing policies as the next hop.
> **Note**:
> Disabling peering connection routing policies may cause service interruption, the length of which depends on when you enable CCN routing policies. 


- Result 3: routing policies from CCN conflict with existing peering connections. CCN routing policies are ignored by default but you can still **enable** these policies. After you enable them, traffic is forwarded using the longest prefix match algorithm. If the existing peering connections are no longer in use after the migration, we recommend that you **disable** routing policies with peering connection as the next hop.


