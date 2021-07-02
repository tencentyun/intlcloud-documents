## Resource Limits
| Resource | Limit | Higher quota allowed | Description |
|-------|-------|------------------|------------------|
| Connections per user | 10 | Yes | Each user can access up to 10 connections. |
| Dedicated tunnels per connection | 5 | Yes | Up to 5 dedicated tunnels can be created in a connection. |
| Direct connect gateway per VPC | 2 (one standard and the other supports NAT) | No | Each VPC supports up to two direct connect gateways. |
| Local IP translations per direct connect gateway | 100 | Yes | Each direct connect gateway supports up to 100 local IP translations. |
| Peer IP translations per direct connect gateway | 100 | Yes | Each direct connect gateway supports up to 100 peer IP translations. |
| Local source IP port translations per direct connect gateway | 20 | Yes | Each direct connect gateway supports up to 20 local source IP port translations. |
| Local destination IP port translations per direct connect gateway | 100 | Yes | Each direct connect gateway supports up to 100 local destination IP port translations. |
| Number of static routes per dedicated tunnel | 20    | No   | A dedicated tunnel supports up to 20 static routes. |
| Number of BGP routes per dedicated tunnel | 100 | No   |A dedicated tunnel supports up to 100 BGP routes. |

## Access Limits
### Direct Connect
- When a direct connect gateway is created, the IP translation and IP port translation are not configured by default. In this case, neither of them takes effect.
- Dedicated tunnels support BGP and static routes.
- Note the following limits for routing distribution:
 To improve the fine-grained scheduling capability of your network, do not publish the following routes:
`9.0.0.0/8`, `10.0.0.0/8`, `11.0.0.0/8`, `30.0.0.0/8`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12`, and `192.168.0.0/16`.
>! The direct connect gateway will directly reject large IP ranges.
 >
 You can split the above large routes as follows for distribution:
  - <strong>`9.0.0.0/8`</strong>
is split into `9.0.0.0/9` + `9.128.0.0/9`.
 - <strong>`10.0.0.0/8`</strong>
is split into `10.0.0.0/9` + `10.128.0.0/9`.
 - <strong>`11.0.0.0/8`</strong>
is split into `11.0.0.0/9` + `11.128.0.0/9`.
 - <strong>`30.0.0.0/8`</strong>
is split into `30.0.0.0/9` + `30.128.0.0/9`.
 - <strong>`100.64.0.0/10`</strong>
is split into `100.64.0.0/11` + `100.96.0.0/11`.
 - <strong>`131.87.0.0/16`</strong>
is split into `131.87.0.0/17` + `131.87.128.0/17`.
 - <strong>`172.16.0.0/12`</strong>
is split into `172.16.0.0/13` + `172.24.0.0/13`.
 - <strong>`192.168.0.0/16 `</strong>
is split into `192.168.0.0/17` + `192.168.128.0/17`.

### IP translation
- IP address pools cannot fall within the CIDR block of the VPC in which the direct connect gateway resides.
- ACL rules for multiple IP address pools should not overlap. Otherwise, this will cause network address translation conflicts.
- IP address pools cannot contain overlapping IP addresses.
- IP address pools only support a single IP or IP ranges, and `/24` IP ranges should be consistent. For example, `192.168.0.1 - 192.168.0.6` is supported, but `192.168.0.1 - 192.168.1.2` is not.
- Address pools should not contain the broadcast address (`255.255.255.255`), Class D addresses (`224.0.0.0 - 239.255.255.255`), or Class E addresses (`240.0.0.0 - 255.255.255.254`).
- Local source IP port translation supports up to 100 IP address pools, each supporting up to 20 ACL rules. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the quota if needed.
- To switch from IP translation to IP port translation, remove the original IP translation rules and refresh the page to edit the IP port translation rules.

### IP port translation
- The original IP must fall within the CIDR block of the VPC in which the direct connect gateway resides.
- The original IP port must be unique. In other words, an IP port in a VPC can only be mapped to one IP port.
- The mapped IP port cannot fall within the CIDR block of the VPC.
- The mapped IP port must be unique. In other words, multiple IP ports in a VPC cannot be mapped to one IP port.
- Original IPs and mapped IPs do not support the broadcast address (`255.255.255.255`), Class D addresses (`224.0.0.0 - 239.255.255.255`), and Class E addresses (`240.0.0.0 - 255.255.255.254`).
- Local destination IP port translation supports up to 100 IP port mappings. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the quota if needed.
- If both IP translation and IP port translation are configured, IP translation takes priority when both are hit.
