To create a VPC peering connection between different developers within the same region, complete the following steps:

(1) The initiator makes a request for creating an intra-region peering connection.
You can use the API [Create a Regional Peering Connection](https://intl.cloud.tencent.com/document/product/215/2107) to initiate a request for creating a regional peering connection. Afterwards, you need to notify the receiver's developer to accept the request.

2. The receiver accepts the request for peering connection.
If you are the receiver, you can use the API [Accept an Intra-Region Peering Connection](https://intl.cloud.tencent.com/document/product/215/2106) to accept the intra-region peering connection created by the initiator's developer.

3. The initiator modifies the route table.
After the receiver accepts the request for peering connection, you need to modify route table policies by calling the API [Modify the Route Table](https://intl.cloud.tencent.com/document/product/215/15766) and create a routing policy, which directs the next hop that accesses the receiver's VPC through the peering connection to this peering connection.

4. The initiator modifies the route table associated with the subnet.
After configuring the routing policy, you can use the API [Modify the Route Table Associated with a Subnet](https://intl.cloud.tencent.com/document/product/215/1416) to direct the subnet that accesses the receiver's VPC through the peering connection to this route table.

5. The receiver modifies the route table.
After accepting the request for peering connection, you need to modify route table policies by calling the API [Modify the Route Table](https://intl.cloud.tencent.com/document/product/215/15766) and create a routing policy, which directs the next hop that accesses initiator's VPC through the peering connection to this peering connection.

6. The receiver modifies the route table associated with the subnet.
After configuring the routing policy, you can use the API [Modify the Route Table Associated with a Subnet](https://intl.cloud.tencent.com/document/product/215/1416) to direct the subnet that accesses the initiator's VPC through the peering connection to this route table.

A cross-region interconnection is configured in the same way as a intra-region interconnection. For more information about the use cases of peering connection, see <a href="https://intl.cloud.tencent.com/doc/product/215/5000" title="Peering Connection">About Peering Connection</a>.
