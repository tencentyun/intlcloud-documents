## Async Decoupling

The transaction engine is the core system of Tencent billing. The data of each transaction order needs to be monitored by dozens of downstream business systems, including item price approval, delivery, reward point, and stream computing analysis. Such systems use different message processing logic, making it impossible for a single system to adapt to all associated business. In this case, TDMQ for Pulsar can implement efficient async communication and application decoupling to ensure the business continuity of the primary site.

![](https://qcloudimg.tencent-cloud.cn/raw/ba9e98b9b9fcc26668784f7446474b48.svg)

## Peak Shifting

Companies hold promotional campaigns such as new product launch and festival red packet grabbing from time to time, which often cause temporary traffic spikes and pose huge challenges to each backend application system. In this case, TDMQ for Pulsar can act as a buffer to centrally collect the suddenly increased requests in the upstream, allowing downstream businesses to consume the request messages based on their actual processing capacities.

![](https://qcloudimg.tencent-cloud.cn/raw/49b4ee40f2e00a0a10b34957c22fc918.svg)

## Sequential Message Sending/Receiving

Sequential messages are used in some business scenarios, such as order creation, payment, delivery, and refund of in-app/game items, which are all strictly executed in sequence. Similar to the First In, First Out (FIFO) principle, TDMQ for Pulsar offers a sequential message feature dedicated to such scenarios to ensure message FIFO.

![](https://qcloudimg.tencent-cloud.cn/raw/b0b56746d9a5985e902b568d90938f78.svg)

## Consistency of Distributed Transactions

Tencent Billing (Midas) is an internet billing platform that incubates and sustains Tencent businesses' revenue of hundreds of billions of CNY and handles amounts up to hundreds of millions of CNY per day. It solves the core problem of money-item consistency and uses TDMQ for Pulsar and distributed transactions to process business transactions, which greatly improve the efficiency and performance. A billing system often has a long transaction linkage with a significant chance of error or timeout. TDMQ for Pulsar's automated repush and abundant message retention features can be used to provide transaction compensation, and the eventual consistency of payment tips notifications and transaction pushes can also be achieved through TDMQ for Pulsar.

![](https://qcloudimg.tencent-cloud.cn/raw/f60f81e0cf0d954f5e73d4a82a124d6e.svg)

## Data Sync

TDMQ for Pulsar can easily implement cross-IDC sync if messages need to be consumed across many IDCs.

![](https://qcloudimg.tencent-cloud.cn/raw/91bd5517d8ae4a89e454172821b528e6.svg)

## Big Data Analysis

Data creates value in the "flow". Most traditional data analysis are based on batch computing models, which means they cannot analyze data in real time. In contrast, TDMQ for Pulsar can easily implement real-time analysis of business data when combined with a stream computing engine.

