Direct Connect connects Tencent Cloud with the user IDC with a dedicated physical line. After configuring the Direct Connect gateway and dedicated tunnel on the Tencent Cloud side, users need to configure routes on the local IDC.
>?This document only introduces the local routing configurations associated with Tencent Cloud Direct Connect. For other information, please see the local router documentation or consult your router provider.

## Routing Configuration
>?It's recommended that you use the default configurations of `Keepalive` and `holdtime` for the BGP connection between the two peers. The `holdtime` is three times the interval at which keepalive messages are sent. The recommended `holdtime` value is 180s.
>
``` 
# Configure ports
interfaces <interface_number>
description <interface_desc>
no shutdown
speed <interface_speed>
duplex full
no negotiation auto
commit

# Configure virtual tunnels
interfaces <interface_number>.<subinterface_number>
description <subinterface_desc>
encapsulation dot1q <subinterface_vlanid>
ipv4 address <subinterface_ipaddress> <subinterface_netmask>
bfd interval <value> min_rx <value> multiplier <value> //BFD parameter
commit

# Set eBGP
router bgp <as_number>
#bgp router-id <router_id>
neighbor <bgp_peer_address>
remote-as <bgp_peer_as_number>
password encrypted <bgp_auth_key>
description <bgp_peer_desc>
remote-as <bgp_peer_as_number> fall-over bfd //Configure BFD for BGP
commit

```
