Direct Connect connects Tencent Cloud to the user IDC through connections. After configuring the Direct Connect gateway and dedicated tunnel on the Tencent Cloud side, users need to configure routes on the local IDC.
>?This document only introduces the local routing configurations associated with Tencent Cloud Direct Connect. For other information, please see the local router documentation or consult your router provider.

## Routing Configuration
``` 
# Set ports
interfaces <interface_number>
description <interface_desc>
undo portswitch
undo shutdown
speed <interface_speed>
duplex full
undo negotiation auto
commit

# Set virtual tunnels (layer 3 sub-interfaces)
interface  <interface_number>.subinterface-number
description <subinterface_desc>
dot1q termination vid <vlanid>
ip address <subinterface_ipaddress> <subinterface_netmask>

# Set eBGP 
bgp <as_number>
#router-id <route_id>
peer <bgp_peer_address> as-number <bgp_peer_as_number>
peer <bgp_peer_address> password cipher <bgp_auth_key>
peer <bgp_peer_address> description <bgp_desc>
ipv4-family unicast
peer <bgp_peer_address> enable
commit

```
