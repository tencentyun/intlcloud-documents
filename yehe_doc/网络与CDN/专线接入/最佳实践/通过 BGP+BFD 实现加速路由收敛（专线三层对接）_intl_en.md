This document describes how to accelerate routing convergence between customer IDC and private network by initiating BGP routing protocol on the local IDC switch and configuring bidirectional forwarding detection (BFD) on Tencent Cloud Direct Connect gateway.

## Background
![]()
>! In a connection using static routes, It's recommended that you use static route +BFD/NQA to achieve route convergence.
>
- The connection connects the IDC switch and the layer 3 network sub-interface of Tencent Cloud switch, thereby connecting IDC and Tencent Cloud network. 
- Implement mutual access to resources through VPC/CCN.
- Implement routing convergence through BGP+BFD/NQA.

## Prerequisites
- You have built a VPC as instructed in [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).
- You have applied for a connection as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244) and completed the preparatory construction.


## Configuration Guide
### Step 1. [Creating a Direct Connect gateway](https://intl.cloud.tencent.com/document/product/216/19256) 
1. Log in to the Direct Connect Gateway console. Click **Direct Connect Gateway** in the left sidebar.
2. Select a region and VPC at the top of the **Direct Connect Gateway** page, and click **+New**.
![]()
3. Complete the configurations in the pop-up window and click **OK**.
![]()

### Step 2. [Creating a dedicated tunnel](https://intl.cloud.tencent.com/document/product/216/19250) 
1. Log in to the [Direct Connect - Dedicated Tunnel](https://console.cloud.tencent.com/dc/dcConn) console.
2. Complete basic configurations such as name, connection type, access network, region and associated direct connect gateway, and click **Next**.
 <img src="" width="70%">
3. Configure the following parameters on the **Advanced Configuration** page, and then click **OK**.
 <img src="" width="70%">


### Step 3. Configuring health check as instructed in [Dedicated Tunnel Health Check](https://intl.cloud.tencent.com/document/product/216/46292)
1. Click the name of the created tunnel on the **Dedicated Tunnel** page.
 ![]()
2. Click **Edit** on the right of **Routing Modes** on the **Advanced Tunnels** tab of the tunnel details page.
3. Enable **Health Check**.
4. Configure the parameters of health check, and click **Save**.</br>
 <img src="" width="70%">

### Step 4. Completing the IDC local configuration as instructed in [Huawei NE Series Routers](https://intl.cloud.tencent.com/document/product/216/46925) 
This document takes Huawei CE switch as an example. For other local configurations, see [Huawei NE Series Routers](https://intl.cloud.tencent.com/document/product/216/46925).
If you can't implement the layer 3 sub-interface connection due to special reasons, you can try layer 2 sub-interfaces. For details, see Mode 2.
- **(Recommended) Mode 1: Layer 3 sub-interface+BGP**:
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


- <b>Mode 2: Layer 2 Vlanif interface+BGP (It is recommended to disable STP of Layer 2 interfaces)</b>：
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
VLAN
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
