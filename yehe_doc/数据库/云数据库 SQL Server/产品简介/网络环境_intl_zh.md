云数据库 SQL Server 支持私有网络环境。

## 网络限制
- 不同地域之间的网络完全隔离，不同地域之间的云产品**默认不能通过内网通信**。
- 处于不同私有网络的云产品，可以通过 [云联网](https://www.tencentcloud.com/document/product/1003) 进行通信，此通信方式较为高速、稳定。
- [负载均衡](https://www.tencentcloud.com/document/product/214) 当前默认支持同地域流量转发，绑定本地域的云数据库。如果开通 [跨地域绑定](https://intl.cloud.tencent.com/document/product/214/38441) 功能，则可支持负载均衡跨地域绑定云数据库。
- 云数据库 SQL Server 尚未开放实例的外网 IP，有需求的用户可以利用 SSH2 的端口映射在外网连接实例，并对其进行配置和管理，请参见 [连接实例](https://intl.cloud.tencent.com/document/product/238/11627)。
- 选购云数据库 SQL Server 时，建议选择与云服务器相同的地域，可降低访问延迟。


## 网络连通性检测
可通过 [云数据库 SQL Server 购买页](https://buy.cloud.tencent.com/sqlserver#/) 中提供的网络连通性检测工具，检查已选择的地域/可用区和网络类型中，是否存在可与云数据库 SQL Server 内网连通的云服务器。
![](https://main.qcloudimg.com/raw/d1bca3859d60633ed0fb5669c88daf13.png)
单击**查看详情**可查看内网可连通的云服务器相关信息，包括 ID/实例名、可用区、配置（CPU、内存、磁盘、网络）、主IP地址，并且提供搜索功能，帮助用户快速判断可与云数据库 SQL Server 内网连通的云服务器。
![](https://main.qcloudimg.com/raw/8c76d06d19734b7fe8f85ba2f14b64a1.png)
