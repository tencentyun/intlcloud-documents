## 什么是腾讯云事件总线？
腾讯云事件总线（EventBridge）是一款安全，稳定，高效的无服务器事件管理平台，作为流数据和事件的自动收集、处理、分发管道，通过可视化的配置，实现事件源（例如：Kakfa，审计，数据库等）和目标对象（例如：CLS，SCF等）的快速连接，当前 EventBridge 已接入一百多个云上服务，助力分布式事件驱动架构的快速构建。

## 产品架构

腾讯云 EventBridge 的产品架构如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/b7f41697d36193e37b5d1d89f387e143.png)

- [事件源](https://intl.cloud.tencent.com/document/product/1108/42274)：将腾讯云服务、自定义应用、SaaS 应用等应用程序产生的事件消息发布到事件集。
- [事件集](https://intl.cloud.tencent.com/document/product/1108/42284)：存储接收到的事件消息，并根据事件规则将事件消息路由到事件目标。
- 事件目标：消费事件消息。

## 产品功能
- 事件收集：提供标准事件投递接口，完成云产品事件、SaaS 服务、自定义应用事件等不同事件源的规范化接入。
- 事件管理：提供事件的可管理特性，通过格式匹配、内容筛选、格式转换、追踪、归档、重放等能力，为客户在事件驱动（EDA）架构下提供更多支持。
- 事件投递：支持多种类型投递目标接入，具有高可扩展能力，可基于实际业务场景提供不同解决方案。
