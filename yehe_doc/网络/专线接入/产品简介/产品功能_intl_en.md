## Connection
A connection is a physical line that connects customer’s local IDC to Tencent Cloud. You can establish a network connection between your IDC and Tencent Cloud Direct Connect access point through a third-party network service provider.

## Dedicated Tunnel
- Dedicated tunnels are the network link segmentations of a connection.
- You can create dedicated tunnels that connect to different direct connect gateways, making the interconnection between your on-premises IDC and multiple VPCs possible.

## Direct Connect Gateway
- A direct connect gateway is the ingress and egress of the dedicated tunnel between VPC and connection. A VPC supports up to 2 direct connect gateways (one standard and the other supports NAT).
- Direct connect gateways can connect to multiple connections through dedicated tunnels. This allows for a hybrid cloud that connects with multiple regions.

## Network Address Translation (NAT)
NAT is a solution that addresses the IP address conflicts when connecting hybrid clouds. You can configure NAT rules on direct connect gateways. NAT includes IP translation and IP port translation.
### IP translation
- IP translation translates the original IPs to a new IP address for network interconnection. IP translation includes **local IP translation** and **peer IP translation**.
- IP translation does not distinguish between source and destination. A mapped IP can access or be accessed by IDC.

#### Local IP translation
**1. Description**
 - Local IP translation maps the IP address of a resource in a Tencent Cloud VPC to a new one and use the new IP address to communicate with the on-premise IDCs.
 - You can set more than one local IP translation rule and configure network ACL for each local IP translation rule. Network ACL supports configuring source port, destination IP, and destination port.
>!NAT rules take effect only for network requests that meet ACL restriction requirements.
 - Local IP translation does not restrict the direction of network requests, which could be active access of the VPC to the IDC or vice versa.
 ![](https://main.qcloudimg.com/raw/034c4a7af620026fdede9dc722a582fc.png)

**2. Sample translation**
If IP A `192.168.0.3` in a VPC is mapped to IP B `10.100.0.3`, the IP address of all network packets accessing the IDC from IP A via Direct Connect is automatically translated to `10.100.0.3`. All network packets accessing `10.100.0.3` from the IDC are automatically directed to IP A `192.168.0.3`.

#### Peer IP translation
**1. Description**
 - Peer IP translation maps the IP address of an IDC resource to a new one and uses the IP address to communicate with the VPC.
 - Unlike local IP translation, peer IP translation does not support network ACL restrictions. Therefore, once peer IP translation rules are configured, they take effect on all IDCs that are connected with dedicated tunnels.
 - Peer IP translation does not restrict the direction of network requests, which can be active access of the VPC to the IDC or vice versa.
![](https://main.qcloudimg.com/raw/770fdb55f2f1ea69fc4b8ee563194dda.png)

**2. Sample translation**
If IP D `10.0.0.3` in an IDC is mapped to IP C `172.16.0.3`, the IP address of all network packets accessing the VPC from IP D `10.0.0.3` is automatically translated to IP C `172.16.0.3`. All network packets accessing IP C `172.16.0.3` from the VPC are automatically directed to IP D `10.0.0.3`.

>!
- After local IP translation and peer IP translation are configured, direct connect gateway only forwards the routes of the translated IPs to the IDC. Therefore, an IP address that has not been configured with local and peer IP translation will not be able to ping the IDC. However, a direct connect gateway is not a replacement for network firewalls. If you need advanced network protection, please configure security groups and network ACL policies within your VPC and deploy physical network firewall devices in your IDC.
- When the direct connect gateway is also configured with peer IP translation, the **Destination IP** of the ACL rule for local original IP port translation should be the **mapped IP of peer IP translation**, instead of the original IP.

### IP port translation
- IP port translation maps the original IP port to a new one and use the new IP port for network interconnection. IP port translation includes **local source IP port translation** and **local destination IP port translation**.
- IP port translation is directional. Source IP port translation is for requests to external (to the IDC) resources, and destination IP port translation is for requests from external (to the VPC) resources.

#### Local source IP port translation
**1. Description**
 - Local source IP port translation translates the port of the original VPC IP address to a random port of a random IP address in the IP pool when a cloud resource accesses the IDC through a direct connect gateway.
 - Local source IP port translation supports ACL rules. Only outbound access requests compliant with ACL rules can be matched with address pool forwarding rules. By deploying different ACL rules for the address pool, you can flexibly configure the network address translation rules with multiple third-party access.
![](https://main.qcloudimg.com/raw/ad5969948df4e434c846423206429e7c.png)

- Local source IP port translation only supports access requests initiated by resources in VPCs. To access ports within the VPC via Direct Connect, the IDC should also be configured with local destination IP port translation. For local source IP port translation, access requests initiated by resources in VPCs are stateful connections. Therefore, response packets are not a concern.

**2. Sample translation**
VPC C with an IP range `172.16.0.0/16` needs to connect to third-party bank A and B via Direct Connect. Bank A with an IP range `10.0.0.0/28` needs to connect to the IP range `192.168.0.0/28`. Bank B with an IP range `10.1.0.0/28` needs to connect to the IP range `192.168.1.0/28`. For them to communicate, you need to configure the following local source IP port translations:
- Address pool A `192.168.0.1 - 192.168.0.15`; ACL rule A: source IP `172.16.0.0/16`, destination IP `10.0.0.0/28`, destination port ALL.
- Address pool B `192.168.1.1 - 192.168.1.15`; ACL rule B: source IP `172.16.0.0/16`, destination IP `10.1.0.0/28`, destination port ALL.

The access requests from the VPC to Bank A and B are respectively translated into a random port of the address pool that satisfies ACL rule A or B to access the appropriate dedicated tunnels.

#### Local destination IP port translation
**1. Description**
 - Local destination IP port translation handles requests to cloud resources in a VPC from the IDC. It translates the VPC IP address and port to a new IP address and a new port. IDC can only communicate with VPC resources by sending requests to the mapped IP address and port, without exposing the real one.
![](https://main.qcloudimg.com/raw/394a9e3444d23ec4b18af4aaf7198671.png)

 - Local destination IP port translation does not support ACL rules. Therefore, IP port translation rules will take effect on all dedicated tunnels connected to the direct connect gateway. Local destination IP port translation only takes effect on requests from IDC to a VPC via dedicated tunnels. To access an IDC, the VPC should be configured with local source IP port translation. For local destination IP port translation, the network requests are stateful connections. Therefore, response packets are not a concern.

**2. Sample translation**
For VPC C with an IP range `172.16.0.0/16`, if you only want to open some ports for IDC to access the VPC via Direct Connect, you can configure it as follows:
- Mapping A: the original IP port is `172.16.0.1:80` and the mapped IP port is `10.0.0.1:80`.
- Mapping B: the original IP port is `172.16.0.0:8080` and the mapped IP port is `10.0.0.1:8080`.
The IDC can use `10.0.0.1:80` and` 10.0.0.1:8080` via Direct Connect to access `172.16.0.1:80` and `172.16.0.0:8080` in the VPC.

>!
- After local source and destination IP port translations are configured, the direct connect gateway only forwards the translated IP port routes to the IDC. Therefore, the local IP port that is not configured with translations cannot initiate requests nor receive requests. However, a direct connect gateway is not a replacement for network firewalls. If you need advanced network protection, please configure security groups and network ACL policies within your VPC and deploy physical network firewall devices in your IDC.
- When both IP translation and IP port translation are configured, IP translation has priority. If there is no match for IP translation, IP port translation is used.
- When the direct connect gateway is also configured with peer IP translation, the **Destination IP** of the ACL rule for local source IP port translation should be the **mapped IP of peer IP translation**, instead of the original IP.

