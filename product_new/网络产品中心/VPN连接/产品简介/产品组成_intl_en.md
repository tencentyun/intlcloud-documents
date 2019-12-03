A VPN connection consists of a VPN gateway, a customer gateway, and a VPN tunnel.
## VPN Gateway

A VPN gateway is an egress gateway for establishing a VPN connection in a VPC. It is used with a customer gateway (IPsec VPN gateway on the IDC side) to establish an encrypted tunnel between a Tencent Cloud VPC and an external IDC for secure and reliable network communication. A Tencent Cloud VPN gateway is virtualized through software. With a dual-server hot backup mechanism, the system automatically switches to another server when one server becomes faulty, without affecting the normal operation of business.

Five bandwidth limits are available for a VPN gateway: 5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps, and 100 Mbps.
If you want to use [Anti-DDoS](https://cloud.tencent.com/document/product/297) to provide ultra-large-bandwidth DDoS and CC defense for the VPN gateway, you can bind Anti-DDoS Pro instance to the VPN gateway for security protection.

## Customer Gateway
A customer gateway is a logical object that records the public IP address of the IPsec VPN gateway on the IDC side. It is used with a Tencent Cloud VPN gateway. Encrypted VPN tunnels can be established between a VPN gateway and multiple customer gateways.

## VPN Tunnel
After the VPN gateway and customer gateway are created, a VPN tunnel can be established between the VPC and the external IDC for encrypted communication. The VPN tunnel currently supports the IPsec encryption protocol, which can meet the requirements of most VPN connections.
Since a VPN tunnel runs on an ISP's public network, congestion or jitter on the public network may affect the quality of the VPN network. Therefore, the SLA cannot be assured. If your business is sensitive to delay and jitter, it is recommended that you connect the VPC by using Direct Connect. For more information, see [Direct Connect](https://cloud.tencent.com/product/dc.html).

### Establishing a VPN Tunnel
A VPN tunnel on Tencent Cloud uses the Internet Key Exchange (IKE) protocol to establish a session during the implementation of IPsec. IKE has a self-protection mechanism that can securely authenticate identities, distribute keys, and establish IPSec sessions on insecure networks.
The following configuration information is required for establishing a VPN tunnel:
- Basic information
- Security policy database (SPD) policy
- (Optional) IKE configuration
- (Optional) IPsec configuration

The basic information, SPD policy, IKE configuration (optional), and IPsec configuration (optional) are described in detail below.
### SPD Policy
An SPD policy consists of a series of SPD rules that are used to specify the IP ranges in a VPC and an IDC that can communicate with each other. Each SPD rule contains one CIDR for the local IP range and at least one CIDR for the customer IP range. One CIDR for the local IP range and one CIDR for the customer IP range form a mapping. One SPD rule can contain multiple mappings.
> The rules for all tunnels of the same VPN gateway cannot contain overlapped mappings. In other words, at least one IP address in the local IP range and customer IP range in a mapping must be different.

**Example:**
As shown in the figure below, the following SPD rules have been configured for the VPN gateway:
 - SPD rule 1: The local IP range is 10.0.0.0/24, and the customer IP ranges are 192.168.0.0/24 and 192.168.1.0/24. Two mappings are available.
 - SPD rule 2: The local IP range is 10.0.1.0/24, and the customer IP range is 192.168.2.0/24. One mapping is available.
 - SPD rule 3: The local IP range is 10.0.2.0/24, and the customer IP range is 192.168.2.0/24. One mapping is available.
 
The mappings are as follows:
 - 10.0.0.0/24-----192.168.0.0/24
 - 10.0.0.0/24-----192.168.1.0/24
 - 10.0.1.0/24-----192.168.2.0/24
 - 10.0.2.0/24-----192.168.2.0/24

The four mappings cannot overlap. In other words, at least one IP address in the local IP range and the customer IP range must be different.
- If a new mapping 10.0.0.0/24-----192.168.1.0/24 is added, it cannot be added to the SPD rules because it overlaps with an existing mapping.
- If a new mapping 10.0.1.0/24-----192.168.1.0/24 is added, it can be added to the SPD rules because it does not overlap with the all the existing mappings.
![](//mccdn.qcloud.com/static/img/5b32174d312e31c5b5a9162a50456de8/image.png)

### IKE Configuration
<style> table th:first-of-type { width: 150px; } </style>

| Configuration item | Description |
| --------------- | ---------------------------------------- |
| Version | IKE V1 |
| Authentication method | Default pre-shared key |
| Authentication algorithm | MD5 and SHA1 supported |
| Negotiation mode | Main mode and aggressive mode supported<br/>In aggressive mode, more information can be sent with fewer packets so that a connection can be established more quickly. The downside of the aggressive mode is that the identity of a security gateway is sent in plain text. In aggressive mode, configuration parameters such as Diffie-Hellman and PFS cannot be negotiated and therefore compatible configurations must be available on both sides. |
| Local identity | IP address and fully qualified domain name (FQDN) supported |
| Customer identity | IP address and FQDN supported |
| DH group | Used during IKE. The security of key exchange increases with expansion of the DH group, but the exchange time also increases.<br/>Group 1: DH group that uses the 768-bit modular exponential (MODP) algorithm.<br/>Group 2: DH group that uses the 1,024-bit MODP algorithm.<br/>Group 5: DH group that uses the 1,536-bit MODP algorithm.<br/>Group 14: DH group that uses the 2,048-bit MODP algorithm. Dynamic VPN is not supported for this option.<br/>Group 24: DH group that uses the 2048-bit MODP algorithm with a 256-bit prime order subgroup. No group VPN is supported for this option. |
| IKE SA lifetime | Unit: second<br/>SA lifetime proposed for IKE security. Before a preset lifetime expires, another SA is determined through negotiation in advance to replace the old SA. The old SA is used until the new SA is determined through the negotiation. The new SA is used immediately after being established, and the old SA is cleared automatically after its lifetime expires. |

### IPsec Information
<style> table th:first-of-type { width: 150px; } </style>

| Configuration item | Description |
| --------------------- | ---------------------------------------- |
| Encryption algorithm | 3DES, AES-128, AES-192, AES-256, and DES supported |
| Authentication algorithm | MD5 and SHA1 supported |
| Packet encapsulation mode | Tunnel |
| Security protocol | ESP |
| PFS |disable, dh-group1, dh-group2, dh-group5, dh-group14, and dh-group24 supported |
| IPsec SA lifetime (s)  | Unit: second |
| IPsec SA lifetime (KB)  | Unit: KB |

