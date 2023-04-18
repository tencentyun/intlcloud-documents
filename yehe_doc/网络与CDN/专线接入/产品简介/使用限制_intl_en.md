## Resource Limits
<table>
<tr>
<th>Resource</th>
<th>Constraints</th>
<th>Support Increasing Quota</th>
<th>Description</th>
</tr>
<tr>
<td>Connections per user</th>
<td>10</th>
<td>Yes</th>
<td>Each user can have up to 10 connections.</th>
</tr>
<tr>
<td>Dedicated tunnels per connection</th>
<td>5</th>
<td>Yes</th>
<td>Up to 5 dedicated tunnels can be created in each connection</th>
</tr>
<tr>
<td>DC gateways per VPC</th>
<td>2 (One standard gateway and one NAT gateway)</th>
<td>No</th>
<td>Up to 2 Direct Connect gateways can be configured in each VPC.</th>
</tr>
<tr>
<td>Local IP translations per DC gateway</th>
<td>100</th>
<td>Yes</th>
<td>Up to 100 local IP translations can be configured for each Direct Connect gateway.</th>
</tr>
<tr>
<td>Peer IP translations per DC gateway</th>
<td>100</th>
<td>Yes</th>
<td>Up to 100 peer IP translations can be configured for each Direct Connect gateway.</th>
</tr>
<tr>
<td>Local source IP port translations per DC gateway</th>
<td>20</th>
<td>Yes</th>
<td>Up to 20 local source IP port translations can be configured for each dedicated gateway.</th>
</tr>
<tr>
<td>Local destination IP port translations per DC gateway</th>
<td>100</th>
<td>Yes</th>
<td>Up to 100 local destination IP port translations can be configured for each Direct Connect gateway.</th>
</tr>
<tr>
<td rowspan="2">Static routes per dedicated tunnel</th>
<td>Dedicated tunnel 1.0: 20</th>
<td>No</th>
<td>Up to 20 static routes can be configured for a dedicated tunnel 1.0.</th>
</tr>
<tr>
<td>Dedicated tunnel 2.0: 50</th>
<td>Yes</th>
<td>Up to 50 static routes can be configured for a dedicated tunnel 2.0. To adjust the quota, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</th>
</tr>
<tr>
<td rowspan="2">BGP routes per dedicated tunnel</th>
<td>Dedicated tunnel 1.0: 100</th>
<td>No</th>
<td>Up to 100 BGP routes can be configured for a dedicated tunnel 1.0.</th>
</tr>
<tr>
<td>Dedicated tunnel 2.0: 100</th>
<td>Yes </th>
<td>Up to 100 BGP routes can be configured for a dedicated tunnel 2.0. To adjust the quota, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</th>
</tr>
</table>


## Access Limits

### Direct Connect
- When a Direct Connect gateway is created, the content of IP translation and IP port translation are left empty by default. In this case, neither of them takes effect.
- Dedicated tunnels support BGP routing and static routing.
- Note the following limits for delivering routes:
 To improve the fine-grained scheduling capability of your network, do not publish the following routes:
  **Dedicated tunnel 1.0**
  `9.0.0.0/8`, `10.0.0.0/8`, `11.0.0.0/8`, `30.0.0.0/8`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12`, and `192.168.0.0/16`.
>! The direct connect gateway will directly reject large IP ranges.
>
 You can split the above large routes as follows for distribution:
  - <strong>`9.0.0.0/8`</strong>
Split as: `9.0.0.0/9` + `9.128.0.0/9`
 - <strong>`10.0.0.0/8`</strong>
Split into `10.0.0.0/9` + `10.128.0.0/9`.
 - <strong>`11.0.0.0/8`</strong>
Split into `11.0.0.0/9` + `11.128.0.0/9`.
 - <strong>`30.0.0.0/8`</strong>
Split into `30.0.0.0/9` + `30.128.0.0/9`.
 - <strong>`100.64.0.0/10`</strong>
Split into `100.64.0.0/11` + `100.96.0.0/11`.
 - <strong>`131.87.0.0/16`</strong>
Split into `131.87.0.0/17` + `131.87.128.0/17`.
 - <strong>`172.16.0.0/12`</strong>
Split into `172.16.0.0/13` + `172.24.0.0/13`.
 - <strong>`192.168.0.0/16 `</strong>
Split into `192.168.0.0/17` + `192.168.128.0/17`.

 **Dedicated tunnel 2.0**
 - `127.0.0.0/8`, `224.0.0.0/4`, `240.0.0.0/4`, `255.255.255.255`, and `169.254.0.0/16` (excluding `169.254.64.0.0/23`).
 Subnets and other IP addresses in the same network segment. To allow mutual access, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to enable peer IP redistribution.



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
To establish a connection between the cusotmer IDC and Tencent Cloud, check that the MAC addresses of both parties meet the following requirements.

### MAC
The Tencent Cloud access exchange uses a fixed MAC address of 3c:fd:fe:29:cb:c2. This MAC address cannot be used by the customer IDC access device. Otherwise, the MAC address conflict will cause MAC address flapping (switching jump), which leads to network problems such as unreachable networks, slow response, and no response.
>?MAC address flapping (switching jump) occurs when a MAC address is learned by two outbound interfaces in the same VLAN and the MAC address entry learned later overrides the earlier one, making the MAC address unstable.

The following are scenarios where MAC address flapping occurs.
![](https://qcloudimg.tencent-cloud.cn/raw/17260e52033989f2c1dc743dbe2b3382.png)
As shown in the figure above, customer exchange B connects to Tencent Cloud exchanges A and A1 through two connections (connections 1 and 2).
MAC address flapping occurs in exchange B when Tencent Cloud returns packets to the customer IDC.


### Access Limits
To prevent network congestion due to network loops, you are advised to use layer-3 network sub-interfaces to connect to Tencent Cloud Direct Connect devices.
