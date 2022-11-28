TDMQ for RocketMQ records the complete flow of a message being sent from the producer to the TDMQ for RocketMQ server for consumption by the consumer, which is displayed as a message trace in the console.
A message trace records the entire process of how a message flows, including the duration of each stage (accurate down to the microsecond), execution result, producer IP, and consumer IP.
![](https://qcloudimg.tencent-cloud.cn/raw/a14a3f3df794422fc331be4ec54874c0.png)

## Overview

You can use the message query feature in the TDMQ for RocketMQ console to view the content, parameters, and trace of a specific message by time or by the message ID/message key displayed in the log. With this feature, you can do the following:

- View the specific content and parameters of the message.
- View the producer IP from which a message was sent, whether it was sent successfully, and the exact time when it arrived at the server.
- View whether the message was persistently stored.
- View the consumers who consumed the message, whether it was consumed successfully, and the exact time when its consumption was acknowledged.
- View the message queue's message processing latency to analyze the performance of the distributed system.

## Query limits

You can query messages in the last 3 days.



## Prerequisites

You have deployed the producer and consumer services as instructed in the [SDK documentation](https://intl.cloud.tencent.com/document/product/1113/45956), and they produced and consumed messages in the last 3 days.

The TDMQ for RocketMQ virtual cluster service has been upgraded in some regions since August 8, 2022. The message trace feature of the old version of a virtual cluster is implemented by the server while that of the new version is implemented by the client. Therefore, if you use the new version of TDMQ for RocketMQ virtual cluster, you need to configure your client to enable the message trace feature. Below are sample settings:
<dx-tabs>
::: <b>Producer settings</b>

<dx-codeblock>
:::  java
DefaultMQProducer producer = new DefaultMQProducer(namespace, groupName,
    // ACL permission
    new AclClientRPCHook(new SessionCredentials(AK, SK)), true, null);
:::
</dx-codeblock>

:::
::: <b>Push consumer settings</b>

<dx-codeblock>
:::  java
// Instantiate the consumer
DefaultMQPushConsumer pushConsumer = new DefaultMQPushConsumer(NAMESPACE,groupName,
    new AclClientRPCHook(new SessionCredentials(AK, SK)),
    new AllocateMessageQueueAveragely(), true, null);
:::
</dx-codeblock>

:::
::: <b>Pull consumer settings</b>

<dx-codeblock>
:::  java
DefaultLitePullConsumer pullConsumer = new DefaultLitePullConsumer(NAMESPACE,groupName,
    new AclClientRPCHook(new SessionCredentials(AK, SK)));
// Set the NameServer address
pullConsumer.setNamesrvAddr(NAMESERVER);
pullConsumer.setConsumeFromWhere(ConsumeFromWhere.CONSUME_FROM_LAST_OFFSET);
pullConsumer.setAutoCommit(false);
pullConsumer.setEnableMsgTrace(true);
pullConsumer.setCustomizedTraceTopic(null);
:::
</dx-codeblock>

:::
</dx-tabs>


## Directions

1. Log in to the [TDMQ for RocketMQ console](https://console.cloud.tencent.com/tdmq/rocket-cluster) and click **Message Query** on the left sidebar.
2. On the **Message Query** page, select a region and enter the query conditions as prompted.
  - Time Range: Select the time range for query. You can select the last 6 hours, last 24 hours, or last 3 days, or set a custom time range.
  - Current Cluster: Select the cluster where the topic you want to query is located.
  - Namespace: Select the namespace where the topic you want to query is located.
  - Topic: Select the topic you want to query.
  - Query Method: Below are two supported query methods.
    - **By message ID:** A fast exact query method.
    - **By message key:** A fuzzy query method that is used when you have only set the message key.
3. Click **Query**, and the paginated results will be displayed in the list.
4. Click **View Details** in the **Operation** column of the target message to view its basic information, content (message body), and parameters.
5. Click **View Message Trace** in the **Operation** column or select the **Message Trace** tab on the details page to view the trace of the message. For more information, see [Message Trace Description](https://www.tencentcloud.com/document/product/1113/51216).



### Consumption verification

After a message is found, you can click **Verify Consumption** in the **Operation** column to send the message to the specified client for verification. **This feature may lead to message repetition.**

> ? Currently, the consumption verification feature is only available to exclusive clusters. It only verifies the client consumption logic to make sure it is normal without affecting message receiving. Therefore, the verification causes no changes in any message information such as message consumption status.
