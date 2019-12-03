 ### How is a VPN Gateway implemented? How is its availability?
- A VPN gateway is implemented through network functions virtualization (NFV). With a dual-server hot backup mechanism, the system automatically switches to another server when one server becomes faulty, without affecting the normal operation of business.
- Since VPN tunnels run on public networks, congestion, jitter, or delay of the public networks may affect the quality of the VPN network. If your business is sensitive to delay and jitter, it is recommended that you use Direct Connect.

### Is SSL-VPN supported?

No. Currently, only IPsec VPN is supported. To use SSL-VPN, it is recommended that you purchase Cloud Marketplace [SSL-VPN](https://market.cloud.tencent.com/search/SSLVPN) products.

### What can I do when the VPN tunnel connection fails?

A connection can be established successfully through a VPN tunnel only when the same negotiation information is configured for both ends. You need to check the consistency of the configurations at both ends as follows:
>
>- Inconsistency of any parameter can cause the failure to establish a VPN tunnel.
>- The default VPN configuration varies for different devices and public cloud service providers.

1. Check the IKE configuration information for the first stage.
Check the consistency of all the parameters required in the first stage, including the IKE version, authentication method, encryption algorithm, authentication algorithm, negotiation mode, identifier, DH group, and IKE SA lifetime at the both ends. In case of any inconsistency, correct it and try again.
The negotiation parameters in the first stage of the Tencent Cloud VPN gateway are configured as follows by default:
<table><tbody>
<tr><th>IKE configuration item</th><th>Default configuration</th><th>Optional configuration</th></tr>
<tr><td>IKE</td><td>V1</td><td>-</td></tr>
<tr><td>Authentication method</td><td>Pre-shared key</td><td>AES-128, AES-192, AES-256, and DES</td></tr>
<tr><td>Encryption algorithm</td><td>3DES</td><td>SHA1</td></tr>
<tr><td>Authentication algorithm</td><td>MD5</td><td>-</td></tr>
<tr><td>Negotiation mode</td><td>Main</td><td>Aggressive</td></tr>
<tr><td>Local identifier</td><td>IP address (public IP address of the Tencent Cloud VPN gateway by default)</td><td>FQDN</td></tr>
<tr><td>Customer identifier</td><td> IP address (public IP address of the customer VPN gateway by default)</td><td>FQDN</td></tr>
<tr><td>DH group</td><td>DH1</td><td>DH2, DH5, DH14, and DH24</td></tr>
<tr><td>IKE SA lifetime</td><td>86,400 seconds</td><td>-</td></tr>
</tbody></table>
2. Check the IKE configuration information for the second stage.
Check the consistency of all the parameters required in the second stage, including the encryption algorithm, authentication method, packet encapsulation mode, security protocol, PFS, and IPsec SA lifetime at both ends. In case of any inconsistency, correct it and try again.
The IPsec parameters in the second stage of the Tencent Cloud VPN gateway are configured as follows by default:
<table><tbody>
<tr><th>IPsec configuration item</th><th>Default configuration</th><th>Optional configuration</th></tr>
<tr><td>Encryption algorithm</td><td>3DES</td><td>AES-128, AES-192, AES-256, and DES</td></tr>
<tr><td>Authentication algorithm</td><td>MD5</td><td>SHA1</td></tr>
<tr><td>PFS</td><td>Disable</td><td>DH1, DH2, DH5, DH14, and DH24</td></tr>
<tr><td>IPsec SA lifetime</td><td>3,600 seconds</td><td>-</td></tr>
</tbody></table>
