Direct Connect connects Tencent Cloud with the user IDC with a dedicated physical line. After configuring the Direct Connect gateway and dedicated tunnel on the Tencent Cloud side, users need to configure routes on the local IDC.
>?This document only introduces the local routing configurations associated with Tencent Cloud Direct Connect. For other information, please see the local router documentation or consult your router provider.
>

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
commit

# Configure IP SLA (NQA)
ip sla <operation-number>
icmp-echo x.x.x.x<nexthop_address> source-ip x.x.x.x <source_address>
frequency <value> //Set a detection frequency
timeout <value> //Set a timeout period
ip sla schedule <operation-number> life forever start-time now
en

# Configure Track-associated IP SLA
track <operation-number> ip sla <operation-number> reachability
end

# Configure static routing
router static
vrf <vrf-name> //If no VRF is specified, the static route is in the default VRF mode.
  address-family <ipv4 | ipv6> unicast
  <ip-prefix/netmask> <next_hop_ip> <interface_number> <description_text> <distance> <tag tag_value> track <operation-number>
commit

```
