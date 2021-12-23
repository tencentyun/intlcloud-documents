## Traffic Peak Shifting for Flash Sales System

A flash sales system may fail due to traffic surges. TDMQ for RabbitMQ can mitigate the traffic pressure at the upstream to secure the stable operations of the message system.

![](https://main.qcloudimg.com/raw/038b68e5fdb74d4a5fd9e2c01615a06b.svg)

## Async Decoupling of Business Systems

The order data in a transaction system involves over 100 downstream business systems, such as shipping, logistics, and order. TDMQ for RabbitMQ can implement async communication and service decoupling between systems to reduce their mutual dependency, improve the processing efficiency, and ensure the system stability.

![](https://main.qcloudimg.com/raw/f298ddad8957c4ab5b2066fdfb5d51d4.svg)
