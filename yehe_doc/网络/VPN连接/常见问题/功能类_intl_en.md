 ### How does a VPN gateway work? How about its availability?
- A VPN gateway uses the network functions virtualization (NFV) and an active-active hot backup mechanism. When one server fails, automatic switchover helps ensure the normal operation of your businesses.
- Because a VPN tunnel runs on the public network, congestion, jitter, or delay on the public network may affect the VPN network. If your business is sensitive to delay and jitter, we recommend using the [Direct Connect](https://intl.cloud.tencent.com/document/product/216).

### What should I do if the VPN tunnel connection fails?
A VPN tunnel can successfully establish a connection only when both sides have the same negotiation information. You need to check the consistency of the configurations on both sides as follows:
>!
>- Inconsistency of any parameter can cause the failure to establish a VPN tunnel.
>- The default VPN configuration varies by devices and public cloud service providers.

1. Check the IKE configuration information for the first stage.
Check the consistency of all the parameters required in the first stage, including the IKE version, identity verification, encryption algorithm, authentication algorithm, negotiation mode, identifier, DH group, and IKE SA lifetime on both sides. In case of any inconsistency, correct it and try again.
The negotiation parameters in the first stage of the Tencent Cloud VPN gateway are configured as follows by default:
<table><tbody>
<tr><th>IKE Configuration Item</th><th>Default Configuration</th><th>Optional Configuration</th></tr>
<tr><td>IKE</td><td>V1</td><td>-</td></tr>
<tr><td>Identity verification</td><td>Pre-shared key</td><td>AES-128, AES-192, AES-256, and DES</td></tr>
<tr><td>Encryption algorithm</td><td>3DES</td><td>SHA1</td></tr>
<tr><td>Authentication algorithm</td><td>MD5</td><td>-</td></tr>
<tr><td>Negotiation mode</td><td>Main</td><td>Aggressive</td></tr>
<tr><td>Local identifier</td><td>IP address (public IP address of the Tencent Cloud VPN gateway by default)</td><td>FQDN</td></tr>
<tr><td>Customer identifier</td><td> IP address (public IP address of the customer VPN gateway by default)</td><td>FQDN</td></tr>
<tr><td>DH group</td><td>DH1</td><td>DH2, DH5, DH14, and DH24</td></tr>
<tr><td>IKE SA lifetime</td><td>86,400 seconds</td><td>-</td></tr>
</tbody></table>
2. Check the IPsec configuration information for the second stage.
Check the consistency of all the parameters required in the second stage, including the encryption algorithm, authentication method, message encapsulation mode, security protocol, PFS, and IPsec SA lifetime on both sides. In case of any inconsistency, correct it and try again.
The IPsec parameters in the second stage of the Tencent Cloud VPN gateway are configured as follows by default:
<table><tbody>
<tr><th>IPsec Configuration Item</th><th>Default Configuration</th><th>Optional Configuration</th></tr>
<tr><td>Encryption algorithm</td><td>3DES</td><td>AES-128, AES-192, AES-256, and DES</td></tr>
<tr><td>Authentication algorithm</td><td>MD5</td><td>SHA1</td></tr>
<tr><td>PFS</td><td>Disable</td><td>DH1, DH2, DH5, DH14, and DH24</td></tr>
<tr><td>IPsec SA lifetime</td><td>3,600 seconds</td><td>-</td></tr>
</tbody></table>

### Why does the monitoring data displayed on the VPN gateway and VPN tunnel sometimes differ?
Currently, VPN gateway and VPN tunnel collect data at a different interval. The statistical granularity of the VPN gateway is 1 minute, and that of the VPN tunnel is 10 seconds. Therefore, the statistical data shown on the monitoring page of the VPN gateway may be different from that of the VPN tunnel.


### How can I configure a VPN?
You can fully configure the IPsec VPN on the console. For more information, see [Getting Started Overview](https://intl.cloud.tencent.com/document/product/1037/32689).

### How can I create a VPN gateway?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to create a VPN gateway as instructed in [Step 1: Create a VPN Gateway](https://intl.cloud.tencent.com/document/product/1037/32690).

### How can I create a VPN tunnel?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to create a VPN gateway as instructed in [Step 3: Create a VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/32692).

### How can I query the VPN connection monitoring data?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to query the VPN connection monitoring data as instructed in [Viewing Monitoring Data](https://intl.cloud.tencent.com/document/product/1037/32698).

### How can I set a VPN connection alarm?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to set a VPN connection alarm as instructed in [Setting Alarms](https://intl.cloud.tencent.com/document/product/1037/32699).

### How can I query the VPN gateway details?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to query the VPN gateway details as instructed in [Viewing VPN Gateway Details](https://intl.cloud.tencent.com/document/product/1037/32700).

### How can I modify the VPN tunnel configuration?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to modify the VPN tunnel configuration as instructed in [Modifying VPN Tunnel Configuration](https://intl.cloud.tencent.com/document/product/1037/32701).

### How can I bind an Anti-DDoS instance?
You can log in to the [Anti-DDoS Pro console](https://console.cloud.tencent.com/ddos/overview) to bind an Anti-DDoS instance as instructed in [Binding an Anti-DDoS Instance](https://intl.cloud.tencent.com/document/product/1037/32705).
