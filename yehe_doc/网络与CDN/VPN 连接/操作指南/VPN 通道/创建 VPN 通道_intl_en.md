A VPN tunnel is an encrypted public network tunnel used to transmit data packets in a VPN connection. The VPN tunnel on Tencent Cloud uses the IKE (Internet Key Exchange) protocol to establish a session when implementing IPsec. Featuring a self-protection mechanism, IKE can securely verify identities, distribute keys, and establish IPSec sessions on insecure networks. This document describes how to create a VPN tunnel on the [ VPC Console ](https://console.cloud.tencent.com/vpc/vpnConn?rid=25).

The following configuration information is required to create a VPN tunnel:
+ [Basic information](#buzhou4)
+ [Communication mode](#buzhou6)
+ [IKE configuration (optional)](#buzhou7)
+ [IPsec configuration (optional)](#buzhou8)

## Prerequisites
+ The VPN gateway and customer gateway have been configured.
+ The local and customer IP ranges of the VPN tunnel in the SPD policy cannot overlap.
+ The customer IDC must configure a static public IP.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** in the left sidebar.
3. In the **VPN Connections** page, click **Create**.
4. Configure the basic information of the VPN tunnel in the pop-up dialog box.[](id:buzhou4)
![]()

<table>
<tr>
<th>Parameter</th>
<th>Remarks</th>
</tr>
<tr>
<td>Tunnel name</td>
<td>Custom tunnel name with 60 characters at most.</td>
</tr>
<tr>
<td>Region</td>
<td>Be the same as the region where the VPN gateway is</td>
</tr>
<tr>
<td>VPN gateway type</td>
<td>Includes VPN for VPC and VPN for CCN</td>
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
<td>Health check is disabled by default and used to check the health status of the linkage.
<dx-alert infotype="explain" title="">
After configuring the health check parameters, you need to configure the SPD policy as instructed in [Step 6](#buzhou6) to make the health check effective. For more information, see [Configuring Health Checks](https://intl.cloud.tencent.com/document/product/1037/46006).
</dx-alert>
</td>
</tr>
<tr>
<td>VPN gateway IP for health check</td>
<td>Configure this parameter and enter an available IP address outside of the VPC only when the health check is enabled.</td>
</tr>
<tr>
<td>Customer gateway IP for health check</td>
<td>Configure this parameter and enter an available IP address inside of the IDC only when the health check is enabled. IP addresses 169.254.0.0/16, 224.0.0.0-239.255.255.255, and 0.0.0.0 are not allowed.</td>
</tr>
<tr>
<td>Tag</td>
<td>Used to mark network resources to manage resources conveniently. Configure this optional parameter according to your need.</td>
</tr>
</table>

5. Click **Next** to enter the **Communication mode** configuration interface.[](id:buzhou6)[](id:cfg_vpn_spd)
 - Destination route
The routing policy specifies which IP ranges in the IDC the network to which the VPN gateway belongs can communicate with. After creating a tunnel, you need to configure the routing policy in the route table of the VPN gateway. For more information, see [Configuring Tencent Cloud Routing Policies](https://intl.cloud.tencent.com/document/product/1037/39690).
 - SPD policy
>?
>+ An SPD policy consists of a series of SPD rules to specify the IP ranges in a VPC or CCN and an IDC that can communicate with each other. Each SPD rule contains one CIDR block for the local IP range and at least one for the customer IP range. A CIDR block for the local IP range and a CIDR block for the customer IP range form a mapping. An SPD rule may involve multiple mappings.
>+ The rules for all tunnels of the same VPN gateway cannot contain overlapped mappings. In other words, the local IP range and customer IP range in a mapping cannot have a duplicate address range.
>
**Example:**
As shown in the figure below, a VPN gateway has the following SPD rules:
![](https://qcloudimg.tencent-cloud.cn/raw/aecbf567f760333e4af98ee1b0439d70.jpg)
 - SPD rule 1: the local IP range is 10.0.0.0/24, and the customer IP ranges are 192.168.0.0/24 and 192.168.1.0/24. Two mappings are available.
 - SPD rule 2: the local IP range is 10.0.1.0/24, and the customer IP range is 192.168.2.0/24. One mapping is available.
 - SPD rule 3: the local IP range is 10.0.1.0/24, and the customer IP range is 192.168.2.0/24. One mapping is available.
 The mappings are as follows:
 - 10.0.0.0/24-----192.168.0.0/24
 - 10.0.0.0/24-----192.168.1.0/24
 - 10.0.1.0/24-----192.168.2.0/24
 - 10.0.2.0/24-----192.168.2.0/24
The four mappings cannot overlap. In other words, the local IP range and customer IP range in a mapping cannot have a duplicate address range.
 - A new mapping 10.0.0.0/24-----192.168.1.0/24 cannot be added to SPD rules because it overlaps with an existing mapping.
 - A new mapping 10.0.1.0/24-----192.168.1.0/24 can be added to SPD rules because it does not overlap with any of the existing mappings.
![]()
6. [](id:buzhou7)Click **Next** to enter the **IKE configuration (optional)** interface. Continue to click **Next** if no advanced configuration is required.
![]()
<table>
<tr>
<th width="20%">Configuration Item</th>
<th>Remarks</th>
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
<td>Supports AES-128, AES-192, AES-256, 3DES, DES, and SM4</td>
</tr>
<tr>
<td>Verification algorithm</td>
<td>Used to verify the identities, and supports MD5, SHA1, SHA256, ASE-383, SHA512, and SM3</td>
</tr>
<tr>
<td>Negotiation mode</td>
<td>Main mode and aggressive mode supported<br/>In aggressive mode, more information can be sent with fewer packets so that a connection can be established quickly, but the identity of a security gateway is sent in plain text. The configuration parameters such as Diffie-Hellman and PFS cannot be negotiated and they must have compatible configurations.
</tr>
<tr>
<td>Local ID</td>
<td>Supports IP Address (default) and FQDN (full domain name)</td>
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
<td>Unit: second<br/>SA lifetime proposed for IKE security. Before a preset lifetime expires, another SA is negotiated in advance to replace the old one. The old SA is used before a new one is negotiated. The new SA is used immediately after establishment, and the old one is automatically cleared after its lifetime expires.</td>
</tr>
</table>
7. [](id:buzhou8) Enter the **IPsec configuration (optional)** interface. Click **Complete** if no advanced configuration is required.
<table>
<tr>
<th width="22%">Configuration Item</th>
<th>Remarks</th>
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
