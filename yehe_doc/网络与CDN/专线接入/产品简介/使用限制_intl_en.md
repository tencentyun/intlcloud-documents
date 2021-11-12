## Resource Limits
| Resource | Limit | Allow Applying for Higher Quota | Description |
|-------|-------|------------------|------------------|
| Connections per user | 10 | Yes | Each user can access up to 10 connections. |
| Dedicated tunnels per connection | 5 | Yes | Up to 5 dedicated tunnels can be created in a connection. |
| Direct connect gateway per VPC | 2 (one standard and the other supports NAT) | No | Each VPC supports up to two direct connect gateways. |
| Local IP translations per direct connect gateway | 100 | Yes | Each direct connect gateway supports up to 100 local IP translations. |
| Peer IP translations per direct connect gateway | 100 | Yes | Each direct connect gateway supports up to 100 peer IP translations. |
| Local source IP port translations per direct connect gateway | 20 | Yes | Each direct connect gateway supports up to 20 local source IP port translations. |
| Local destination IP port translations per direct connect gateway | 100 | Yes | Each direct connect gateway supports up to 100 local destination IP port translations. |
| Number of static routes per dedicated tunnel | 20    | No   | A dedicated tunnel supports up to 20 static routes. |
| Number of BGP routes per dedicated tunnel | 100 | No   | A dedicated tunnel supports up to 100 BGP routes. |

## Access Limits
### Direct Connect
- When a Direct Connect gateway is created, the content of IP translation and IP port translation are left empty by default. In this case, neither of them takes effect.
- Dedicated tunnels support BGP routing and static routing.
- Note the following limits for delivering routes:
 To improve the fine-grained scheduling capability of your network, do not publish the following routes:
`9.0.0.0/8`, `10.0.0.0/8`, `11.0.0.0/8`, `30.0.0.0/8`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12`, and `192.168.0.0/16`.
>! The direct connect gateway will directly reject large IP ranges.
>
 You can split the above large routes as follows for distribution:
  - <strong>`9.0.0.0/8`</strong>
Split as: `9.0.0.0/9` + `9.128.0.0/9`
 - <strong>`10.0.0.0/8`</strong>
Split as: `10.0.0.0/9` + `10.128.0.0/9`
 - <strong>`11.0.0.0/8`</strong>
Split as: `11.0.0.0/9` + `11.128.0.0/9`
 - <strong>`30.0.0.0/8`</strong>
Split as: `30.0.0.0/9` + `30.128.0.0/9`
 - <strong>`100.64.0.0/10`</strong>
Split as: `100.64.0.0/11` + `100.96.0.0/11`
 - <strong>`131.87.0.0/16`</strong>
Split as: `131.87.0.0/17` + `131.87.128.0/17`
 - <strong>`172.16.0.0/12`</strong>
Split as: `172.16.0.0/13` + `172.24.0.0/13`
 - <strong>`192.168.0.0/16 `</strong>
Split as: `192.168.0.0/17` + `192.168.128.0/17`

### IP translation
- IP address pools cannot fall within the CIDR block of the VPC in which the direct connect gateway resides.
- ACL rules for multiple IP address pools should not overlap. Otherwise, this will cause network address translation conflicts.
- IPs among multiple IP address pools cannot overlap.
- IP address pools only support a single IP or IP ranges, and `/24` IP ranges should be consistent. For example, `192.168.0.1 - 192.168.0.6` is supported, but `192.168.0.1 - 192.168.1.2` is not.
- Address pools should not contain the broadcast address (`255.255.255.255`), Class D addresses (`224.0.0.0 - 239.255.255.255`), or Class E addresses (`240.0.0.0 - 255.255.255.254`).
- Local source IP port translation supports up to 100 IP address pools, each supporting up to 20 ACL rules. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the quota if needed.
- To switch from IP translation to IP port translation, remove the original IP translation rules and refresh the page to edit the IP port translation rules.

### IP port translation
- The source IP must fall within the CIDR range of the VPC in which the Direct Connect gateway resides.
- The source IP port must be unique. In other words, an IP port in a VPC can only be mapped to one IP port.
- The mapped IP port cannot fall within the CIDR range of the VPC.
- The mapped IP port must be unique. In other words, multiple IP ports in a VPC cannot be mapped to one IP port.
- Original IPs and mapped IPs do not support the broadcast address (`255.255.255.255`), Class D addresses (`224.0.0.0 - 239.255.255.255`), and Class E addresses (`240.0.0.0 - 255.255.255.254`).
- Local destination IP port translation supports up to 100 IP port mappings. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the quota if needed.
- If both IP translation and IP port translation are configured, IP translation takes priority when both are hit.

## Network Limits
Before using connections to connect CPE and Tencent Cloud, check that the MAC addresses of both parties meet the following requirements to ensure proper network connection.

### MAC
The Tencent Cloud access exchange uses a fixed MAC address of 3c:fd:fe:29:cb:c2. This MAC address cannot be used by the CPE access device. Otherwise, the MAC address conflict will cause MAC address flapping (switching jump), which leads to network problems such as unreachable networks, slow response, and no response.
>?MAC address flapping (switching jump) occurs when a MAC address is learned by two outbound interfaces in the same VLAN and the MAC address entry learned later overrides the earlier one, making the MAC address unstable.

The following are scenarios where MAC address flapping occurs.
![]()
As shown in the figure above, CPE exchange B connects to Tencent Cloud exchanges A and A1 through two connections (connections 1 and 2).
MAC address flapping occurs in exchange B when Tencent Cloud returns packets to the CPE.

### VRRP
Currently, Tencent Cloud Direct Connect does not allow CPE to interconnect with Tencent Cloud via VRRP.

### Access Limits
To prevent network congestion due to network loops, you are advised to use layer-3 network sub-interfaces to connect to Tencent Cloud Direct Connect devices.
