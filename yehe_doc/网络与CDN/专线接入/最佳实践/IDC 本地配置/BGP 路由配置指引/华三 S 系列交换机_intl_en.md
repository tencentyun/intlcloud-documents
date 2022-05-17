Direct Connect connects Tencent Cloud with the user IDC with a dedicated physical line. After configuring the Direct Connect gateway and dedicated tunnel on the Tencent Cloud side, users need to configure routes on the local IDC. Using the layer-3 sub-interfaces to connect to Tencent Cloud is recommended.

>?This document only introduces the local routing configurations associated with Tencent Cloud Direct Connect. For other information, please see the local router documentation or consult your router provider.

## Routing Configuration
>?It's recommended that you use the default configurations of `Keepalive` and `holdtime` for the BGP connection between the two peers. The `holdtime` is three times the interval at which keepalive messages are sent. The recommended `holdtime` value is 180s.
>
``` 
# Configure ports
interfaces <interface_number>
description <interface_desc>
port link-mode route
undo shutdown
speed <interface_speed>
duplex full

# Configure layer 3 sub-interfaces
interface  interface-number.subnumber
description <vlan_description>
dot1q termination vid <vlanid>
ip address <subinterface_ipaddress> <subinterface_netmask>
bfd min-transmit-interval <value> //BFD parameter
bfd min-receive-interval <value>  //BFD parameter
bfd detect-multiplier <value>  //BFD parameter


# Set eBGP
bgp <as_number>
#router-id <route_id>
peer <bgp_peer_address> as-number <bgp_peer_as_number>
peer <bgp_peer_address> password cipher <bgp_auth_key>
peer <bgp_peer_address> description <bgp_desc>

# Configure BFD for eBGP
peer <bgp_peer_address> bfd
```
