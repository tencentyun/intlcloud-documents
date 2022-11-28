TDMQ for RocketMQ is distributed message middleware developed by Tencent Cloud based on Apache RocketMQ. It is fully compatible with all the components and principles of Apache RocketMQ and supports connection to open-source RocketMQ clients without any modifications.

Featuring low latency, high performance, reliability, and scalability, and trillions of QPS, TDMQ for RocketMQ can add async decoupling and peak shifting capabilities to distributed application systems. It also provides the capabilities that internet applications require, such as massive message retention, high throughput, and reliable retry mechanism.



TDMQ for RocketMQ is available in the forms of virtual cluster and exclusive cluster.

Virtual clusters are logically isolated from each other and are billed in a **pay-as-you-go (postpaid)** manner, so you only need to pay for the messages and topic resources you used. Such clusters are suitable for business scenarios where the number of messages is small or fluctuates greatly. They are currently in beta testing and will be billed from December, 2022.

Exclusive clusters are physically isolated from each other and are billed in a **monthly subscribed (prepaid)** manner, so you need to make an upfront purchase. If your business involves a large volume of messages, you will find it more cost-effective to use exclusive clusters to meet your high SLA requirements.

For comparison between the two cluster types, see [Product Series](https://www.tencentcloud.com/document/product/1113/51102).
