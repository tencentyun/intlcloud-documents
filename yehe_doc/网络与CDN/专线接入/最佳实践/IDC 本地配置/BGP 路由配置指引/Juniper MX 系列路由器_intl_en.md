Direct Connect connects Tencent Cloud to the user IDC through connections. After configuring the direct connect gateway and dedicated tunnel on the Tencent Cloud side, users need to configure routes on the local IDC.
>?This document only introduces the local routing configurations associated with Tencent Cloud Direct Connect. For other information, please see the local router documentation or consult your router provider.
>

## Routing Configuration
``` 
# Configure ports
set interfaces <interface_number> description <interface_desc>
set interfaces <interface_number> vlan-tagging
set interfaces <interface_number> link-mode full-duplex
set interfaces <interface_number> speed <interface_speed> // Whether this command can be configured depends on whether the module supports it
set interfaces <interface_number> gigether-options no-auto-negotiation // This command is recommended to be used in combination with
the previous one
commit

# Configure virtual tunnels
set interfaces <interface_number> unit <subinterface_number> vlan-id <subinterface_vlanid>
set interfaces <interface_number> unit <subinterface_number> description <subinterface_desc>
set interfaces <interface_number> unit <subinterface_number> family inet address
<subinterface_ipaddress>/<subinterface_netmask>
commit

# Set eBGP 
set protocols bgp group ebgp type external // Define protocol group. Changing ebgp name is allowed.
set protocols bgp group ebgp neighbor <bgp_peer_address> loacal-as <as_number> // If not configured, the global AS number will be used
 by default (set routing-options autonomous-system XX)
set protocols bgp group ebgp neighbor <bgp_peer_address> peer-as <bgp_peer_as_number>
set protocols bgp group ebgp neighbor <bgp_peer_address> authentication-key <bgp_auth_key>
set protocols bgp group ebgp neighbor <bgp_peer_address> description <bgp_peer_desc>
commit

```
