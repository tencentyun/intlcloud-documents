Direct Connect connects Tencent Cloud with the user IDC with a dedicated physical line. After configuring the Direct Connect gateway and dedicated tunnel on the Tencent Cloud side, users need to configure routes on the local IDC.
>?This document only introduces the local routing configurations associated with Tencent Cloud Direct Connect. For other information, please see the local router documentation or consult your router provider.
>

## Routing Configuration
>?It's recommended that you use the default configurations of `Keepalive` and `holdtime` for the BGP connection between the two peers. The `holdtime` is three times the interval at which keepalive messages are sent. The recommended `holdtime` value is 180s.
>
``` 
# Configure ports
set interfaces <interface_number> description <interface_desc>
set interfaces <interface_number> vlan-tagging
set interfaces <interface_number> link-mode full-duplex
set interfaces <interface_number> speed <interface_speed> // Whether this command can be configured depends on whether the module supports it
set interfaces <interface_number> gigether-options no-auto-negotiation // This command is recommended to be used in combination with
Usage
commit

# Configure virtual tunnels
set interfaces <interface_number> unit <subinterface_number> vlan-id <subinterface_vlanid>
set interfaces <interface_number> unit <subinterface_number> description <subinterface_desc>
set interfaces <interface_number> unit <subinterface_number> family inet address
<subinterface_ipaddress>/<subinterface_netmask>
commit

# Configure static routing
# Configure a static route to the user IP globally
set routing-options static route <customer_prefix/mask> next-hop <customer_interface_ip>
# Configure BFD for the static routes. To configure RPM for the static routes, consult equipment vendors.
set routing-options static route <customer_prefix/mask>bfd-liveness-detection minimum-interval <value> 

such as set routing-options static route 1.1.1.0/24 next-hop 192.168.1.2 bfd-liveness-detection minimum-interval 1000 

# Configure a static route to the user IP in VRF mode
set routing-instances <vrf_name> routing-options static route <customer_prefix/mask> next-hop
<customer_interface_ip>
such as set routing-instances cap routing-options static route 1.1.1.0/24 next-hop 192.168.1.2
commit

```
