This document describes how to accelerate routing convergence between customer IDC and private network by initiating BGP routing protocol on the local IDC switch and configuring bidirectional forwarding detection (BFD) on Tencent Cloud direct connect gateway.

## Background
![](https://qcloudimg.tencent-cloud.cn/raw/bc455a9ac71c934c7e6908d3c4819af1.jpg)
>! In a connection using static routes, we recommended that you use static routes and BFD/NQA to achieve route convergence.
>
- The connection connects the IDC switch and the layer 3 network sub-interface of Tencent Cloud switch, thereby connecting IDC and Tencent Cloud network. 
- Implement mutual access to resources through VPC/CCN.
- Implement routing convergence through BGP+BFD/NQA.

## Prerequisite
- You have built a VPC as instructed in [Building Up an IPv4 VPC](https://www.tencentcloud.com/document/product/215/31891).
- You have applied for a connection as instructed in [Applying for Connection](https://www.tencentcloud.com/document/product/216/19244) and completed the preparatory construction.


## Configuration Guide
### Step 1. Create a direct connect gateway
For more information, see [Creating a Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).

### Step 2. Create a dedicated tunnel
The tunnels created on the connections vary depending on the access method.
- The tunnels created on your own connections are exclusive dedicated tunnels, which are applicable to scenarios with requirements for high-bandwidth access and exclusive access. For more information, see [Exclusive Virtual Interface](https://intl.cloud.tencent.com/document/product/216/48574).
- The tunnels created on our partners' connections pre-established in Tencent are shared dedicated tunnels, which are applicable to scenarios where there is no need for high-bandwidth access and the cloudification time is short. For more information, see [Shared Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/48575).

### Step 3. Configure health check
For more information, see [Dedicated tunnel health check](https://intl.cloud.tencent.com/document/product/216/46292).


### Step 4. Completing the IDC local configuration as instructed in [Huawei NE Series Routers](https://intl.cloud.tencent.com/document/product/216/46925) 
This document takes Huawei CE switch as an example. For other local configurations, see [Huawei NE Series Routers](https://intl.cloud.tencent.com/document/product/216/46925).
If you can't implement the layer 3 sub-interface connection due to special reasons, you can try layer 2 sub-interfaces. For details, see Mode 2.
- **(Recommended) Mode 1: Layer 3 sub-interface+BGP**
``` 
# Set sub-interfaces for layer 3 connection
interfaces
<interface_number>.<sub_number>
description <interface_desc>
dot1q termination vid <vlan id>
ip address <subinterface_ipaddress>
<subinterface_netmask>
speed <interface_speed>
duplex full
undo negotiation auto
commit
# Set eBGP 
bgp <as_number>
router-id <route_id>
peer <bgp_peer_address> as-number
<bgp_peer_as_number>
peer <bgp_peer_address> password cipher
<bgp_auth_key>
peer <bgp_peer_address> description
<bgp_desc>
ipv4-family unicast
peer <bgp_peer_address> enable
commit
# Set BFD configuration of eBGP
bgp <as_number>
router-id <route_id>
peer <bgp_peer_address> bfd min-tx-interval
1000 min-rx-interval 1000 detect-multiplier 3
```


- **Mode 2: Layer 2 Vlanif interface+BGP (It is recommended to disable STP for layer 2 interfaces)**
``` 
# Set ports
interfaces
<interface_number>
description
<interface_desc>
port link-type
trunk
undo shutdown
speed
<interface_speed>
duplex full
undo negotiation
auto
stp disable ** (****Disable****stp****STP****)**
commit
# Set virtual tunnels
vlan
<subinterface_vlanid>
description
<subinterface_desc>
# Set logic interfaces
interface Vlanif
<subinterface_vlanid>
description <subinterface_desc>
ip address
<subinterface_ipaddress> <subinterface_netmask>
# Configure interface VLAN
interfaces
<interface_number>
port trunk
allow-pass vlan <subinterface_vlanid>
commit
# Set eBGP 
bgp
<as_number>
router-id
<route_id>
peer
<bgp_peer_address> as-number <bgp_peer_as_number>
peer
<bgp_peer_address> password cipher <bgp_auth_key>
peer
<bgp_peer_address> description <bgp_desc>
ipv4-family
unicast
peer
<bgp_peer_address> enable
# Set BFD configuration of eBGP
bgp <as_number>
router-id <route_id>
peer <bgp_peer_address> bfd min-tx-interval
1000 min-rx-interval 1000 detect-multiplier 3
commit
```



## How to Set Keepalive and Holdtime Parameters
After establishing a BGP connection between two peers, the two peers periodically send keepalive messages to the peer to maintain the validity of the BGP connection. If a router does not receive a keepalive message or any other type of packet from the peer within the specified holdtime, the BGP connection is considered to have been interrupted and thus the BGP connection is interrupted.

The keepalive-time and hold-time values are determined through negotiation between the two peers. The smaller hold-time value in the Open message of both peers is the final hold-time value. The smaller value between **the result of the negotiated hold-time value divided by 3** and the locally configured keepalive-time value is used as the final keepalive-time value.
When the BGP connection is established, the recommended holdtime is 180 seconds (default value used by most vendors).

If the configured holdtime is less than 30 seconds, the linkage may interrupt the neighbor session in normal cases, and linkage jitter detection is required. You are advised to enable BFD to improve convergence performance.
