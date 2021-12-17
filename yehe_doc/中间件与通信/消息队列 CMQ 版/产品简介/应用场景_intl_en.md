## One-to-Many Production

There are many communications between system components or applications, each of which needs to maintain their own network connections. Plus, the types of communicated content are diverse, further making it difficult and costly to implement such communications. In this case, TDMQ for CMQ can support a single producer for several subscribers and deliver messages asynchronously. It can also enable clients to consume certain messages through message filtering.

![](https://main.qcloudimg.com/raw/779f9d46b84da0c7f2d1c2471fd2d03c.svg)



## Async Notification

When a message is sent, it cannot be delivered reliably if the recipient is unavailable due to power outage, server downtime, or CPU overload. If TDMQ for CMQ is used, the message will be persistently stored in a queue until the recipient becomes available to consume it successfully.

![](https://main.qcloudimg.com/raw/000923c8cf36ac9224f0a9b5b7b07e9b.svg)




## System Decoupling

Your business receives contents submitted by users, stores some data in your own system, and forwards the processed data to other business applications (such as data analysis and storage systems). These system components or applications are closed coupled with each other. In contrast, if TDMQ for CMQ is used, the recipient and sender are imperceptible to each other's information, which greatly reduces the coupling degree. This is especially helpful when the controllability of dependent components is low.

![](https://main.qcloudimg.com/raw/d1549d9fb9f9688a0b0e51bc439be85e.svg)

## Peak Shifting

During flash or group sales, the high number of users often causes temporary traffic spikes and poses huge challenges to each backend application system. In this case, TDMQ for CMQ can act as a buffer to centrally collect the suddenly increased requests in the upstream, allowing downstream businesses to consume the request messages based on their actual processing capacities.

![](https://main.qcloudimg.com/raw/6d4ecc8fd681d4c5354f41b4db9ae8df.svg)

## Unified Platform

As an ecommerce system grows over time, if the order system (order_module), inventory system (inventory_module), and shipping system use Java, Erlang, and Python architectures respectively, developers may need to spend much time maintaining some redundant code to sustain the communications between the modules. After TDMQ for CMQ is introduced, such troubles caused by the differences between platforms and between programming languages can be eliminated.

![](https://main.qcloudimg.com/raw/7d83c6392d352a64ca0a3a91b7e49bd4.svg)


## Cross-user Data Exchange

Two services need to communicate with each other when their networks cannot interconnect or the application route information (such as IP and port) is variable. For example, if two Tencent Cloud services need communication but don't know each other's address, they can agree on the queue name in TDMQ for CMQ, so that one service can send messages to the queue and the other can receive messages from it and thus implement data exchange.

![](https://main.qcloudimg.com/raw/effa13d288155a02222860748bd41dc1.svg)

