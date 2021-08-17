本文为您介绍如何通过 Redis 控制台配置多可用区和查看多可用区。

## 操作场景
云数据库 Redis 支持同地域下跨多个 [可用区部署副本](https://intl.cloud.tencent.com/document/product/239/39812)，相对单可用区实例（主节点和副本节点在同一可用区），多可用区实例具有更高的可用性和容灾能力。
- 未开启副本只读（读写分离）的实例，读写请求都会经过本可用区的 Proxy 路由到主节点，保障数据的一致性，同时保障最多仅有一次的跨 AZ（Available Zone）访问。
- 开启副本只读（读写分离）的实例，写请求将路由到主节点，读请求将路由到本可用区的副本节点，满足业务就近访问的诉求。

推荐采用一主两副本，主 AZ 一主一副本，副本 AZ 一个副本，这种部署模式可以最大限度保障业务的可用性，及降低主机故障带来的延迟影响，因为在主 AZ 部署一个副本，主节点故障后，主可用区有一个副本可以优先选主，保障主可用区的访问延迟不会因为主节点切换到备可用区而受到影响。

>?目前仅云数据库 Redis 4.0 标准架构、集群架构和 Redis 5.0 标准架构、集群架构支持多可用区。


## 操作步骤
### 选择多可用区
1. 登录 [Redis 购买页](https://buy.cloud.tencent.com/redis)，选择地域、可用区、副本等相关配置，单击【立即购买】。
 - 副本数量：副本数决定最大可用区数量，最大可用区数量 = 副本数 + 1。
 - 可用区：同地域下 Redis 节点部署的不同可用区，最大支持部署到6个可用区。
![](https://main.qcloudimg.com/raw/d76a6c8cc996b58c8f5df1a17102111c.png)
2. 支付完成后，返回实例列表，待实例状态变为“运行中”，即可进行后续操作。

### 查看多可用区
- 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表的“可用区”列，带有“M”标志的实例即为多可用区实例，且可查看多可用区信息。
![](https://main.qcloudimg.com/raw/5c553bf4c0817c0dbddb662405078fe7.png)
- 在 [实例列表](https://console.cloud.tencent.com/redis)，单击实例 ID 进入管理页面，在详情页的“可用区”处带有“M”标志的实例即为多可用区实例，且可查看多可用区信息。
![](https://main.qcloudimg.com/raw/d579e1ab309c754ef0ea56904ad5f194.png)
- 在 [实例列表](https://console.cloud.tencent.com/redis)，单击实例 ID 进入管理页面，在节点管理页，可查看各节点的详细信息，及调整节点配置。
![](https://main.qcloudimg.com/raw/aa0adb39b9bfb543051ca6bdfda78664.png)
