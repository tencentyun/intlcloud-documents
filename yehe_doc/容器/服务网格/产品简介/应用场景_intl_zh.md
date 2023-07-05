## 变更发布

基于 TCM 在南北向与东西向流量控制能力，无需业务改造感知，可轻松配置实现服务和 API 级别的上下线发布、版本定义/灰度、特征路由、负载均衡策略等控制，提升发布变更的效率与可控性。

![](https://qcloudimg.tencent-cloud.cn/raw/eb73f0b31b3af37a437b7be9c19f4632.png)

## 多层级观测

无侵入获取应用通信的 Metric，Trace，Access log 遥测数据，支撑构建多层级的观测能力。覆盖应用通信性能实时监控，全链路调用追踪与链路分析，流量接入的 downstream 分析与代理转发访问行为回溯，量化应用通信的性能和质量。
![](https://qcloudimg.tencent-cloud.cn/raw/254a290424701deb474e492c24fda5ca.png)

## 分布式高可用架构

提升应用通信与应用架构的可用性，使用重试、超时、连接池管理、健康检查和限流等机制，控制和保障应用间的通信容错；在同城双活，两地三中心的应用分布部署架构下，通过地域/故障感知调度能力，实现自动化的 failover 与可控的 distribute 多集群流量调度，灵活实现 DNS/Ingress/Service 三级容灾管理。

![](https://qcloudimg.tencent-cloud.cn/raw/b8c6f5de8b8a10f9c3a673723e1d3a74.png)

## 安全隔离

以 service-based 的认证与授权机制，在容器化动态 IP 场景下，实现可控的服务认证与访问控制管理。支持 JWT 请求身份认证，自动 mTLS 实现零信任网络，与基于身份与流量特征限制访问权限。

![](https://qcloudimg.tencent-cloud.cn/raw/08602ea644783acb89325d7016ab3405.png)

