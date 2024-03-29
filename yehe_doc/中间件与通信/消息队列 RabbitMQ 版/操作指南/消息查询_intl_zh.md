## 操作场景

当您需要查看某条消息的具体内容或具体参数时，可以使用 TDMQ RabbitMQ 版控制台的消息查询功能，根据时间段查某一批消息或者根据消息 ID 精确查询某条消息的生产记录，找到生产记录后可以进一步查看这条消息的消息体内容和消息参数。

## 查询限制

- 消息查询最多可以查询近3天的消息。
- 一次性最多可以查询65536条消息。

## 前提条件

已经参考 [SDK 文档](https://intl.cloud.tencent.com/document/product/1113/43132) 部署好生产端和消费端服务，并在3天内有消息生产和消费。

## 操作步骤

1. 登录 [TDMQ RabbitMQ 控制台](https://console.cloud.tencent.com/tdmq/rabbit-cluster) ，在左侧导航栏单击**消息查询**。
2. 在消息查询页面，首先选择好地域，再选择需要查询的时间范围，分别勾选要查询消息的 Vhost 与 Queue，如果您知道对应的消息 ID，也可以输入消息 ID 进行精准查询。
3. 单击**查询**，下方列表会展示所有查询到的结果并分页展示。
![](https://qcloudimg.tencent-cloud.cn/raw/e2cfb55d14ca2b4bd3ba1d50d12e3786.png)
4. 找到您希望查看内容或参数的消息，单击操作列的**查看详情**，即可查看消息的基本信息、内容（消息体）以及参数。
![](https://qcloudimg.tencent-cloud.cn/raw/07fdf0c52915ec1ac060fc170f3391d5.png)

