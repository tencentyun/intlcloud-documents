### 云数据库 Redis 集群版的 hash 算法如何使用？
Redis 集群版的 hash 算法同社区 Redis Cluster 一致，HASH_SLOT = CRC16(key) mod 16384，参考 [官方文档](https://redis.io/topics/cluster-spec)。

### 单实例最高支持多大容量？

| 版本 | 规格范围 |
|--|--|
| 内存版（标准架构） | 0.25GB - 64GB  |
| 内存版（集群架构） | 2GB - 8TB  |
| CKV 版（标准架构） | 4GB - 384GB  |
| CKV 版（集群架构） | 12GB - 48TB  |

### 数据保存在云数据库 Redis 是否可靠？
Redis 标准架构（0副本）不提供高可用，其他版本 Redis 均为主从复制结构，数据热备加上每日冷备的方式，可保障数据可靠性。

### 云数据库 Redis 采用哪种持久化方式？
云数据库 Redis 后端由备份集群完成全量和增量备份工作，持久化在备机执行，对线上业务几乎无影响。

### 为什么刚购买成功，存储容量就占用了2M？
云数据库 Redis 系统维持自身数据结构所用。

### 云数据库 Redis 可以用可视化工具管理吗，例如 Redis Desktop Manager？
云数据库 Redis 控制台可以进行运维管理操作，如果还需使用可视化工具，可通过 CVM 做跳板机对外提供链接地址给 Redis Desktop Manager 访问。

### 扩容和缩容，会中断业务吗？
Redis 各版本扩容和缩容闪断情况如下：
- 垂直方向扩容时，若所扩容量已超出单机剩余容量，则集群会进行分片或迁移节点，此时有秒级业务闪断，若所扩容量未超出单机剩余容量，则不会出现闪断。
- 水平方向扩容时，集群是增加节点数量，存在秒级业务闪断。
- 水平方向缩容时，回收节点会让集群中的节点发生迁移，存在秒级业务中断。
- 垂直方向缩容不会出现秒级业务闪断。

### 如何添加监控报警？
可通过自定义监控告警实现，请参见 [监控告警](https://intl.cloud.tencent.com/document/product/239/34589)。

### select 0-15 需要申请不同的实例么?
不需要。标准架构和集群架构均可以设置多个库。

### Redis 是否支持 Lua 功能？
- Redis 内存版（标准架构）的实例，2018年9月1日之前的购买的，默认不开通 Lua 功能，需 [提交工单](https://console.cloud.tencent.com/workorder/category
) 申请开通，之后购买的实例默认开通 Lua 功能。
- Redis 内存版（集群架构）、CKV 版（标准架构）、CKV 版（集群架构）默认开通 Lua 功能。

### 云数据库 Redis 支持缓存失效订阅事件吗？
支持。

### 账号误删与忘记密码怎么办？
- 若误删帐号，可登录  [Redis 控制台](https://console.cloud.tencent.com/redis) 单击实例 ID 进入实例管理页面，选择**账号管理**>**创建账号**进行新建账号。
- 若忘记默认账号密码，可通过**账号管理**页找到对应账号进行**重置密码**操作。

### 云数据库 Redis 从节点与主节点数据不同步？
云数据库 Redis 主节点的更新会自动复制到其关联的从节点。鉴于 Redis 的异步复制技术，从节点更新可能会落后于其主节点。可能原因如下：
- 主节点的 I/O 写入量超过了从节点同步的速度。
- 主节点和从节点之间有网络延迟。

### 如何检测云数据库 Redis 端口连通性？
您可以使用 telnet 命令来检测 Redis 端口的连通性。

### 如何设置云数据库 Redis 缓存策略？
登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表单击实例 ID，进入参数配置页面，通过 maxmemory-policy 参数来配置缓存策略，参数默认值为 noeviction。

### 如何下载云数据库 Redis 的客户端？
兼容 Redis 协议的客户端均可访问云数据库 Redis，您可以根据需求选择对应 Redis 客户端，下载地址请参见 [官方网站](http://redis.io/clients?spm=a2c4g.11186623.2.5.c3a25c83nYgvqS)。

### 如何升级云数据库 Redis 版本？
登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表单击实例 ID，进入实例详情页面可升级实例版本，详情请参见 [升级实例版本](https://intl.cloud.tencent.com/document/product/239/37710)。

### 如何升级云数据库 Redis 架构？
登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表单击实例 ID，进入实例详情页面可升级实例架构，详情请参见 [升级实例架构](https://intl.cloud.tencent.com/document/product/239/37860)。
