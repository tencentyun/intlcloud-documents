## Resource Limits
| Resource | Limit | Higher quota allowed |
|-------|-------|------------------|
| Connections per user | 10 | Yes |
| Dedicated tunnels per connection | 5 | Yes |
| Direct Connect gateway per VPC | 1 | No |
| Local IP translations per Direct Connect gateway | 100 | Yes |
| Peer IP translations per Direct Connect gateway | 100 | Yes |
| IPs for local source IP port translation per Direct Connect gateway | 20 | Yes |
| Local destination IP port translations per Direct Connect gateway | 100 | Yes |
| Number of static routes per dedicated tunnel | 20 | No |
| Number of BGP routes per dedicated tunnel | 100 | No |

## Access Limits
### Direct Connect
- When a Direct Connect gateway is created, the content of IP translation and IP port translation are left empty by default. In this case, neither of them takes effect.
- Dedicated tunnels support BPG routing and static routing.
- Note the following limits for routing distribution:
 To ensure the fine-grained scheduling capability of your network, do not publish the following routes:
`9.0.0.0/8`, `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12`, `192.168.0.0/16`.
>!If a large IP range route is published, the direct connect gateway will directly reject it.
 
 You can split the above routes as follows for distribution:
  - <strong>`9.0.0.0/8`</strong>
should be split into `9.0.0.0/9` + `9.128.0.0/9`.
 - <strong>`10.0.0.0/8`</strong>
should be split into `10.0.0.0/9` + `10.128.0.0/9`.
 - <strong>`172.16.0.0/12`</strong>
should be split into `172.16.0.0/13` + `172.24.0.0/13`.
 - <strong>`192.168.0.0/16`</strong>
should be split into `192.168.0.0/17` + `192.168.128.0/17`.
 - <strong>`100.64.0.0/10`</strong>
should be split into `100.64.0.0/11` + `100.96.0.0/11`.
 - <strong>`131.87.0.0/16`</strong>
should be split into `131.87.0.0/17` + `131.87.128.0/17`.
 - <strong>`172.16.0.0/12`</strong>
should be split into `172.16.0.0/13` + `172.24.0.0/13`.
 - <strong>`192.168.0.0/16 `</strong>
should be split into `192.168.0.0/17` + `192.168.128.0/17`.

### IP translation
- IP address pools cannot fall within the CIDR range of the VPC in which the Direct Connect gateway resides.
- ACL rules for multiple IP address pools should not overlap. Otherwise, this will cause network address translation conflicts.
- IP address pools cannot not contain overlapping IP addresses.
- IP address pools only support single IP or IP ranges. `/24` IP ranges should be consistent. For example, `192.168.0.1 - 192.168.0.6` is supported, but `192.168.0.1 - 192.168.1.2` is not.
- Address pools should not contain the broadcast address (`255.255.255.255`), Class D addresses (`224.0.0.0 - 239.255.255.255`), or Class E addresses (`240.0.0.0 - 255.255.255.254`).
- Local source IP port translation supports up to 100 IP address pools, each supporting up to 20 ACL rules. Your can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to request quota increases if needed.
- To switch from IP translation to IP port translation, remove the original IP translation rules and refresh the page to edit the IP port translation rules.

### IP port translation
- The original IP must fall within the CIDR range of the VPC in which the Direct Connect gateway resides.
- The original IP port must be unique. In other words, an IP port in a VPC can only be mapped to one IP port.
- The mapped IP port cannot fall within the CIDR range of the VPC.
- The mapped IP port must be unique. In other words, multiple IP ports in a VPC cannot be mapped to one IP port.
- Original IPs and mapped IPs do not support the broadcast address (`255.255.255.255`), Class D addresses (`224.0.0.0 - 239.255.255.255`), and Class E addresses (`240.0.0.0 - 255.255.255.254`).
- Local destination IP port translation supports up to 100 IP port mappings. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to request quota increases if needed.
- If both IP translation and IP port translation are configured, IP translation takes priority when both are hit.
