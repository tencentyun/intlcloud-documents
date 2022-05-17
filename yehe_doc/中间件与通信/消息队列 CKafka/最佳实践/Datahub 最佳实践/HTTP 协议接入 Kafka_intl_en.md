## Overview

Apache Kafka, like any client-server application, offers access to its functionality through a well-defined set of APIs. These APIs are exposed via the Kafka wire protocol, a Kafka-specific binary protocol over TCP. The best way to interact with the Apache Kafka APIs is to make use of a client library that works with the Kafka wire protocol. The Apache Kafka project only officially supports a client library for Java, but in addition to that, Confluent officially supports client libraries for C/C++, C#, Go, and Python.

Unfortunately, some programming languages lack officially supported, production-grade client libraries for Kafka. However, HTTP is a widely available, universally supported protocol. For data access, DataHub exposes message sending APIs over the HTTP protocol to simplify client configurations.

This document describes message sending in the HTTP-based data access feature of DataHub and provides suggestions for real world cases.

## Architecture

After the HTTP data access layer is enabled, an HTTP client in the public network can directly send messages to a CKafka instance through TencentCloud API as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/37a35f97e9ede93e35b3a3567cc50884.jpg)

### Prerequisites

You have created the target CKafka instance and topic.

## Directions

### Creating data access task

For detailed directions, see [Reporting over HTTP](https://intl.cloud.tencent.com/document/product/597/46807).


### Sending message via SDK

1. Import the data reporting SDK through Maven or Gradle into the Java project. Below is the `pom.xml` file for project configuration:
<dx-codeblock>
:::  xml
<dependency>
    <groupId>com.tencentcloudapi</groupId>
    <artifactId>tencentcloud-sdk-java</artifactId>
    <version>3.1.430</version>
</dependency>
:::
</dx-codeblock>
2. Click **Task Details** in [Data Access](https://console.intl.cloud.tencent.com/ckafka/datahub-access) and copy the access point information to the SDK for data writes.
![](https://qcloudimg.tencent-cloud.cn/raw/c0cdd9480626d044fbab71b63d35679e.png)
3. Enter the access point information. In the sample code, `generateMsgFromUserAccess` is used to assemble all messages to be sent.
   <dx-codeblock>
   :::  java
   List<BatchContent> batchContentList = generateMsgFromUserAccess(userId);
   // Here, `ap-xxx` is the region abbreviation of the corresponding TencentCloud API
   CkafkaClient client = new CkafkaClient(
   new Credential("yourSecretId", "yourSecretKey"), "ap-xxx");
   

SendMessageRequest messageRequest = new SendMessageRequest();
// Access point ID of the data access task
messageRequest.setDataHubId("datahub-lzxxxxx6");
messageRequest.setMessage(batchContentList.toArray(BatchContent[]::new));

try {
  SendMessageResponse sendMessageResponse = client.SendMessage(messageRequest);
  String[] messageId = sendMessageResponse.getMessageId();
  for (String s : messageId) {
	 LOGGER.info(s)
  }
} catch (TencentCloudSDKException e) {
  LOGGER.error(e.getMessage());
}
:::
</dx-codeblock>
4. Below is a sample returned value for message sending at the HTTP access layer:
<dx-codeblock>
:::  json
{
    "Response": {
        "MessageId": [
            "datahub-lxxxxxx6:topicDev:4:2:1648185961342:1648185961398"
        ],
        "RequestId": "3fq3na5r-xxxx-xxxx-xxxx-b2fiv0se7ded"
    }
}
:::
</dx-codeblock>
5. Here, **MessageId** consists of a series of metadata fields returned after the message is sent to the CKafka instance, as detailed below:
<dx-codeblock>
:::  json
"[datahubId]:[topic name]:[topic partition number]:[topic offset]:[time when the HTTP access layer received the message]:[time when the message was sent to Kafka]"
:::
</dx-codeblock>


### Querying message

You can query messages sent at the HTTP access layer in the [CKafka console](https://intl.cloud.tencent.com/document/product/597/39719). For detailed directions, see [Querying Message](https://intl.cloud.tencent.com/document/product/597/39719). In this example, messages at offset 2 in partition 4 in the `topicDev` topic are queried as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9aa559445ddd6053bc6bcba0eceb9cbf.png)


### Pausing task

If you find that the data access task affects the normal business, you can pause the task.

1. On the [Data Access](https://console.intl.cloud.tencent.com/ckafka/datahub-access) page, click **Pause** in the **Operation** column of the target task to pause the task.
![](https://qcloudimg.tencent-cloud.cn/raw/d41b251855cc6f057c4cdb2497069f19.png)
2. If the prompt in the top-right corner in the following figure is displayed, the task was paused successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/417a61130eefa1d41ee1a29bfdb4a394.png)
3. At this time, if you send a message at the HTTP access layer, you will receive the following response:
<dx-codeblock>
:::  json
{
    "Response": {
        "Error": {
            "Code": "FailedOperation",
            "Message": "task status suspended [datahub-lxxxxxx6]"
        },
        "RequestId": "5f737a5b-xxxx-xxxx-xxxxx-b2fb703e7ded"
    }
}
:::
</dx-codeblock>

