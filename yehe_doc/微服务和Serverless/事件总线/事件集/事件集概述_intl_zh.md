事件集负责接收来自事件源的事件，事件集绑定具体的事件规则后即可正常使用。本文为您介绍如下事件集涉及的类型。



事件总线 EventBridge 的事件集包括以下类型：

- 云服务事件集：即 default 事件集，默认创建在**广州**。腾讯云服务产生的 [云监控事件](https://intl.cloud.tencent.com/document/product/1108/46252) 及 [云审计事件](https://intl.cloud.tencent.com/document/product/1108/46246) 会自动发布到该事件集，不支持用户手动创建、删除。
- 自定义事件集：需要您自行创建并管理的事件总线，用于接收您自己的应用程序的事件。您自己的应用程序的事件只能发布到自定义总线。

为保证每条事件投递链路的可观测性，您可以在创建事件集的同时开启 [链路追踪](https://intl.cloud.tencent.com/document/product/1108/46990) 功能。
