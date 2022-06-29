## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Python as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed Python](https://www.python.org/downloads/)
- [You have installed pip](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-python-sdk-demo.zip)

## Directions

1. Prepare the environment.
   Install the `pulsar-client` library in the client environment as instructed in [Pulsar Python client](https://pulsar.apache.org/docs/en/client-libraries-python/).
   <dx-codeblock>
   :::  shell
   pip install pulsar-client==2.8.1
   :::
   </dx-codeblock>
2. Create a client.
<dx-codeblock>
:::  python
   # Create a client
   client = pulsar.Client(
       authentication=pulsar.AuthenticationToken(
           # Role token
           AUTHENTICATION),
       # Service access address
       service_url=SERVICE_URL)
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>SERVICE_URL</td>
        <td style='text-align:left;'>Cluster access address, which can be viewed and copied on the <a
                href='https://console.cloud.tencent.com/tdmq/cluster'><strong>Cluster</strong></a> page in the console.<br><img
                src="https://qcloudimg.tencent-cloud.cn/raw/8612bb79a799375eb97d5e871e239372.png"
                referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>AUTHENTICATION</td>
        <td style='text-align:left;'>Role token, which can be copied in the <strong>Token</strong> column on the <strong><a
                href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.<img
                src="https://qcloudimg.tencent-cloud.cn/raw/65a283caa4b28d9fab366114ea8636b1.png" referrerpolicy="no-referrer"
                alt="img"></td>
    </tr>
    </tbody>
</table>
3. Create a producer.
<dx-codeblock>
:::  python
   # Create a producer
   producer = client.create_producer(
       # Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from the **Topic** page.
       topic='pulsar-xxx/sdk_python/topic1'
   )
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
</dx-alert>
4. Send the message.
<dx-codeblock>
:::  python
   # Send the message
   producer.send(
       # Message content
       'Hello python client, this is a msg.'.encode('utf-8'),
       # Message parameter
       properties={'k': 'v'},
       # Business key
       partition_key='yourKey'
   )
:::
</dx-codeblock>
   The message can also be sent in async mode.
<dx-codeblock>
:::  python
   # Send the callback in async mode
   def send_callback(send_result, msg_id):
       print('Message published: result:{}  msg_id:{}'.format(send_result, msg_id))
   
   # Send the message
   producer.send_async(
       # Message content
       'Hello python client, this is a async msg.'.encode('utf-8'),
       # Async callback
       callback=send_callback,
       # Message configuration
       properties={'k': 'v'},
       # Business key
       partition_key='yourKey'
   )
:::
</dx-codeblock>
5. Create a consumer.
<dx-codeblock>
:::  python
   # Subscribe to the message
   consumer = client.subscribe(
       # Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from the **Topic** page.
       topic='pulsar-xxx/sdk_python/topic1',
       # Subscription name
       subscription_name='sub_topic1'
   )
:::
</dx-codeblock>
> ?
>
> - You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
>   ![img](https://qcloudimg.tencent-cloud.cn/raw/4bb986f5e871cb9d72d9066ecf7eea66.png)
> - You need to enter the subscription name in the `subscriptionName` parameter, which can be viewed on the **Consumption Management** page.
6. Consume the message.
<dx-codeblock>
:::  python
   # Obtain the message
   msg = consumer.receive()
   try:
       # Simulate the business processing logic
       print("Received message '{}' id='{}'".format(msg.data(), msg.message_id()))
       # Return `ack` as the acknowledgement if the consumption is successful
       consumer.acknowledge(msg)
   except:
       # If the consumption fails, the message will be delivered again
       consumer.negative_acknowledge(msg)
:::
</dx-codeblock>
7. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq), click **Topic** > **Topic Name** to enter the **Consumption Management** page, and click the triangle below a subscription name to view the production and consumption records.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/206f52b4a67a3a5eba82309e0d5bc001.png)

>?The above is a brief introduction to the way of publishing and subscribing to messages. For more operations, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-python-sdk-demo.zip) or [Pulsar Python client](https://pulsar.apache.org/docs/en/client-libraries-python/).
