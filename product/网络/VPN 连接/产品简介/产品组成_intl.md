A VPN connection is composed of a VPN gateway, a Customer gateway and a VPN tunnel.
## VPN Gateway

VPN gateway is an egress gateway used to establish VPN connections from your VPC. It is used with customer gateway (IPsec VPN gateway on IDC side) to establish an encrypted tunnel between a Tencent Cloud VPC and an external IDC for secure and reliable network communication. Tencent Cloud VPN gateway is implemented based on software virtualization. With a dual-server hot backup mechanism, it switches to another server automatically in case of a fault of one server, without affecting the normal operation of business.

Based on the bandwidth cap, VPN gateway is available in 5 bandwidth levels: 5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps and 100 Mbps. You can adjust the VPN gateway bandwidth setting at any time and the change takes effect immediately.

If you need [Dayu Anti-DDoS](/document/product/297) to provide ultra-large bandwidth DDoS and CC defense for the VPN gateway, you can bind a Dayu high defense package to the VPN gateway for security protection.

## Customer Gateway
A customer gateway is a logical object that records the public IP address of the IPsec VPN gateway on IDC side, and it is used in conjunction with the Tencent Cloud VPN gateway. Encrypted VPN tunnels can be established between a VPN gateway and multiple customer gateways.

## VPN Tunnel
After a VPN gateway and a customer gateway are established, a VPN tunnel can be established for encrypted communication between your VPC and the external IDC. Currently, VPN tunnels support IPsec encryption protocol, which can meet the needs of most VPN connections.
A VPN tunnel runs in the ISP's public network. The congestion and jitter of the public network will affect the network condition of the VPN. Therefore, the expected service quality cannot be guaranteed as specified in the Service Level Agreement (SLA). If your business is sensitive to delay and jitter, it is recommended to connect to the VPC through Direct Connect. For more information, see [Direct Connect](https://cloud.tencent.com/product/dc.html).

### Establishing a VPN tunnel
Tencent Cloud VPN tunnel uses Internet Key Exchange (IKE) protocol to establish a session when implementing IPsec. IKE is provided with a self-protection mechanism that can securely authenticate identities, distribute keys and establish IPSec sessions over unsecured networks.
Establishing a VPN tunnel involves the following configuration information:
- Basic information
- Security Policy Database (SPD) policy
- IKE configuration (optional)
- IPsec configuration (optional)

The basic information, SPD policy, IKE configuration (optional) and IPsec configuration (optional) are described in detail below.



### SPD policy
- The Security Policy Database (SPD) policy consists of a series of SPD rules used to specify which IP address ranges of the VPC can communicate with IP address ranges of the IDC. Each SPD rule includes a CIDR for local IP address ranges and at least one CIDR for customer IP address ranges.
Note the following limitations on using SPD rules:
 - Rules for tunnels under the same VPN gateway cannot overlap.
 - Local IP address ranges for rules applied to any tunnel under the same VPN gateway cannot overlap.
 - Customer IP address ranges for a single rule cannot overlap.
 - The local IP address range of each rule must fall within IP address ranges of the [VPC](/document/product/215/4927).
 - The customer IP address range of each rule must not fall within IP address ranges of the [VPC](/document/product/215/4927).
- The following is a correct instance:
 - SPD policy 1: The local IP address range is `10.0.0.0/24`, and the customer IP address range is `192.168.0.0/24`/`192.168.1.0/24`.
 - SPD policy 2: The local IP address range is `10.0.2.0/24`, and the customer IP address range is `192.168.2.0/24`.
 - SPD policy 3: The local IP address range is `10.0.2.0/24`, and the customer IP address range is `192.168.2.0/24`.
![](//mccdn.qcloud.com/static/img/5b32174d312e31c5b5a9162a50456de8/image.png)

### IKE configuration
<style> table th:first-of-type { width: 150px; } </style>

| Configuration Item | Description |
| --------------- | ---------------------------------------- |
| Version | IKE V1                                   |
| Authentication method | Default pre-shared private key |
| Authentication algorithm | Authentication algorithm. MD5 and SHA1 are supported |
| Negotiation mode | Supports main mode and aggressive mode<br/>The difference is that more information can be sent with fewer packets in aggressive mode, which results in a quicker connection establishment. The downside is that the identity of security gateway has to be sent in plain text. When using aggressive mode, configuration parameters such as Diffie-Hellman and PFS may not be negotiated. Therefore, it's critical that their configurations are compatible on both sides |
| Local identity | Supports IP address and Fully Qualified Domain Name (FQDN) |
| Customer identity | Supports IP address and FQDN |
| DH group         | Specifies the DH group used during IKE. The security of key exchange increases with the expansion of the DH group, but the exchange time also increases<br/>Group1: DH group using 768-bit modular exponential (MODP) algorithm<br/> Group2: DH group using 1024-bit MODP algorithm<br/> Group5: DH group using 1536-bit MODP algorithm<br/>Group14: DH group using 2048-bit MODP algorithm. Dynamic VPN is not supported for this option<br/>Group24: DH group using 2048-bit MODP algorithm with a 256-bit prime order subgroup. Group VPN is not supported for this option |
| IKE SA Lifetime | Unit: second<br/>Sets the SA lifetime of IKE security proposal. Before the expiration of set lifetime, another SA will be negotiated in advance to replace the old SA. When the new SA has not been negotiated, the old SA will still be used. After the new SA is established, the new SA will be used immediately, and the old SA will be cleared automatically after its lifetime has expired |

### IPsec information
<style> table th:first-of-type { width: 150px; } </style>

| Configuration Item | Description |
| --------------------- | ---------------------------------------- |
| Encryption algorithm | Supports 3DES, AES-128, AES-192, AES-256, and DES |
| Authentication algorithm | Supports MD5 and SHA1 |
| Message encapsulation mode | Tunnel                                   |
| Security protocol | ESP                                      |
| PFS                    | Supports disable, dh-group1, dh-group2, dh-group5, dh-group14, and dh-group24 |
| IPsec SA lifetime(s)  | Unit: second |
| IPsec SA lifetime(KB) | Unit: KB |


