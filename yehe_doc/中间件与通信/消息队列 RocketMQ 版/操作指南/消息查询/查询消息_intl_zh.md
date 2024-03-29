当一条消息从生产者发送到 TDMQ RocketMQ 版服务端，再由消费者进行消费，TDMQ RocketMQ 版会完整记录这条消息中间的流转过程，并以消息轨迹的形式呈现在控制台。
消息轨迹记录了消息从生产端到 TDMQ RocketMQ 版服务端，最后到消费端的整个过程，包括各阶段的时间（精确到微秒）、执行结果、生产者 IP、消费者 IP 等。
![](https://qcloudimg.tencent-cloud.cn/raw/a14a3f3df794422fc331be4ec54874c0.png)

## 操作场景

当您需要排查以下问题时，就可以使用 TDMQ RocketMQ 版控制台的消息查询功能，按照时间维度或者根据日志中查到的消息 ID/消息 Key，来查看具体某条消息的消息内容、消息参数和消息轨迹。

- 查看某条消息的具体内容，具体参数。
- 查看消息由哪个生产 IP 发送，是否发送成功，消息到服务端的具体时间。
- 查看消息是否已持久化。
- 查看消费由哪些消费者消费了，是否消费成功，消息确认消费的具体时间。
- 需要做分布式系统的性能分析，查看 MQ 对相关消息处理的时延。

## 查询限制

消息查询最多可以查询近3天的消息。



## 前提条件

已经参考 [SDK 文档](https://intl.cloud.tencent.com/document/product/1113/45956) 部署好生产端和消费端服务，并在3天内有消息生产和消费。

2022年8月8日部分地区上线新的虚拟集群 RocketMQ 服务，由于新版的集群与旧版集群的消息轨迹实现不同，所以在使用上有些许差异。旧版集群消息轨迹由服务端实现，客户端无需关注消息轨迹相关设置，新版集群需要客户端进行来设置开启消息轨迹功能，具体设置示例如下：
<dx-tabs>
::: <b>生产者设置</b>

<dx-codeblock>
:::  java
DefaultMQProducer producer = new DefaultMQProducer(namespace, groupName,
    // ACL权限
    new AclClientRPCHook(new SessionCredentials(AK, SK)), true, null);
:::
</dx-codeblock>

:::
::: <b>push 消费者设置</b>

<dx-codeblock>
:::  java
// 实例化消费者
DefaultMQPushConsumer pushConsumer = new DefaultMQPushConsumer(NAMESPACE,groupName,
    new AclClientRPCHook(new SessionCredentials(AK, SK)),
    new AllocateMessageQueueAveragely(), true, null);
:::
</dx-codeblock>

:::
::: <b>pull 消费者设置</b>

<dx-codeblock>
:::  java
DefaultLitePullConsumer pullConsumer = new DefaultLitePullConsumer(NAMESPACE,groupName,
    new AclClientRPCHook(new SessionCredentials(AK, SK)));
// 设置NameServer的地址
pullConsumer.setNamesrvAddr(NAMESERVER);
pullConsumer.setConsumeFromWhere(ConsumeFromWhere.CONSUME_FROM_LAST_OFFSET);
pullConsumer.setAutoCommit(false);
pullConsumer.setEnableMsgTrace(true);
pullConsumer.setCustomizedTraceTopic(null);
:::
</dx-codeblock>

:::
</dx-tabs>


## 操作步骤

1. 登录 [TDMQ RocketMQ 控制台](https://console.cloud.tencent.com/tdmq/rocket-cluster) ，在左侧导航栏单击**消息查询**。
2. 在消息查询页面，选择好地域后根据页面提示输入查询条件。
  - 时间范围：选择需要查询的时间范围，支持近6小时，近24小时，近3天和自定义时间范围。
  - 当前集群：选择需要查询的 Topic 所在的集群。
  - 命名空间：选择需要查询的 Topic 所在的命名空间。
  - Topic：选择需要查询的 Topic。
  - 查询方式：消息查询功能支持两种查询方式。
    - **按消息 ID 查询：**该方式属于精确查询、速度快、精确匹配。
    - **按消息 Key 查询：**该方式属于模糊查询，适用于您没有记录消息 ID 但是设置了消息 Key 的场景。
3. 单击**查询**，下方列表会展示所有查询到的结果并分页展示。
4. 找到您希望查看内容或参数的消息，单击操作列的**查看详情**，即可查看消息的基本信息、内容（消息体）以及参数。
5. 单击操作列的**查看消息轨迹**，或者在详情页单击 Tab 栏的**消息轨迹**，即可查看该消息的消息轨迹（详细说明请参见 [消息轨迹查询结果说明](https://www.tencentcloud.com/document/product/1113/51216)）。



### 消费验证

在查询到某条消息后，您可以单击操作列的**消费验证**将该条消息发送到指定的客户端来验证该消息。**该功能可能会导致消息重复。**

> ? 当前仅专享集群支持消费验证功能。消费验证功能仅用于验证客户端的消费逻辑是否正常，并不会影响正常的收消息流程，因此消息的消费状态等信息在消费验证后并不会改变。
