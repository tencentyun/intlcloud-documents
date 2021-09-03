A VPN tunnel is an encrypted public network tunnel used to transmit data packets in a VPN connection. The VPN tunnel on Tencent Cloud uses the IKE (Internet Key Exchange) protocol to establish a session when implementing IPsec. Featuring a self-protection mechanism, IKE can securely verify identities, distribute keys, and establish IPSec sessions on insecure networks. This document describes how to create a VPN tunnel on the [VPC console](https://console.cloud.tencent.com/vpc/vpnConn?rid=25).

The following configuration information is required to create a VPN tunnel:
+ [Basic information](#buzhou4)
+ [SPD (Security Policy Database) policy](#buzhou6)
+ [IKE configuration (Optional)](#buzhou7)
+ [IPsec configuration (Optional)](#buzhou8)

## Prerequisites
+ The VPN gateway and customer gateway have been configured.
+ The VPN gateway IP range and customer IP range cannot overlap.
+ The customer IDC must be configure with a static public IP.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** on the left sidebar to go to the management page.
3. Click **Create** on the **VPN Tunnel** management page.
4. Configure the basic information of the VPN tunnel in the pop-up dialog box.[](id:buzhou4)

<table>
<tr>
<th>Parameter Name</th>
<th>Notes</th>
</tr>
<tr>
<td>Tunnel Name</td>
<td>A custom tunnel name with up to 60 characters</td>
</tr>
<tr>
<td>Region</td>
<td>It is the same as the region of VPN gateway.</td>
</tr>
<tr>
<td>VPN Gateway Type</td>
<td>VPC or CCN</td>
</tr>
<tr>
<td>VPC</td>
<td>Select the VPC of the VPN gateway only when the <b>VPN Gateway Type</b> is <b>VPC</b>. This parameter is not available for CCN-based VPN gateways.</td>
</tr>
<tr>
<td>VPN Gateway</td>
<td>Select a VPN gateway from the list.</td>
</tr>
<tr>
<td>Customer Gateway</td>
<td>Select an existing customer gateway. Or you can create a new one.</td>
</tr>
<tr>
<td>Customer Gateway IP</td>
<td>The public IP address of the customer gateway.</td>
</tr>
<tr>
<td>Pre-shared Key</td>
<td>Used for identity authentication between the VPN gateway and customer gateway. The two peers must use the same pre-shared key.</td>
</tr>
<tr>
<td>Enable Health Check</td>
<td>Used to enable/disable health check and check the health status of the linkage. <b>Disabled</b> by default.</td>
</tr>
<tr>
<td>VPN Gateway IP Address for Health Check</td>
<td>It’s only required when the health check is enabled. It should be an available IP outside the VPC IP range.</td>
</tr>
<tr>
<td>Customer Gateway IP Address for Health Check</td>
<td>It’s only required when the health check is enabled. It should be an available IP within the IDC IP range. Note that the following IP addresses are not allowed: 169.254.0.0/16, 224.0.0.0-239.255.255.255, and 0.0.0.0.</td>
</tr>
<tr>
<td>Tag</td>
<td>(Optional) Attach a tag to the network resource as you need for easy management.</td>
</tr>
</table>

5. Click **Next** to go to the **SPD Policy** configuration page.

6. Configure the SPD policy.[](id:buzhou6)
  >?
  >+ An SPD policy consists of a series of SPD rules to specify the IP ranges in a VPC or CCN and an IDC that can communicate with each other. Each SPD rule contains one VPN gateway CIDR block and at least one customer gateway CIDR block. A CIDR block and a customer gateway CIDR block form a mapping. An SPD rule may involve multiple mappings.
  >+ The rules for all tunnels of the same VPN gateway cannot contain overlapped mappings. In other words, the VPN gateway IP range and customer gateway IP range in a mapping cannot have a duplicate address range.
  >
**Example:**
As shown in the figure below, a VPN gateway has the following SPD rules:
![](https://main.qcloudimg.com/raw/64171d0e6d862108d5e84ea3b9e3114f.png)
 - SPD rule 1: the VPN gateway IP range is 10.0.0.0/24, and the customer gateway IP ranges are 192.168.0.0/24 and 192.168.1.0/24. Two mappings are formed.
 - SPD rule 2: the VPN gateway IP range is 10.0.1.0/24, and the customer gateway IP range is 192.168.2.0/24. One mapping is formed.
 - SPD rule 3: the VPN gateway IP range is 10.0.1.0/24, and the customer gateway IP range is 192.168.2.0/24. One mapping is formed.
 There are four mappings as follows:
 - 10.0.0.0/24-----192.168.0.0/24
 - 10.0.0.0/24-----192.168.1.0/24
 - 10.0.1.0/24-----192.168.2.0/24
 - 10.0.2.0/24-----192.168.2.0/24
Note that the mapping rules cannot overlap with each other, which means that the VPN and customer gateway IP range of a rule cannot be both overlapped with the two corresponding IP ranges of another rule. 
 - Suppose that you want to add a new mapping between 10.0.0.0/24-----192.168.1.0/24. The operation fails as the combination of VPN gateway IP and customer gateway IP already exists.
 - You can add a new mapping between 10.0.1.0/24 and 192.168.1.0/24 as it does not overlap with any of the existing mappings.

7.[](id:buzhou7)Click **Next** to go to the **IKE Configuration (Optional)** page. If no advanced configuration is required, click **Next** directly.

<table>
<tr>
<th width="20%">Configuration Item</th>
<th>Notes</th>
</tr>
<tr>
<td>Version</td>
<td>IKE V1, IKE V2</td>
</tr>
<tr>
<td>Identity Verification Method</td>
<td>Default pre-shared key</td>
</tr>
<tr>
<td>Encryption Algorithm</td>
<td>The encryption algorithm supports AES-128, AES-192, AES-256, 3DES, and DES</td>
</tr>
<tr>
<td>Verification Algorithm</td>
<td>The identity verification algorithm. MD5 and SHA1 supported.</td>
</tr>
<tr>
<td>Negotiation Mode</td>
<td><b>Main</b> mode and <b>Aggressive</b> mode supported<br/>In <b>aggressive</b> mode, more information can be sent with fewer packets so that a connection can be established quickly, but the identity of a security gateway is sent in plain text. The configuration parameters such as Diffie-Hellman and PFS cannot be negotiated and they must have compatible configurations.
</tr>
<tr>
<td>VPN Gateway Identifier</td>
<td>IP Address and FQDN (full domain name) supported. IP Address by default</td>
</tr>
<tr>
<td>Customer Gateway Identifier</td>
<td>IP Address and FQDN supported. IP Address by default</td>
</tr>
<tr>
<td>DH group</td>
<td>Specifies the DH group used during IKE. The security of key exchange increases as the DH group expands, but the exchange may take a longer period.<br/>DH1: DH group that uses the 768-bit modular exponential (MODP) algorithm<br/> DH 2: DH group that uses the 1,024-bit MODP algorithm<br/> DH5: DH group that uses the 1,536-bit MODP algorithm<br/>DH14: DH group that uses the 2,048-bit MODP algorithm. Dynamic VPN is not supported for this option<br/>DH 24: DH group that uses the 2,048-bit MODP algorithm with a 256-bit prime order subgroup. </td>
</tr>
<tr>
<td>IKE SA Lifetime</td>
<td>Unit: second<br/>SA lifetime proposed for IKE security. Before a preset lifetime expires, another SA is negotiated in advance to replace the old one. The old SA is used before a new one is negotiated. The new SA is used immediately after establishment, and the old one is automatically cleared after its lifetime expires.</td>
</tr>
</table>

8.[](id:buzhou8)Go to the **IPsec configuration (Optional)** page. Directly click **Finish** if no advanced configuration is required.

<table>
<tr>
<th width="22%">Configuration Item</th>
<th>Notes</th>
</tr>
<tr>
<td>Encryption Algorithm</td>
<td>3DES, AES-128, AES-192, and AES-256 supported</td>
</tr>
<tr>
<td>Verification Algorithm</td>
<td>MD5 and SHA1 supported</td>
</tr>
<tr>
<td>Packet Encapsulation Mode</td>
<td>Tunnel</td>
</tr>
<tr>
<td>Security Protocol</td>
<td>ESP</td>
</tr>
<tr>
<td>PFS</td>
<td>disable, DH-GROUP1, DH-GROUP2, DH-GROUP5, DH-GROUP14, and DH-GROUP24 supported</td>
</tr>
<tr>
<td>IPsec SA lifetime(s)</td>
<td>Unit: s</td>
</tr>
<tr>
<td>IPsec SA lifetime(KB</td>
<td>Unit: KB</td>
</tr>
</table>

9. After the VPN tunnel is successfully created, return to the VPN tunnel list page and click **More**. Choose **Download config file** to complete the download.
10. Other operations:
     1. Clicking **Reset** will clear existing tunnel configurations. This operation will interrupt data transmission over the existing VPN tunnel and reestablish the connection. Please get ready for network change in advance.
     2. Click **More** > **Log** to view the tunnel log.
     3. Click **More** > **Delete** to delete the tunnel. Unconnected tunnels can be deleted.
     4. Click **More** > **Download config file** to download the tunnel configuration file. This file can be uploaded to the customer VPN device.
     5. Click **More** > **Edit Tag** to modify tags.

