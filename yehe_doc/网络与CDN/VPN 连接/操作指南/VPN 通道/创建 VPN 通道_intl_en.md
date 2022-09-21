A VPN tunnel is an encrypted public network tunnel used to transfer data packets in a VPN connection. The VPN tunnel in Tencent Cloud uses the IKE (Internet Key Exchange) protocol to establish a session when implementing IPsec. Featuring a self-protection mechanism, IKE can securely verify identities, distribute keys, and establish IPsec sessions over insecure networks. This document describes how to create a VPN tunnel in the console. You can also manage your VPN tunnels through APIs and SDKs. For more information, see [API Documentation](https://intl.cloud.tencent.com/document/product/1037/34252).

The following configuration information is required to create a VPN tunnel:
+ [Basic information](#buzhou4)
+ [Communication mode](#buzhou6)
+ [IKE configuration (optional)](#buzhou7)
+ [IPsec configuration (optional)](#buzhou8)

## Prerequisites
+ You have [created a VPN gateway](https://intl.cloud.tencent.com/document/product/1037/39684) and [customer gateway](https://intl.cloud.tencent.com/document/product/1037/39691).
+ Make sure that the number of created VPN tunnels doesn't exceed the quota. You can adjust the quota as instructed in [Use Limits](https://intl.cloud.tencent.com/document/product/1037/32682).


## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **VPN tunnel** to enter the management page.
3. In the **VPN Connections** page, click **Create**.
4. Configure the basic information of the VPN tunnel in the pop-up dialog box.[](id:buzhou4)
![]()
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>Tunnel name</td>
<td>Custom tunnel name with 60 characters at most.</td>
</tr>
<tr>
<td>Region</td>
<td>The region of the VPN gateway that is associated with the VPN tunnel to be created.</td>
</tr>
<tr>
<td>VPN gateway type</td>
<td>You can select VPC VPN or CCN VPN for the VPN gateway type. For more information on the two VPN gateway types, see <a href="https://intl.cloud.tencent.com/document/product/1037/32679">Overview</a>.</td>
</tr>
<tr>
<td>VPC</td>
<td>Select the VPC of the VPN gateway only when the <b>VPN gateway type</b> is <b>VPC</b>. The VPN for CCN doesn't have such a parameter.</td>
</tr>
<tr>
<td>VPN gateway</td>
<td>Select a VPN gateway from the list.</td>
</tr>
<tr>
<td>Customer gateway</td>
<td>Select a customer gateway that has been created. Otherwise, create one.</td>
</tr>
<tr>
<td>Customer gateway IP</td>
<td>The public IP address of the customer gateway</td>
</tr>
<tr>
<td>Enable DPD</td>
<td>DPD is enabled by default and used to check whether the peer is alive or not</br>. If the response of the DPD request message actively sent by the local end is not received within the specified timeout period, it is considered that the peer is offline and timeout action is performed.</td>
</tr>
<tr>
<td>DPD timeout period</td>
<td>The overall DPD timeout period. Valid range: 30-60s. The default value is 30s.</td>
</tr>
<tr>
<td>DPD timeout action</td>
<td><ul><li>Disconnect: The current SA is cleared and the current VPN tunnel is disconnected</li><li>Retry: Reconnect to the peer</li></ul></td>
</tr>
<tr>
<td>Pre-shared key</td>
<td>Used to verify the identities of local and customer gateways that must use the same pre-shared key.</td>
</tr>
<tr>
<td>Negotiation type</td>
<td><ul><li>Traffic-triggered: After the VPN tunnel is created, the negotiation will start when the traffic flows to the local end.</li><li>Active: After the tunnel is created, the local end actively initiates negotiation with the peer end.</li><li>Passive: The negotiation is launched by the peer end.</li></ul></td>
</tr>
<tr>
<td>Enable health check</td>
<td>Health check is used for primary/secondary tunnels. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1037/41975">Connecting IDC to a Single Tencent Cloud VPC for Primary/Secondary Disaster Recovery</a>. If your business doesn't involve primary/secondary tunnels, you don't need to enable this feature (disabled by default); otherwise, complete the health check configuration on the local and peer addresses as instructed in <a href="https://intl.cloud.tencent.com/document/product/1037/46006">Configuring Health Checks</a>.
<dx-alert infotype="explain" title="">
Once you enable health check and create a VPN tunnel, the system immediately performs network quality analysis (NQA) to check the health of the tunnel. If the tunnel is not linked or your configured peer address doesn't respond to NQA detection, the system will consider the tunnel as unhealthy after multiple detection failures and interrupt the business traffic until the tunnel recovers.
</dx-alert>
</td>
</tr>
<tr>
<td>VPN gateway IP for health check</td>
<td>This parameter is required only when health check is enabled. You can use the IP address assigned by the system or specify one.
<dx-alert infotype="explain" title="">
The specified address cannot conflict with the private network address or IP range of the VPC, CCN, or IDC or the peer address in health check, and it cannot be a multicast, broadcast, or local loopback address.
</dx-alert>
</td>
</tr>
<tr>
<td>Customer gateway IP for health check</td>
<td>This parameter is required only when health check is enabled. You can use the IP address assigned by the system or specify one.
<dx-alert infotype="explain" title="">
The specified address cannot conflict with the private network address or IP range of the VPC, CCN, or IDC or the local address in health check, and it cannot be a multicast, broadcast, or local loopback address.
</dx-alert>
</td>
</tr>
<tr>
<td>Tag</td>
<td>Used to mark network resources to manage resources conveniently. Configure this optional parameter according to your need.</td>
</tr>
</table>
5. Click **Next** to enter the **Communication mode** configuration interface.[](id:buzhou6)[](id:cfg_vpn_spd)
 - Destination route
The routing policy specifies which IP ranges in the IDC the network to which the VPN gateway belongs can communicate with. After creating a tunnel, you need to configure the routing policy in the route table of the VPN gateway. For more information, see [Configuring Tencent Cloud Routing Policies](https://intl.cloud.tencent.com/document/product/1037/39690).
![]()
 - SPD policy
>?
>+ An SPD policy consists of a series of SPD rules to specify the IP ranges in a VPC or CCN and an IDC that can communicate with each other. Each SPD rule contains one CIDR block for the local IP range and at least one for the peer IP range. A CIDR block for the local IP range and a CIDR block for the peer IP range form a mapping. An SPD rule may involve multiple **mappings**.
>+ VPN Gateway will negotiate with the customer gateway according to the **mappings** in sequence. Make sure that your customer gateway device supports mapping-based negotiation; for example, it is supported if the `also` keyword is used in `StrongSwan` configuration.
>+ All SPD rules under the same VPN gateway can form up to **200** mappings. If you need more, we recommend you use **Route-Based VPN Connections**.
>+ The rules for all tunnels of the same VPN gateway cannot contain overlapped mappings. In other words, the local IP range and customer IP range in a mapping cannot have a duplicate address range.
>+ **We recommend you configure a matching rule in the SPD policies in Tencent Cloud and customer gateway**. For example, if the local IP range `10.11.12.0/24` and peer IP range `192.168.1.0/24` are configured in the SPD policy in Tencent Cloud, set the local and peer IP ranges also to `192.168.1.0/24` and `10.11.12.0/24` respectively in the SPD policy in your customer gateway.
>- After an SPD policy is configured, the VPN gateway will automatically distribute the routes, eliminating your need to add routes in the VPN gateway.
>
**Example:**
As shown in the figure below, a VPN gateway has the following SPD rules:
![](https://main.qcloudimg.com/raw/64171d0e6d862108d5e84ea3b9e3114f.png)
 - SPD rule 1: The local IP range is `10.0.0.0/24`, and the peer IP ranges are `192.168.0.0/24` and `192.168.1.0/24`. Two mappings are available.
 - SPD rule 2: The local IP range is `10.0.1.0/24`, and the peer IP range is `192.168.2.0/24`. One mapping is available.
 - SPD rule 3: The local IP range is `10.0.2.0/24`, and the peer IP range is `192.168.2.0/24`. One mapping is available.
 The mappings are as follows:
 - `10.0.0.0/24`-----`192.168.0.0/24`
 - `10.0.0.0/24`-----`192.168.1.0/24`
 - `10.0.1.0/24`-----`192.168.2.0/24`
 - `10.0.2.0/24`-----`192.168.2.0/24`
The four mappings cannot overlap. In other words, the local IP range and customer IP range in a mapping cannot have a duplicate address range.
 - A new mapping `10.0.0.0/24-----192.168.1.0/24` cannot be added to SPD rules because it overlaps with an existing mapping.
 - A new mapping `10.0.1.0/24`-----`192.168.1.0/24` can be added to SPD rules because it does not overlap with any of the existing mappings.
![]()
6. [](id:buzhou7)Click **Next** to enter the **IKE Configuration (Optional)** page. Directly click **Next** if no advanced configuration is required.
![]()
<table>
<tr>
<th width="20%">Configuration Item</th>
<th>Description</th>
</tr>
<tr>
<td>Version</td>
<td>IKE V1, IKE V2</td>
</tr>
<tr>
<td>Identity verification method</td>
<td>Default pre-shared key</td>
</tr>
<tr>
<td>Encryption algorithm</td>
<td>Supported encryption algorithms include AES-128, AES-192, AES-256, 3DES, DES, and SM4. We recommend you use AES-128.</td>
</tr>
<tr>
<td>Verification algorithm</td>
<td>Identity verification algorithm. Supported algorithms include MD5, SHA-1, SHA-256, AES-383, SHA-512, and SM3. We recommend you use MD5.</td>
</tr>
<tr>
<td>Negotiation mode</td>
<td>Main mode and aggressive mode supported<br/>In aggressive mode, more information can be sent with fewer packets so that a connection can be established quickly, but the identity of a security gateway is sent in plain text. The configuration parameters such as Diffie-Hellman and PFS cannot be negotiated and they must have compatible configurations.</td>
</tr>
<tr>
<td>Local ID</td>
<td>Supports IP Address (default) and FQDN (fully qualified domain name)</td>
</tr>
<tr>
<td>Customer ID</td>
<td>Supports IP Address (default) and FQDN</td>
</tr>
<tr>
<td>DH group</td>
<td>Used when IKE is specified. The security of key exchange increases as the DH group expands, but the exchange time also becomes longer<br/>DH1: DH group that uses the 768-bit modular exponential (MODP) algorithm<br/> DH 2: DH group that uses the 1,024-bit MODP algorithm<br/> DH5: DH group that uses the 1,536-bit MODP algorithm<br/>DH14: DH group that uses the 2,048-bit MODP algorithm. Dynamic VPN is not supported for this option<br/>DH 24: DH group that uses the 2,048-bit MODP algorithm with a 256-bit prime order subgroup.</td>
</tr>
<tr>
<td>IKE SA lifetime</td>
<td>Unit: s<br/>SA lifetime proposed for IKE security. Before a preset lifetime expires, another SA is negotiated in advance to replace the old one. The old SA is used before a new one is negotiated. The new SA is used immediately after establishment, and the old one is automatically cleared after its lifetime expires.</td>
</tr>
</table>
7. [](id:buzhou8) Enter the **IPsec configuration (optional)** interface. Click **Complete** if no advanced configuration is required.
<table>
<tr>
<th width="22%">Configuration Item</th>
<th>Description</th>
</tr>
<tr>
<td>Encryption algorithm</td>
<td>Supports AES-128, AES-192, AES-256, 3DES, DES, and SM4</td>
</tr>
<tr>
<td>Verification algorithm</td>
<td>Used to verify identities, and supports MD5, SHA1, SHA256, SHA384, SHA512, and SM3</td>
</tr>
<tr>
<td>Packet encapsulation mode</td>
<td>Tunnel</td>
</tr>
<tr>
<td>Security protocol</td>
<td>ESP</td>
</tr>
<tr>
<td>PFS</td>
<td>Supports disable, DH-GROUP1, DH-GROUP2, DH-GROUP5, DH-GROUP14, and DH-GROUP24</td>
</tr>
<tr>
<td>IPsec SA lifetime(s)</td>
<td>Unit: s</td>
</tr>
<tr>
<td>IPsec SA lifetime (KB)</td>
<td>Unit: KB</td>
</tr>
</table>
​	 
