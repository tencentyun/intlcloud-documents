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
undo portswitch
undo shutdown
speed <interface_speed>
duplex full
undo negotiation auto
commit

# Configure virtual tunnels (layer 3 sub-interfaces)
interface  <interface_number>.subinterface-number
description <subinterface_desc>
dot1q termination vid <vlanid>
ip address <subinterface_ipaddress> <subinterface_netmask>

# Configure NQA detection for static routes
nqa test-instance <admin-name>< test-name>
 test-type icmp  //Default detection type
 destination-address  x.x.x.x（nexthop-address ）//Detection address
 interval seconds <value> //Detection interval
 timeout <value> //Timeout period
 probe-count <value> //Number of packets per detection
 frequency <value> //Detection frequency
 start now


# Configure static routing
# Configure global static routes
ip route-static <ip-address> <mask | mask-length> <nexthop-address>track nqa  <admin-name>< test-name>//<ip-address>
Destination IP ranges for users to access Tencent network services
such as ip route-static 172.16.0.192 255.255.255.192 10.128.152.1 track nqa user test

# Configure static routes for users to access Tencent Cloud in VRF mode
ip route-static <vpn-instance vpn-instance-name> <ip-address> <mask | mask-length> <nexthop-
address>track nqa  <admin-name>< test-name>
such as ip route-static vpn-instance GLOBAL 9.0.0.0 255.0.0.0 10.128.152.1 track nqa user test
commit

```
