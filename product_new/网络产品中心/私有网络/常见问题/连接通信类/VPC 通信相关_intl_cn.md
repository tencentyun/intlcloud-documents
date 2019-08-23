### 云服务器/数据库如何内网通信？
VPC 中云服务器与数据库的内网通信在网络层面均为内网 IP 通信，因此无差异。内网 IP 不同场景的通信方式如下：

| 通信场景 | 通信方案 |
|---------------|------------|
| 不同地域 | 不同地域的云服务器或数据库属于不同 VPC，通过对等连接/ [云联网](https://intl.cloud.tencent.com/document/product/1003/30056) （同/跨账号均支持）通信 |
| 不同可用区 | 同 VPC： 默认互通<br>不同 VPC： 通过对等连接 / [云联网](https://intl.cloud.tencent.com/document/product/1003/30056) （同/跨账号均支持）通信 |
| 不同VPC | 通过对等连接/ [云联网](https://intl.cloud.tencent.com/document/product/1003/30056) （同/跨账号均支持）通信 |
| 不同子网 | 同 VPC：默认互通<br>不同 VPC： 通过对等连接/ [云联网](https://intl.cloud.tencent.com/document/product/1003/30056) （同/跨账号均支持）通信 |
| 跨账号 | 跨账号 通过对等连接/ [云联网](https://intl.cloud.tencent.com/document/product/1003/30056) （同/跨地域均支持）通信 |

>同 VPC 下不同子网间（不论是否在同一可用区），**内网默认互通**，如果不通，请优先排查 [安全组](http://intl.cloud.tencent.com/document/product/213/12452) 及 [网络 ACL](https://intl.cloud.tencent.com/document/product/215/5132) 等防火墙策略。

### VPC 如何与基础网络、公网、其他 VPC、数据中心等通信？
| 通信类型 | 通信方法 |
|---------------|------------|
| VPC 与基础网络内云服务器通信 | [基础网络互通](https://intl.cloud.tencent.com/document/product/215/5002)|
| 访问公网 | NAT 网关 / [弹性公网 IP](https://intl.cloud.tencent.com/document/product/215/4958) / [公网网关](https://intl.cloud.tencent.com/document/product/215/4972) |
| 与其他 VPC 通信 | 对等连接 / [云联网](https://intl.cloud.tencent.com/document/product/1003) （同/跨账号均支持） |
| 连接数据中心 | VPN 连接 / [专线接入](https://intl.cloud.tencent.com/document/product/216) / [云联网](https://intl.cloud.tencent.com/document/product/1003) |


### 如何处理因 VPC 网段冲突而无法建立对等连接的问题？
建立对等连接时，要求两端 VPC 的 CIDR 不可以重叠，否则无法建立对等连接。

- 如果您两端 VPC 中，需要通信的子网网段不重叠，可以使用 [云联网](https://intl.cloud.tencent.com/product/ccn) 来实现通信。云联网可以将 VPC 通信时的网段限制缩小到子网层面。
例如，您需要通信的两个 VPC 网段均为 `10.0.0.0/16`，但子网分别为 `10.0.0.1/24` 和 `10.0.0.2/24`，则可以通过云联网实现通信。详情请参见 [云联网产品文档](https://intl.cloud.tencent.com/document/product/1003)。
- 如果云联网仍不能满足您的需求，则需要将重叠子网内的资源进行迁移。
    - 云服务器更换子网，详情请参见 [更换实例子网](http://intl.cloud.tencent.com/document/product/213/16565)。
    
 >在进行迁移前，请仔细阅读相关文档。

### 若 VPC1 分别和 VPC2、VPC3 建立了对等连接，那 VPC2 和 VPC3 能互通吗？
不能，对等连接能使 VPC 两两建立互联，但是这种互通关系不发生传递。即当 VPC1 与 VPC2 建立了对等连接，VPC1 和 VPC3 也建立了对等连接时，由于对等连接的不传递性，VPC2 和 VPC3 的流量不能互通。

