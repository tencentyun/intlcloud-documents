Direct Connect connects Tencent Cloud with the user IDC with a dedicated physical line. After configuring the Direct Connect gateway and dedicated tunnel on the Tencent Cloud side, users need to configure routes on the local IDC.
>?This document only introduces the local routing configurations associated with Tencent Cloud Direct Connect. For other information, please see the local router documentation or consult your router provider.

## Routing Configuration
>?It's recommended that you use the default configurations of `Keepalive` and `holdtime` for the BGP connection between the two peers. The `holdtime` is three times the interval at which keepalive messages are sent. The recommended `holdtime` value is 180s.
>
``` 
# Configure ports
interfaces <interface_number>
description <interface_desc>
undo shutdown
speed <interface_speed>
duplex full
undo negotiation auto
commit

# Set virtual tunnels
interfaces <interface_number>.<subinterface_number>
description <subinterface_desc>
vlan-type dot1q <subinterface_vlanid>
ip address <subinterface_ipaddress> <subinterface_netmask>
commit

# Set eBGP
bgp <as_number>
router-id <route_id>
peer <bgp_peer_address> as-number <bgp_peer_as_number>
peer <bgp_peer_address> password cipher <bgp_auth_key>
peer <bgp_peer_address> description <bgp_desc>
ipv4-family unicast
peer <bgp_peer_address> enable
commit

# Configure BFD for eBGP
bgp <as_number>
router-id <route_id>
peer <bgp_peer_address> bfd min-tx-interval <time value> min-rx-interval <time value> detect-multiplier <value>
```
