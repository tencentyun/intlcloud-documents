## 秒杀系统流量削峰

秒杀系统可能因瞬时流量过大导致系统“宕机”，TDMQ RabbitMQ 版缓冲上游的流量压力，保证消息系统的稳定运行。

![](https://qcloudimg.tencent-cloud.cn/raw/26acc857144153c8e8c6214a1ea96335.svg)

## 业务系统异步解耦

交易系统的订单数据涉及下游上百个业务系统，如发货、物流、订单等。TDMQ RabbitMQ 版可以实现系统间的异步通信和服务解耦，减轻不同服务之间的依赖，提升处理效率，保证系统稳定性。

![](https://qcloudimg.tencent-cloud.cn/raw/6b5b304edd6063cdb044e8f721ea9419.svg)
