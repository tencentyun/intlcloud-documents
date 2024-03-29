

腾讯云容器服务（Tencent Kubernetes Engine，TKE）基于原生 Kubernetes 提供以容器为核心的解决方案，解决用户开发、测试及运维过程的环境问题、帮助用户降低成本，提高效率。而 Kubernetes 是一款由 Google 开发的开源的容器编排工具，在 Google 已使用超过15年。作为容器领域事实的标准，Kubernetes 可以极大的简化应用的管理和部署复杂度。通过与容器服务集成，可以大大简化用户通过 Prometheus 来监控 Kubernetes 状态及其运行在上面的服务。

## 主要内容

- Prometheus 在 Kubernetes 下的服务发现机制。
- 监控 Kubernetes 集群状态。
- 监控集群基础设施。
- 监控集群应用容器资源使用情况。
- 监控用户部署的应用程序。

## 基本概念

| 述语  | 说明  |
|--------|---------|
| Prometheus Operator | CoreOS 为简化 Kubernetes 操作，引入了 Operator 的概念，针对 Prometheus 推出了 Prometheus Operator，提供 Prometheus 相关自定义 Kubernetes 资源，方便操作 Prometheus |
| ServiceMonitor | 声明式的管理 Service 相关监控配置 |
| PodMonitor   | 声明式的管理 Pod 相关监控配置 |
| 服务发现   | Prometheus 提供了多种抓取任务的服务发现机制，例如基于文件、Consul 等 |

## 操作步骤

1. 登录 [ Prometheus 监控服务控制台](https://console.cloud.tencent.com/monitor/prometheus)。
2. 在实例列表中，选择需要操作的 Prometheus 实例，单击**实例 ID** 或者右侧的**管理**进入实例管理页面。
3. 在管理页面的左侧菜单**集成容器服务**进入容器集成页面，目前主要提供如下服务。
    - 安装 Agent。
    - 集成 Kubernetes 相关的基础监控。
    - 抓取任务状态及Agent 状态。
