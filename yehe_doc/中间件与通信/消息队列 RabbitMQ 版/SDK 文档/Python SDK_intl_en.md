## Overview

This document describes how to use open-source SDK to send and receive messages using the SDK for Python as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources.](https://intl.cloud.tencent.com/document/product/1112/43069)
- [You have installed Python](https://www.python.org/downloads/)
- [You have installed pip](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-python-sdk-demo.zip)



## Directions

### Step 1. Add dependencies

1. RabbitMQ officially recommends Pika. First, you need to install Pika in the client environment.
   ```shell
   python -m pip install pika --upgrade
   ```

2. Import Pika when creating the client.
   ```python
   import pika
   ```



### Step 2. Produce messages

Create, compile, and run the message producing program `messageProducer.py`.
```python
import pika

# Use the username and password to create a login credential object
credentials = pika.PlainCredentials('rolename', 'eyJr***')
# Create a connection
connection = pika.BlockingConnection(pika.ConnectionParameters(
    host='amqp-xx.rabbitmq.x.com', port=5672, virtual_host='amqp-xxx|Vhostname', credentials=credentials))
# Establish a channel
channel = connection.channel()
# Declare the exchange
channel.exchange_declare(exchange='direct_exchange', exchange_type="direct")

routingKeys = ['aaa.bbb.ccc', 'aaa.bbb.ddd', 'aaa.ccc.zzz', "xxx.yyy.zzz"]

for routingKey in routingKeys:
    # Send a message to the specified exchange
    # If you send a message without specifying the exchange, you need to specify the message queue. If the exchange is specified, the `routing_key` parameter indicates the routing key; otherwise, it indicates the message queue name
    channel.basic_publish(exchange='direct_exchange',
                          routing_key=routingKey,
                          body=(routingKey + 'This is a new direct message.').encode(),
                          properties=pika.BasicProperties(
                              delivery_mode=2,  # Set message persistence
                          ))
    print('send success msg to rabbitmq')
connection.close()
```

| Parameter | Description |
| :-------------- | :----------------------------------------------------------- |
| rolename        | Role name, which can be copied on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. |
| eyJr***          | Role key, which can be copied in the **Key** column on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/4888f178ea288d44685b8d7347cbcf70.png) |
| host              | Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/cd3184b4da945fadd138ac1651485d38.png) |
| port              | Cluster access port, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. |
| virtual_host      | Vhost name in the format of **"cluster ID + \| + vhost name"**, which can be copied on the **Vhost** page in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/4063f65f2eb4ca14abe38ae939a3ac26.png) |
| direct_exchange        | Exchange name, which can be obtained from the exchange list in the console.                  |
| routingKeys     | Message routing rule, which can be obtained in the **Binding Key** column in the binding list in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/63ddc4564efd2b741b12bee97481dc6c.png) |

### Step 3. Consume messages

Create, compile, and run the message consuming program `messageConsumer.py`.
```python
import os
import pika
import sys


def main():
    # Use the username and password to create a login credential object
    credentials = pika.PlainCredentials('rolename', 'eyJr***')
    # Create a connection
    connection = pika.BlockingConnection(pika.ConnectionParameters(
        host='amqp-xx.rabbitmq.x.com', port=5672, virtual_host='amqp-xxx|Vhostname', credentials=credentials))
    # Establish a channel
    channel = connection.channel()
    # Declare the message queue
    channel.queue_declare(queue='route_queue1', exclusive=True, durable=True)
    # Bind the message queue to the exchange and specify the routing key
    routing_keys = ['aaa.bbb.ccc', 'aaa.bbb.ddd']
    for routingKey in routing_keys:
        channel.queue_bind(exchange='direct_exchange', queue="route_queue1", routing_key=routingKey)
    # Set that only one unacknowledged message can be received
    channel.basic_qos(prefetch_count=1)

    # Message consumption logic
    def callback(ch, method, properties, body):
        print(" [Consumer1(Direct 'aaa.bbb.ccc'/'aaa.bbb.ddd')] Received (%r)" % body)
        # Manually return the ACK
        ch.basic_ack(delivery_tag=method.delivery_tag)

    # Create a consumer to consume messages in the message queue
    channel.basic_consume(queue='route_queue1',
                          on_message_callback=callback,
                          auto_ack=False)  # Set to manual acknowledgment

    print(" [Consumer1(Direct 'aaa.bbb.ccc'/'aaa.bbb.ddd')] Waiting for messages. To exit press CTRL+C")
    channel.start_consuming()


if __name__ == '__main__':
    try:
        main()
    except KeyboardInterrupt:
        print('Interrupted')
        try:
            sys.exit(0)
        except SystemExit:
            os._exit(0)
```

| Parameter | Description |
| :-------------- | :----------------------------------------------------------- |
| rolename        | Role name, which can be copied on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. |
| eyJr***          | Role key, which can be copied in the **Key** column on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/32045def87e6ebf4142b19718f2cc9e7.png) |
| host              | Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/2d915273c7157f67ac6cdcfe0993a7ad.png) |
| port              | Cluster access port, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. |
| virtual_host      | Vhost name in the format of **"cluster ID + \| + vhost name"**, which can be copied on the **Vhost** page in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/ae7071f7a102ff6553b6332cd19aa7df.png) |
| direct_exchange        | Exchange name, which can be obtained from the exchange list in the console.                  |
| route_queue1      | Queue name, which can be obtained from the queue list in the console.                         |
| routingKey     | Message routing rule, which can be obtained in the **Binding Key** column in the binding list in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/7f5f401a9bd32a1ba06c17e50e8c4690.png) |

### Step 4. View messages

To check whether messages are sent to TDMQ for RabbitMQ successfully, view the connected consumer status on the **[Cluster](https://console.cloud.tencent.com/tdmq/rabbit-cluster)** > **Queue** page in the console.

![img](https://qcloudimg.tencent-cloud.cn/raw/787f5f8df79d4ba86ddaf2a9223a93bb.png)

>? For the complete sample code and other use cases, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-python-sdk-demo.zip) or [RabbitMQ Tutorials](https://www.rabbitmq.com/getstarted.html).
