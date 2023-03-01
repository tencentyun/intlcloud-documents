[](id:01)
### What do I do when an employee leaves the company or a project team, or when I need to temporarily revoke an employee’s permissions?
You can disable the corresponding certificate on the SSL VPN client page. For more information, see [Managing SSL VPN Client Certificate](https://intl.cloud.tencent.com/document/product/1037/43915).

[](id:02)
### Can I remotely connect to my VPC over a VPN connection?
Yes. Tencent Cloud provides SSL VPN that allows you to remotely access the resources and services in your VPC by using a computer or mobile phone. That is, you can connect to your VPC by using SSL VPN. For more information, see [Connecting the Mobile Client to VPC > Directions](https://intl.cloud.tencent.com/document/product/1037/43900).

[](id:03)
### Can I access the internet over an SSL VPN connection?
No. This is not supported.

[](id:04)
### Can multiple IDCs communicate with each other by using a VPN gateway?
Yes. You can use **VPN for Cloud Connect Network (CCN)** to allow multiple IDCs that do not require access to cloud resources to communicate with each other. In this case, each IDC uses its own IPsec VPN devices to access the VPN gateway for CCN, without being associated with a CCN instance, for traffic forwarding.

[](id:05)
### Can multiple IDCs communicate with a VPC by using a VPN gateway?
Yes. You can create a VPN gateway for CCN and associate the gateway with a CCN instance. In this case, each IDC uses its own IPsec VPN devices to access the VPN gateway for CCN to communicate with a VPC.

[](id:06)
### Can I implement redundant communication by using a DC connection as the primary connection and a VPN connection as the secondary connection?
Yes. You can create a VPC-based Direct Connect (DC) gateway and a VPC-based VPN gateway. Then, you can create a DC connection and a VPN connection. Based on the VPC route priority, the DC connection serves as the primary connection and the VPN connection serves as the secondary connection. This allows you to implement redundant communication. For more information, see Hybrid Cloud Primary/Secondary Communication (DC and VPN).


[](id:08)
### How do I implement primary/secondary disaster recovery?
You can use Tencent Cloud VPN Connections to implement primary/secondary disaster recovery. To be specific, you can create two IPsec VPN tunnels (route table) and configure the subnet routing, gateway routing, as well as routing weights. For more information, see [Connecting IDC to a Single Tencent Cloud VPC for Primary/Secondary Disaster Recovery](https://intl.cloud.tencent.com/document/product/1037/41975).

[](id:09)
### How do I use Tencent Cloud VPN Connections? How do I choose between IPsec VPN and SSL VPN?
Tencent Cloud VPN Connections supports both the IPsec and SSL network security protocols.
- You can use IPsec VPN for site-to-site connections. For more information, see [IPSec VPN](https://www.tencentcloud.com/document/product/1037/43324).
- You can use SSL VPN for client-to-site connections. For more information, see [Connecting the Mobile Client to VPC](https://www.tencentcloud.com/document/product/1037/43898).

[](id:10)
### Does Tencent Cloud VPN Connections support internet access acceleration?
No. Tencent Cloud VPN Connections does not support internet access acceleration. If you want to accelerate internet access, see [Anycast Internet Acceleration](https://www.tencentcloud.com/document/product/644).

[](id:11)
### Can I use Tencent Cloud VPN Connections to access a hotel system that runs on Tencent Cloud from hotels in six regions?
Yes. You can use SSL VPN in this scenario. If you have higher security requirements, you can configure access control. For more information, see [SSL VPN Access Control and Portal Login Guide](https://intl.cloud.tencent.com/document/product/1037/48819).

[](id:12)
### Can I use Tencent Cloud VPN Connections to visit Google?
No. Tencent Cloud VPN Connections provides services in compliance with national laws and regulations, and does not provide the internet access or proxy service. You are not allowed to technically circumvent internet censorship to visit banned websites.

[](id:13)
### Can I use Tencent Cloud VPN Connections to access Tencent Cloud without a public IP address?
Yes. You can use SSL VPN in this scenario.

[](id:14)
### Can I use Tencent Cloud VPN Connections for non-Tencent Cloud products?
Yes. Tencent Cloud VPN Connections is developed based on the standard IKE and IPsec protocols. Therefore, it is compatible with all VPN devices and services in compliance with the protocols.

[](id:15)
### Does Tencent Cloud VPN Connections support primary/secondary disaster recovery based on ECMP?
No. Tencent Cloud VPN Connections does not support Equal-Cost Multipath Routing (ECMP). However, you can use Tencent Cloud VPN Connections to implement primary/secondary disaster recovery in the following way: Create two IPsec VPN tunnels (route table) and configure the subnet routing, gateway routing, as well as routing weights. For more information, see [Connecting IDC to a Single Tencent Cloud VPC for Primary/Secondary Disaster Recovery](https://intl.cloud.tencent.com/document/product/1037/41975).

[](id:16)
### How can I configure a VPN connection?
You can fully configure an IPsec VPN connection on the console. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1037/32689).

[](id:17)
### How can I create a VPN gateway?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to create a VPN gateway as instructed in [Step 1: Create a VPN Gateway](https://intl.cloud.tencent.com/document/product/1037/32690).

[](id:18)
### Can two VPCs communicate with each other through a VPN connection?
Yes. You can separately purchase VPN gateways and configure VPN tunnels and customer gateways in the two VPCs, but the configuration is complex. We recommend that you use [Cloud Connect Network (CCN)](https://www.tencentcloud.com/products/ccn). CCN connects two VPCs by using the private network of Tencent to ensure the quality of communication.

[](id:19)
### Can I use Tencent Cloud VPN Connections for the proxy service?
Tencent Cloud VPN Connections provides services in compliance with national laws and regulations, and does not provide the internet access or proxy service.
