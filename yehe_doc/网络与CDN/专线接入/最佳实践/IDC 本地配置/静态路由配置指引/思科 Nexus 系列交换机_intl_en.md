Direct Connect connects Tencent Cloud with the user IDC with a dedicated physical line. After configuring the Direct Connect gateway and dedicated tunnel on the Tencent Cloud side, users need to configure routes on the local IDC. Using the layer-3 sub-interfaces to connect to Tencent Cloud is recommended.
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
no switchport
speed <interface_speed>
duplex full
no negotiation auto
end

# Configure layer 3 sub-interfaces
interface  interface-number.subnumber
description <vlan_description>
encapsulation dot1q <vlanid>
ip address <subinterface_ipaddress> <subinterface_netmask>
end

# Configure IP SLA (NQA)
ip sla <operation-number>
icmp-echo x.x.x.x<nexthop_address> source-ip x.x.x.x <source_address>
frequency <value> //Set a detection frequency
timeout <value> //Set a timeout period
ip sla schedule <operation-number> life forever start-time now
end

# Configure Track-associated IP SLA
track <operation-number> ip sla <operation-number> reachability
end

# Configure static routes and associate track
ip route <ip_prefix/netmask> <interface_number | vlan_id> <next_hop_ip> <name nexthop_name><distance> <tag tag_value> track <operation-number>

```
