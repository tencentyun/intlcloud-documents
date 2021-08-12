A route table consists of multiple routing policies that control the outbound traffic direction of subnets in the VPC. Each subnet can only be associated with one route table, while each route table can be associated with multiple subnets. You can create multiple route tables for subnets with different traffic routes.

## Types
There are two types of route tables: default and custom. 
- **Default route table**: when you create a VPC, the system automatically generates a default route table, which will be associated with subnets created later if no custom route table is selected. You cannot delete the default route table, but you can add, delete, and modify routing policies in it.
- **Custom route table**: you can create or delete a custom route table in the VPC. This custom route table can be associated with all the subnets to apply the same routing policy.
![](https://main.qcloudimg.com/raw/a86260ffb40bec52c9f64a307d956691.png)  
>?You can associate a route table when [creating a subnet](https://intl.cloud.tencent.com/document/product/215/31806), or [changing the route table](https://intl.cloud.tencent.com/document/product/215/40090) after a subnet is created.

## Routing Policy
A route table controls traffic routes by using routing policies. A routing policy consists of the destination, next-hop type, and next hop.
- **Destination**: specifies the destination IP range to which you want to forward traffic. It should be an IP range. If you want to enter a single IP address, set the mask to `32` (for example, `172.16.1.1/32`). The destination cannot be an IP range of the VPC where the route table resides, because the local route already allows private network interconnection in this VPC.
>?If you have deployed a [TKE service](https://intl.cloud.tencent.com/document/product/457/6759) in the VPC, the destination you configure in the routing policy of the VPC subnet cannot fall within the VPC CIDR block or contain the TKE IP range.
>For example, if the VPC CIDR block is `172.168.0.0/16` and the TKE CIDR block is `192.168.0.0/16`, the destination IP range cannot fall within `172.168.0.0/16`, or contain `192.168.0.0/16` when you configure routing policy for a VPC subnet.
- **Next-hop type**: indicates the egress of data packets for the VPC. The next-hop type of VPC supports **NAT Gateway**, **Peering connection**, **VPN gateway**, **Direct connect gateway**, **CVM**, and others.
- **Next hop**: specifies the next hop instance (identified by the next-hop ID) to which the traffic is forwarded, such as a NAT Gateway in a VPC.


### Routing policy priority
When there are multiple routing rules in a routing table, the following routing priority applies:
- Traffic within VPC: traffic within VPC is matched first.
- Exact match route (the longest prefix match): when there are multiple routes in the route table that can match the destination IP, the route with the longest (exact) mask is matched to determine the next hop.
- Public IP: if no routing policy is matched, a CVM instance can access the Internet through its public IP address.
**Use case:**
When a subnet is associated with a NAT Gateway, and the CVM in the subnet has a public IP (or EIP), the CVM accesses the Internet through the NAT Gateway by default (because the priority of the exact match route is higher than that of the public IP). However, you can set a routing policy to allow the CVM to access the Internet by using its public IP address. For details, see [Adjusting the Priorities of NAT Gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).

## 等价路由 
等价路由 ECMP（Equal-CostMultipathRouting），是指到达同一目的地址存在多条相同代价的不同路径。在数据包传输时，如果使用传统的路由技术，去往同一目的地址的数据包仅能利用其中一条路径，而其他路径处于备份或者无效状态，当一条路径故障时，切换路径也需要耗费一定的时间，而等价路由可以在网络环境下同时使用多条路径，不仅增加了传输带宽，也实现了多路径流量负载均衡和冗余链路备份的目的。

通常建议 ECMP 用于链路间差异不大的情况下，例如去往某目的地址配置了两条 ECMP 路径，路径 A 带宽为2Mbps，路径 B 带宽为3Mbps，那么网络总带宽可达到4Mbps，即增加了传输带宽，且 A 和 B 链路间可以实现流量负载；但如果路径 B 带宽为100Mbps，那么总网络带宽也只能达到 4Mbps，因此请根据业务实际情况，配置 ECMP 路由。

VPC支持部分同类型路由形成ECMP，不同类型间均不支持ECMP，情况如下：

| 下一跳类型     | 是否支持同类型形成 ECMP  | ECMP 支持的最大数量 |
| -------------- | ----------------------- | --------------------------- |
| NAT 网关        | 否                       | N/A                 |
| 云服务器公网 IP | 否                     | N/A                 |
| 云服务器       | 是                    | 同类型最多8个       |
| 对等连接       | 否                     | N/A                 |
| 专线网关       | 是                     | 同类型最多8个       |
| 云联网         | 否                     | N/A                 |
| 高可用虚拟 IP   | 是                    | 同类型最多8个       |
| VPN 网关        | 是                      | 同类型最多8个       |

### 应用场景
等价路由通常用于，当网关承载带宽有限时，可通过路由实现网关间的流量负载。例如某用户在云上 VPC 和云下 IDC 业务通信带宽需要2000Mbps，但目前 VPN 带宽最大为1000Mbps，那么可以创建两个1000Mbps规格的 VPN 网关，建立两条 VPN 隧道来实现流量分担，两条 VPN 链路可以满足总带宽达到2000Mbps的需求。

## 主备路由
主备路由是指去往同一目的地址配置了2条或多条路径，而只有1条路径处于活跃状态，其他路径则处于备用或无效状态。例如 VPC 去往某 IDC 配置了两条路由，即路径 A 和路径 B，数据包仅通过主路径 A 去往目的地址，路径 B 处于无效备用状态；当路径 A 发生链路故障时，可使能路径 B 生效，流量则从路径 A 切到路径 B，保证了业务的可用性，这种情况下称路径 A、B 为主备路由。

VPC 路由表在添加路由策略时，根据下一跳类型定义了不同的优先级，即去往同一目的端，可以配置下一跳为不同类型的网关，形成主备路由，再结合 VPC 网络探测功能，探测链路质量和可达性，通过配置告警及时发现链路异常，快速切换主备路由，以满足业务高可用。
>?
>+ 路由优先级功能目前处于内测中，如有需要，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category)。
>+ VPC 路由表中根据不同的下一跳类型定义了不同的优先级，目前默认路由优先级为：云联网 > 专线网关 > VPN 网关 > 其他。
>+ 暂不支持控制台修改优先级，如需调整，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category)。

VPC 不同类型路由支持主备情况如下：

| 下一跳类型         | 是否支持主备                                            |
| ------------------ | ------------------------------------------------------- |
| NAT 网关            | 否                                                      |
| 云服务器公网 IP     | 否                                                      |
| 云服务器           | 是，支持与云联网/VPN 网关/专线网关/高可用虚拟 IP 形成主备  |
| 对等连接（同地域） | 否                                                      |
| 对等连接（跨地域） | 否                                                      |
| 专线网关           | 是，支持与云联网/VPN 网关/高可用虚拟 IP/云服务器形成主备  |
| 云联网             | 是，支持与 VPN/专线网关/高可用虚拟 IP/云服务器形成主备    |
| 高可用虚拟 IP       | 是，支持与云联网/VPN 网关/专线网关/云服务器形成主备      |
| VPN 网关            | 是，支持与云联网/专线网关/高可用虚拟 IP/云服务器形成主备 |


### 应用场景
主备路由通常用于，当某一网关链路故障时，可通过主备路由实现流量的平滑切换。例如：
+ VPC 型专线网关（主）& VPC 型 VPN 网关（备）
  **场景描述**：用户通过 VPC 型专线网关打通云上 VPC 和自建 IDC 的通信，同时通过 VPN 网关创建 VPN 备用通道来实现 IDC 与 VPC 通信链路的备份。
  ![](https://main.qcloudimg.com/raw/6371959ca33fe42ac9dfc3c62529bb87.png)
+ 云联网型专线网关（主）& VPC 型 VPN 网关（备）
  **场景描述**：用户通过云联网型专线网关打通云上 VPC 和自建 IDC 的通信，同时通过 VPN 网关创建 VPN 备用通道来实现 IDC 与 VPC 通信链路的备份。
	![](https://main.qcloudimg.com/raw/92f84ee71e0a12212b95641bf76b5bee.png)
