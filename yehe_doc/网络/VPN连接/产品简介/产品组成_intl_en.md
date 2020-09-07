A VPN connection consists of a VPN gateway, a customer gateway, and a VPN tunnel.
## VPN Gateways
A VPN gateway is an egress gateway for VPC or CCN to establish a VPN connection. It is used with a customer gateway (IPsec VPN gateway on the IDC side) to establish an encrypted communication between a Tencent Cloud VPC or CCN and an external IDC. Tencent Cloud VPN gateway uses software virtualization and an active-active hot backup architecture. When one server fails, automatic switchover helps ensure the normal operation of your businesses.

Eight bandwidth caps are available for a VPN gateway: 5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, and 1000 Mbps.
If you need [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029) to defend against DDoS and CC attacks with high-bandwidth protection, you can bind it to the VPN gateway.

## Customer Gateways
A customer gateway is a logical object used with a Tencent Cloud VPN gateway to record the fixed public IP address of the IPsec VPN gateway on the IDC side. Each VPN gateway can create encrypted VPN tunnels with multiple customer gateways.

## VPN Tunnel
After VPN gateway and customer gateway are created, you can establish a VPN tunnel between the VPC or CCN and an external IDC for encrypted communication. Currently, VPN tunnel supports the IPsec encryption protocol, meeting the requirements of most VPN connections.
Because a VPN tunnel runs on an ISP's public network, congestion or jitter on the public network may affect the VPN network. If your business is sensitive to delay and jitter, we recommend that you connect the VPC or CCN via Direct Connect. For more information, see [Direct Connect](https://intl.cloud.tencent.com/product/dc).

### Establishing a VPN tunnel
A VPN tunnel on Tencent Cloud uses the Internet Key Exchange (IKE) protocol to establish a session when implementing IPsec. IKE has a self-protection mechanism that can securely authenticate identities, distribute keys, and establish IPSec sessions on insecure networks.
The following configuration information is required to establish a VPN tunnel:

- Basic information
- Security policy database (SPD) policy
- (Optional) IKE configuration
- (Optional) IPsec configuration

Basic information, SPD policy, IKE configuration (optional), and IPsec configuration (optional) are described in detail below.
### SPD Policy
An SPD policy consists of a series of SPD rules used to specify the IP ranges in a VPC or CCN and an IDC that can communicate with each other. Each SPD rule contains one CIDR for the local IP range and at least one CIDR for the customer IP range. The two of them form a mapping. One SPD rule can contain multiple mappings.
> The rules for all tunnels of the same VPN gateway cannot contain overlapped mappings. In other words, the local IP range and customer IP range in a mapping cannot have a duplicate address range.

**Example:**
As shown in the figure below, a VPN gateway has the following SPD rules:
![](https://main.qcloudimg.com/raw/802efcd114423a1d07cbc058c5b062ca.png)

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

### IKE Configuration
<style> table th:first-of-type { width: 150px; } </style>

| Configuration item | Description |
| --------------- | ---------------------------------------- |
| Version | IKE V1 |
| Identity verification method | Default pre-shared key |
| Verification algorithm | MD5 and SHA1 supported |
| Negotiation mode | Main mode and aggressive mode supported<br/>In aggressive mode, more information can be sent with fewer packets so that a connection can be established quickly, but the identity of a security gateway is sent in plain text. The configuration parameters such as Diffie-Hellman and PFS cannot be negotiated and they must have compatible configurations. |
| Local identity | IP address and fully qualified domain name (FQDN) supported |
| Customer identity | IP address and FQDN supported |
| DH group | Used during IKE. The security of key exchange increases as the DH group expands, but the exchange time also becomes longer.<br/>Group 1: DH group that uses the 768-bit modular exponential (MODP) algorithm.<br/>Group 2: DH group that uses the 1,024-bit MODP algorithm.<br/>Group 5: DH group that uses the 1,536-bit MODP algorithm.<br/>Group 14: DH group that uses the 2,048-bit MODP algorithm. Dynamic VPN is not supported for this option.<br/>Group 24: DH group that uses the 2048-bit MODP algorithm with a 256-bit prime order subgroup. No group VPN is supported for this option. |
| IKE SA lifetime | Unit: second<br/>SA lifetime proposed for IKE security. Before a preset lifetime expires, another SA is negotiated in advance to replace the old one. The old SA is used until the new one is negotiated. The new SA is used immediately after establishment, and the old one is automatically cleared after its lifetime expires. |

### IPsec Information
<style> table th:first-of-type { width: 150px; } </style>

| Configuration Item | Description |
| --------------------- | ---------------------------------------- |
| Encryption algorithm | 3DES, AES-128, AES-192, AES-256, and DES supported |
| Verification algorithm | MD5 and SHA1 supported |
| Packet encapsulation mode | Tunnel |
| Security protocol | ESP |
| PFS | disable, dh-group1, dh-group2, dh-group5, dh-group14, and dh-group24 supported |
| IPsec SA lifetime (s)  | Unit: second |
| IPsec SA lifetime (KB)  | Unit: KB |

