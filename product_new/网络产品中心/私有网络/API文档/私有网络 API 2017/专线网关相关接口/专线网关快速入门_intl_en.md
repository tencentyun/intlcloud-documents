To create a direct connect gateway to quickly connect Tencent Cloud with a local IDC, complete the following steps:
1. Establish a connection.
You can establish a connection on the <a href="https://console.cloud.tencent.com/vpc/dc" title="Connection">Connection Management</a> page in the Tencent Cloud console.

2. Create a direct connect gateway.
You can create a direct connect gateway by using the API [Create Direct Connect Gateways](https://intl.cloud.tencent.com/document/product/215/4824). You can choose whether to enable NAT based on your needs. The NAT direct connect gateway supports the configuration of network address translation.

3. Set up a dedicated tunnel. You need to create a dedicated tunnel that connects to different direct connect gateways on the <a href="https://console.cloud.tencent.com/vpc/dcConn" title="Dedicated Tunnel">Dedicated Tunnel Management</a> page in the Tencent Cloud console so that the local IDC can interconnect with multiple VPCs.



4. Modify the routing table associated with subnets.
After configuring routing policies, you can use the API [Modify Routing Tables Associated with Subnets](https://intl.cloud.tencent.com/document/product/215/1416) to point the subnet that needs to access other VPCs through the direct connect gateway to the routing table.

For specific use cases of the direct connect gateway, see <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect Gateway Description</a>.
