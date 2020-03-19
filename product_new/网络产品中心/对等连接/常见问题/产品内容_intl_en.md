### Is the connectivity of a peering connection transitive?
A peering connection enables connectivity between two VPCs, but the connectivity cannot be transited.
For example, as shown in the following figure, peering connections are created between VPC 1 and VPC 2, and between VPC 1 and VPC 3. However, due to the non-transitivity of peering connections, traffic cannot flow between VPC 2 and VPC 3.
![](//mccdn.qcloud.com/static/img/9127397dcb1df231bfd8d32bcd628223/image.png)
>**Note:**
>Even if a peering connection is created, both ends of the connection cannot communicate with each other if routes for sending and returning packets are not configured at both ends.

### What is the difference between intra-region and cross-region peering connections?
- Intra-region peering connections are used to connect applications located in different VPCs within the same region.
- Cross-regional peering connections are used to implement connectivity between VPCs in different regions.

For more information, see [Features](https://cloud.tencent.com/document/product/553/18829#.E5.90.8C.E5.9C.B0.E5.9F.9F.E5.92.8C.E8.B7.A8.E5.9C.B0.E5.9F.9F.E5.AF.B9.E7.AD.89.E8.BF.9E.E6.8E.A5).

### Can I set bandwidth limits for peering connections?
- For a cross-region peering connection: you can set a bandwidth limit when you create the connection using an API. Setting bandwidth limits in the console will be supported in the near future.
- For an intra-region peering connection: you do not need to set a bandwidth limit for the connection because bandwidth is free of charge and is unlimited.

### If a peering connection is deleted at one end, is the VPC at the other end still accessible from the peer end?
No. The peering connection can be disconnected at either end at any time. The connection is ineffective immediately upon disconnection. The VPC at either end is accessible only after the connection is created again.


### Can I create a peering connection between VPCs of different accounts?
Yes. This is possible as long as the owner of the other VPC accepts your peering connection request.

### Can I create a peering connection between two VPCs with overlapped IP ranges?
No. The IP ranges of VPCs at the two ends of a peering connection cannot overlap.

### Is traffic encrypted over a peering connection?
No. After a peering connection is created, access between two VPCs is similar to that between two CVMs in the same VPC, without additional encryption. Network traffic within a VPC is always isolated from other networks.

### Is a single point of failure possible?
Single points of failure or bandwidth bottlenecks cannot occur because a peering connection between VPCs is not a gateway or a VPN connection and it does not depend on separate hardware.


