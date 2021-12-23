## Traffic Peak Shifting for Flash Sales System

A flash sales system may fail due to traffic surges. TDMQ for RabbitMQ can mitigate the traffic pressure at the upstream to secure the stable operations of the message system.

![](https://qcloudimg.tencent-cloud.cn/raw/26acc857144153c8e8c6214a1ea96335.svg)

## Async Decoupling of Business Systems

The order data in a transaction system involves over 100 downstream business systems, such as shipping, logistics, and order. TDMQ for RabbitMQ can implement async communication and service decoupling between systems to reduce their mutual dependency, improve the processing efficiency, and ensure the system stability.

![](https://qcloudimg.tencent-cloud.cn/raw/6b5b304edd6063cdb044e8f721ea9419.svg)
