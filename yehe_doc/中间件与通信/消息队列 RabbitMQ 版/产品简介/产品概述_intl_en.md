TDMQ for RabbitMQ is Tencent's proprietary message queue service. It supports the AMQP 0-9-1 protocol and is fully compatible with all components and principles of Apache RabbitMQ. It also has the underlying benefits of computing-storage separation and flexible scaling.

TDMQ for RabbitMQ has extremely flexible routing to adapt to the message delivery rules of various businesses. It can buffer the upstream traffic pressure and ensure the stable operations of the message system. It is often used to implement async communication and service decoupling between systems to reduce their mutual dependency, making it widely applicable to distributed systems in finance and government affairs industries.

## Architecture

 The basic concepts of TDMQ for RabbitMQ are as follows: 

- Producer: sends messages to exchanges.
- Vhost: is used for logical isolation. Exchanges and queues of different vhosts are isolated from each other.
- Exchange: receives messages from producers and routes them to queues.
- Queue: caches messages for consumers to consume them.
- Consumer: pulls messages from queues for consumption.

![](https://qcloudimg.tencent-cloud.cn/raw/52a2af2c7b2f6fe1d514c6c9caa347d4.svg)

For more concepts of TDMQ for RabbitMQ, see [Relevant Concepts](https://intl.cloud.tencent.com/document/product/1112/43065). 

