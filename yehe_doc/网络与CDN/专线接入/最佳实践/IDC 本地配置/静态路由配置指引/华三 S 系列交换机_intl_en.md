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
port link-mode route
undo shutdown
speed <interface_speed>
duplex full

# Configure layer 3 sub-interfaces
interface  interface-number.subnumber
description <vlan_description>
dot1q termination vid <vlanid>
ip address <subinterface_ipaddress> <subinterface_netmask>

# Configure NQA detection for static routes
nqa entry <admin-name> < test-name>
type icmp-echo  //Default detection type
destination-address  x.x.x.x（nexthop-address ）//Detection address
interval seconds 2 //Detection interval
frequency <value> //Detection frequency
history-record enable
probe count  <value> //Number of packets per detection
probe timeout <value> //Timeout period 

# Configure Track 
track <number> nqa entry  <admin-name>< test-name> //Associate Track with NQA

# Configure static routing
ip route-static <Destination_IP_address> <Mask_of_the-IP_address> <VLAN_interface> track <number> 

```
