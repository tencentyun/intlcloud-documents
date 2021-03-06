
### 云数据库 Redis 连接失败，如何处理？
>?
>- 使用的云服务器 CVM 访问云数据库的内网地址时，云服务器和数据库须是同一账号，且同一个 VPC 内（保障同一个地域），或同在基础网络内。
>- 对于不同的 VPC 下（包括同账号/不同账号，同地域/不同地域）的云服务器和数据库，内网连接方式请参见 [对等连接](https://intl.cloud.tencent.com/document/product/553/18827)。
>- Redis 暂不支持外网地址，如需通过外网地址连接实例，可参见 [iptable 转发](https://intl.cloud.tencent.com/document/product/239/35905)。
>
连接失败常见原因如下：
- Redis 与 CVM 不在同一账号下。建议云服务器与数据库是同一账号，且同一个 VPC 内（保障同一个地域）。
- Redis 与 CVM 不在相同地域。建议云服务器与数据库是同一账号，且同一个 VPC 内（保障同一个地域）。
- Redis 与 CVM 的 VPC 不同。请参见 [配置网络](https://intl.cloud.tencent.com/document/product/239/31944) 更换网络。
- 云服务器的安全组规则阻塞了对 Redis 内网地址和端口的访问。请参见 [配置安全组](https://intl.cloud.tencent.com/document/product/239/31945) 修改安全组规则。

### 云服务器与云数据库部署在同一区域上，如何连接 Redis？
云服务器与云数据库部署在同一区域上时，使用内网访问，请参见 [连接数据库实例](https://intl.cloud.tencent.com/document/product/239/9897)。

### 云服务器与云数据库部署在不同区域上，如何连接 Redis？
基础网络和私有网络互通，请参见 [基础网络互通](https://intl.cloud.tencent.com/document/product/215/31807)。
私有网络之间互通，请参见 [对等连接](https://intl.cloud.tencent.com/document/product/553/18827)。

### 如何处理云数据库 Redis 无法 ping 通？ 
Redis 默认禁`ping`，可以使用 telnet 来检测连通性。

### 如何开通 Redis 的外网访问？ 
云数据库 Redis 暂时不支持外网地址。如需通过外网访问，可使用带有外网的云服务器通过 [Iptable 代理](https://intl.cloud.tencent.com/document/product/239/35905) 的方式来实现。
>?iptable 转发的方式存在稳定性风险，不建议在生产环境使用外网接入。

### 如何查看内网地址？
登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表查看，或单击实例 ID，进入实例详情页查看。

