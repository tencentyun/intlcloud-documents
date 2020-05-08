The following video describes the components of Direct Connect.
<div class="doc-video-mod"><iframe src="https://cloud.tencent.com/edu/learning/quick-play/1670-12009?source=gw.doc.media&withPoster=1&notip=1"></iframe></div>

## Connection
A connection is a physical line that connects Tencent Cloud with your on-premises IDC. You can establish a network connection between your IDC and the Tencent Cloud Direct Connect access point through a third-party network service provider.
## Dedicated Tunnel
- Dedicated tunnels are the network link segmentations of a connection.
- You can create dedicated tunnels that connect to different Direct Connect gateways, making the interconnection between your on-premises IDC and multiple VPCs possible.

## Direct Connect Gateway
- A Direct Connect gateway is the ingress point of the dedicated tunnel that connects to the VPC. A VPC supports up to 2 Direct Connect gateways (one supports NAT and the other does not).
- Direct Connect gateways can establish dedicated tunnels with multiple connections. This allows for a hybrid cloud that connects with multiple regions.

## Network Address Translation (NAT)
NAT is a solution that addresses the IP address conflicts when connecting hybrid clouds. You can configure NAT rules on Direct Connect gateways. NAT includes IP translation and IP port translation.
### IP translation
- IP translation translates the original IP address to a new IP address for the purpose of network interconnection. IP translation includes **local IP translation** and **peer IP translation**.
- IP translation does not distinguish between source and destination. A mapped IP can either actively access the peer or be accessed by the peer.

#### Local IP translation
**1. Description**
 - Local IP translation maps the IP address of a Tencent Cloud resource in a VPC to a new IP addressre so it can use the new IP address to communicate with the on-premise IDCs.
 - You can set more than one local IP translation rule and configure network ACL for each local IP translation rule. Network ACL supports the configuration of source port, destination IP, and destination port.
> NAT rules take effect only for network requests that meet ACL restriction requirements.
 - Local IP translation does not restrict the direction of network requests, which could be the active access of the VPC to the Direct Connect peer or vice versa.


**2. Sample translation**
If IP A `192.168.0.3` in a VPC is mapped to IP B `10.100.0.3`, the origin IP address of all network packets from `192.168.0.3` are automatically translated to `10.100.0.3` when they exit the VPC. All network packets accessing `10.100.0.3` from the Direct Connect peer is automatically directed to IP A `192.168.0.3`

#### Peer IP translation
**1. Description**
 - Peer IP translation maps the IP address of an IDC resource to a new one and uses the IP address to communicate with the VPC.
 - Unlike local IP translation, peer IP translation does not support network ACL restrictions. Therefore, once peer IP translation rules are configured, they take effect for all dedicated tunnel peers.
 - Peer IP translation does not restrict the direction of network requests, which can be the active access of the VPC to the Direct Connect peer or vice versa.

**2. Sample translation**
If Direct Connect peer IP D `10.100.0.3` is mapped to IP C`172.16.0.3`, the network packet original IP of the active access of IP D `10.100.0.3` to the Direct Connect is automatically changed to IP C `172.16.0.3`, and all network packets accessing IP C `172.16.0.3` from the VPC are automatically directed to IP D `10.0.0.3`.

>
>- After local IP translation and peer IP translation are configured, Direct Connect gateway only delivers the routes of the translated IPs to the Direct Connect peer. Therefore, the IP addresses that has not been configured with local and peer IP translation will not be able to ping the Direct Connect peer. However, Direct Connect gateways is not a replacement for network firewalls. If you need advanced network protection, you should configure security groups and network ACL policies within your VPC and deploy physical network firewall devices in your IDC.
>- When the Direct Connect gateway is also configured with Peer IP Translation, the **Destination IP** of the ACL rule for local original IP port translation should be the **mapped IP of peer IP translation**, instead of the original IP.

### IP port translation
- IP port translation refers to the mapping of original IP port to a new IP port for the purpose of network communication using the new IP port. IP port translation includes **local source IP port translation** and **local destination IP port translation**.
- IP port translation is directional. Source IP port translation is for requests to external (to the VPC) resources and destination IP port translation is for requests from external (to the VPC) resources.

#### Local source IP port translation
**1. Description**
 - Local source IP port translation refers to the translation of the port of the original VPC IP address to a random port of a random IP address in the IP pool when a cloud resource send requests to the IDC through a Direct Connect gateway.
 - Local source IP port translation supports ACL rules. Only outbound requests compliant with ACL rules can be matched with address pool forwarding rules. By deploying different ACL rules for the address pool, you can flexibly configure the network address translation rules with multiple third-party access.


- Local source IP port translation only supports requests initiated by resources in VPCs. If the Direct Connect peer wants to access IP ports within the VPC, it should also be configured with local destination IP port configuration. For local source IP port translation, requests initiated by resources in VPCs are stateful connections. Therefore response packets are not a concern.

**2. Sample translation**
VPC C with an IP range of `172.16.0.0/16` need to connect to third-party bank A and B via Direct Connect. Bank A has an IP range of `10.0.0.0/28` and needs to connect to the IP range `192.168.0.0/28`. Bank B has an IP range of `10.1.0.0/28` and needs to connect to the IP range `192.168.1.0/28`. , requiring the connected network segment `192.168.1.0/28`. for them to communicate, you need to configure the following local source IP port translations:
- Address pool A `192.168.0.1 - 192.168.0.15`; ACL rule A: source IP `172.16.0.0/16`, destination IP `10.0.0.0/28`, destination port ALL.
- Address pool B `192.168.1.1 - 192.168.1.15`; ACL rule B: source IP `172.16.0.0/16`, destination IP `10.0.0.0/28`, destination port ALL.

The requests to Bank A and B from the VPC are translated into the random ports of corresponding address pools based on ACL rule A and B to access the appropriate dedicated tunnels.

#### Local destination IP port translation
**1. Description**
 - Local destination IP port translation handles requests to cloud resources in a VPC from the IDC. It translates the IP address and port of the cloud resource to a new IP address and a new port. Requests from the IDC use the new IP addresses and ports to access cloud resources without exposing the real IP addresses and ports.


 - Local destination IP port translation does not support ACL rules. Therefore, IP port translation rules are effective for all dedicated tunnels connected to the Direct Connect gateway. Local destination IP port translation only takes effect for requests from dedicated tunnel peers to VPCs. If VPCs need to access Direct Connect peers, it should be configured with local source IP port translation. For local destination IP port translation, the network requests are stateful connections. Therefore response packets are not a concern.

**2. Sample translation**
For the VPC C network IP range `172.16.0.0/16`, if you only want to open some of the ports to the active access of Direct Connect peers, you can configure as follows:
Mapping A: the original IP port is `172.16.0.1:80` and the mapped IP port is `10.0.0.1:80`.
Mapping B: the original IP port is `172.16.0.0:8080` and the mapped IP port is `10.0.0.1:8080`.
The Direct Connect peer can use `10.0.0.1:80` and` 10.0.0.1:8080` to access to `172.16.0.1:80` and `172.16.0.0:8080` in the VPC.

>
- After local source and destination IP port translations are configured, the Direct Connect gateway only delivers the translated IP port routes to the Direct Connect peer. Therefore, the local IP port that is not configured cannot initiate requests nor receive requests. However, Direct Connect gateways is not a replacement for network firewalls. If you need advanced network protection, you should configure security groups and network ACL policies within your VPC and deploy physical network firewall devices in your IDC.
- When IP translation and IP port translation are both configured, IP translation has priority. If there is no match for IP translation, IP port translation is used.
- When the Direct Connect gateway is also configured with peer IP translation, the **Destination IP** of the ACL rule for local source IP port translation should be the **mapped IP of peer IP translation**, instead of the original IP.
