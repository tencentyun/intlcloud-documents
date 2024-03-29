
### Prometheus 监控服务是否支持自定义上报数据？[](id:question2)

支持，Prometheus 监控服务支持多种语言自定义上报指标监控数据，并展示在集成的 Grafana 大盘中。


### Prometheus 监控服务的监控数据是怎么采集的？

通过 prometheus agent 拉取，也支持通过 pushgateway 方式写入。完全兼容开源 prometheus 采集方式。

### 每个实例都是一个单独的 exporter 么？

目前社区中 MySQL，Kafka 这种是一个实例一个 exporter，Redis是支持一个 exporter 多实例的。


### Prometheus 监控服务和自建有什么区别吗？

TMP 完全兼容开源生态，并与腾讯云监控数据打通，帮助用户快速搭建监控体系（自定义监控，组件监控，基础监控等），支持 Grafana 并预设了常用的监控 Dashboard，支持丰富的 Exporter 并预设了常见的告警模板；很好解决了开源社区 Prometheus 高可用搭建困难， Prometheus 性能可扩展性差，运维消耗人力等痛点。

### Prometheus支持哪些云产品？

云服务器、云数据库 MongoDB、云数据库 MySQL、云数据库 PostgreSQL、云数据库 Redis、ElasticSearch、容器服务等。详情请参见 [集成中心](https://intl.cloud.tencent.com/document/product/1116/43163)。


### 可以在 Prometheus 监控服务的 Grafana 界面集成其他数据源吗？
Prometheus 监控服务不支持其他数据源，建议使用 [腾讯云 Grafana 可视化服务](https://www.tencentcloud.com/document/product/1124)集成其它数据源。


### 支持通过 Promethues  pull 模式拉取监控数据吗？

暂不支持，只能通过API拉取。详情请参见 [监控数据查询](https://intl.cloud.tencent.com/document/product/1116/43212)。

### Prometheus 监控按量付费版本 Series 存储的限制是？
每个实例的 Series 限制最大为 450万，如需调整可以 [提交工单](https://console.intl.cloud.tencent.com/workorder/category)，在资源充足的情况下，我们将会为您合理地调整相关限制。

### Prometheus 监控服务支持接入 EKS 集群吗?
支持，按量计费版本支持标准集群、弹性集群（EKS）、边缘集群、注册集群。

