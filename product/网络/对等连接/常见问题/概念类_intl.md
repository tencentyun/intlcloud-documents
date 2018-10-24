### What is peering connection?
VPC peering connection is a cross-VPC network interconnection service for office data synchronization. For more information, see [Product Overview](https://cloud.tencent.com/document/product/553/18827#.E7.AE.80.E4.BB.8B).

### Is the connectivity of a peering connection transitive?
Peering connection allows connectivity between VPCs, which is not transitive.
As shown in the following figure, peering connection is established between VPC 1 and VPC 2, as is done between VPC 1 and VPC 3. However, due to the non-transitive nature of peering connection, VPC 2 and VPC 3 cannot readily interconnect.
![](//mccdn.qcloud.com/static/img/9127397dcb1df231bfd8d32bcd628223/image.png)
>**Note:**
> Even if a peering connection is established, communication cannot be achieved if routes for sending and returning packets are not configured on both ends.

### What's the difference between intra-region and cross-region peering connections?
- Intra-region peering connection is used primarily to connect applications located in different VPCs within the same region.
- Cross-regional peering connection is mainly used to implement connectivity between VPCs in different regions.

For more information, see [Product Features](https://cloud.tencent.com/document/product/553/18829#.E5.90.8C.E5.9C.B0.E5.9F.9F.E5.92.8C.E8.B7.A8.E5.9C.B0.E5.9F.9F.E5.AF.B9.E7.AD.89.E8.BF.9E.E6.8E.A5).



### What are the constraints on using peering connections?
When using a peering connection, pay attention to the limitations on the connection and the resources. For more information, see [Use Limits](https://cloud.tencent.com/document/product/553/18829#.E5.90.8C.E5.9C.B0.E5.9F.9F.E5.92.8C.E8.B7.A8.E5.9C.B0.E5.9F.9F.E5.AF.B9.E7.AD.89.E8.BF.9E.E6.8E.A5).

### Can I set bandwidth limits to peering connections?
- Cross-region peering connection: A bandwidth limit can be set when the connection is created using an API. Setting bandwidth limits in the console will be supported in the near future.
- Intra-region peering connection: There is no bandwidth fee and no bandwidth limit on it.

### If a peering connection is deleted on one end, can the VPC on this end still be accessible from the other end?
No. The peering connection can be interrupted on either end at any time. The connection is invalid immediately upon the interruption. The VPC on either end can only be accessible after the connection is established again.

### If there is already a peering connection established between VPC A and VPC B and between VPC B and VPC C, does this mean a peering connection is also established between VPC A and VPC C?
No. Peering connections are not transitive.


### Can I establish a peering connection between VPCs of different accounts?
Yes. This is possible as long as the owner of the other VPC accepts your peering connection request.

### Can I establish a peering connection between two VPCs with overlapped IP address ranges?
No. The IP address ranges of VPCs on both end of a peering connection cannot overlap.

### Is traffic encrypted over peering connection?
No. After a peering connection is established, communication over it is not encrypted between two different VPCs or two CVMs within the same VPC. Traffics within one VPC is always isolated from the other VPC.

### Is a single point of failure possible?
There is no single point of failure and bandwidth bottleneck as VPC peering connection is neither a gateway nor a VPN connection, and does not rely on a separate piece of physical hardware.



