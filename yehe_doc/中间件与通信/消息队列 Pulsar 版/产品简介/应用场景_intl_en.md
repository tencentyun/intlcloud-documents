## Async Decoupling

The transaction engine is the core system of Tencent billing. The data of each transaction order needs to be monitored by dozens of downstream business systems, including item price approval, delivery, reward point, and stream computing analysis. Such systems use different message processing logic, making it impossible for a single system to adapt to all associated business. In this case, TDMQ for Pulsar can implement efficient async communication and application decoupling to ensure the business continuity of the primary site.

![](https://main.qcloudimg.com/raw/0d9879224dd334eb4ccee436be1a6f81.svg)

## Peak Shifting

Companies hold promotional campaigns such as new product launch and festival red packet grabbing from time to time, which often cause temporary traffic spikes and pose huge challenges to each backend application system. In this case, TDMQ for Pulsar can act as a buffer to centrally collect the suddenly increased requests in the upstream, allowing downstream businesses to consume the request messages based on their actual processing capacities.

![](https://main.qcloudimg.com/raw/6bb7c310c0c4f6048df64705a0c4aff2.svg)

## Sequential Message Sending/Receiving

Sequential messages are used in some business scenarios, such as order creation, payment, delivery, and refund of in-app/game items, which are all strictly executed in sequence. Similar to the First In, First Out (FIFO) principle, TDMQ for Pulsar offers a sequential message feature dedicated to such scenarios to ensure message FIFO.

![](https://main.qcloudimg.com/raw/964ecdc85396c26fb4863acaa9fd2222.svg)

## Consistency of Distributed Transactions

Tencent Billing (Midas) is an internet billing platform that incubates and sustains Tencent businesses' revenue of hundreds of billions of CNY and handles amounts up to hundreds of millions of CNY per day. It solves the core problem of money-item consistency and uses TDMQ for Pulsar and distributed transactions to process business transactions, which greatly improve the efficiency and performance. A billing system often has a long transaction linkage with a significant chance of error or timeout. TDMQ for Pulsar's automated repush and abundant message retention features can be used to provide transaction compensation, and the eventual consistency of payment tips notifications and transaction pushes can also be achieved through TDMQ for Pulsar.

![](https://main.qcloudimg.com/raw/60a8f143cd749516c2f5f03b4d19ed5c.svg)

## Data Sync

TDMQ for Pulsar can easily implement cross-IDC sync if messages need to be consumed across many IDCs.

![](https://main.qcloudimg.com/raw/bf71094b56816dd68ad8c175e1c88e83.svg)

## Big Data Analysis

Data creates value in the "flow". Most traditional data analysis are based on batch computing models, which means they cannot analyze data in real time. In contrast, TDMQ for Pulsar can easily implement real-time analysis of business data when combined with a stream computing engine.

