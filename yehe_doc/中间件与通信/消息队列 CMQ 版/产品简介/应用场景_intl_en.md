## One-to-Many Production

There are many communications between system components or applications, each of which needs to maintain their own network connections. Plus, the types of communicated content are diverse, further making it difficult and costly to implement such communications. In this case, TDMQ for CMQ can support a single producer for several subscribers and deliver messages asynchronously. It can also enable clients to consume certain messages through message filtering.

![](https://qcloudimg.tencent-cloud.cn/raw/9b9693bca84e00f2537d8ab223670bd3.png)

## Async Notification

When a message is sent, it cannot be delivered reliably if the recipient is unavailable due to power outage, server downtime, or CPU overload. If TDMQ for CMQ is used, the message will be persistently stored in a queue until the recipient becomes available to consume it successfully.

![](https://qcloudimg.tencent-cloud.cn/raw/cfb2a95e7c922bab57d1a9092a046a8c.png)

## System Decoupling

Your business receives contents submitted by users, stores some data in your own system, and forwards the processed data to other business applications (such as data analysis and storage systems). These system components or applications are closed coupled with each other. In contrast, if TDMQ for CMQ is used, the recipient and sender are imperceptible to each other's information, which greatly reduces the coupling degree. This is especially helpful when the controllability of dependent components is low.

![](https://qcloudimg.tencent-cloud.cn/raw/6d80dba49234b720d065b88565ca8fdb.png)

## Peak Shifting

During flash or group sales, the high number of users often causes temporary traffic spikes and poses huge challenges to each backend application system. In this case, TDMQ for CMQ can act as a buffer to centrally collect the suddenly increased requests in the upstream, allowing downstream businesses to consume the request messages based on their actual processing capacities.

![](https://qcloudimg.tencent-cloud.cn/raw/ab39604cefd6652dbf5e6170a4968886.png)

## Unified Platform

As an ecommerce system grows over time, if the order system (order_module), inventory system (inventory_module), and shipping system use Java, Erlang, and Python architectures respectively, developers may need to spend much time maintaining some redundant code to sustain the communications between the modules. After TDMQ for CMQ is introduced, such troubles caused by the differences between platforms and between programming languages can be eliminated.

![](https://qcloudimg.tencent-cloud.cn/raw/9e92200df5db544039876d15f80832a0.png)

## Cross-user Data Exchange

Two services need to communicate with each other when their networks cannot interconnect or the application route information (such as IP and port) is variable. For example, if two Tencent Cloud services need communication but don't know each other's address, they can agree on the queue name in TDMQ for CMQ, so that one service can send messages to the queue and the other can receive messages from it and thus implement data exchange.

![](https://qcloudimg.tencent-cloud.cn/raw/de401a79ac507ef106269f3f1e500020.png)

