### How do I purchase the TEM service?
The TEM service is currently in the beta period. You can log in to the [TEM console](https://console.cloud.tencent.com/tem) to experience it free of charge. For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1094/40347).


### Which languages does TEM support?
TEM currently supports microservice applications written in Java. You can make Docker images for non-microservice applications and uploading them to TEM. In this way, you can deploy applications written in any language in TEM.


### All my businesses are in CVM. Do I need to modify the code when migrating them to TEM?
TEM features non-intrusive integration with no business code changes required, which greatly reduces the migration costs. Taking Spring Cloud applications with Eureka or ZooKeeper as the registry as an example, when you migrate them to TEM, you don't need to make any changes, which implements smooth migration imperceptible to users.


### How does TEM implement OPS-free operations?
TEM makes resources serverless, so that you no longer need to estimate the capacity or purchase machine resources. In addition, it also enables quick application deployment, automated monitoring, service governance, and other capabilities, lowering the OPS threshold of your microservices and thus implementing OPS-free operations.


### At what granularities can TEM automatically scale resources?
TEM supports auto scaling at finer resource granularities down to 0.25 CPU cores, which greatly reduces you resource costs.


### What monitoring metrics does TEM provide?
TEM currently provides basic monitoring capabilities (in the CPU and memory dimensions) and will add more metrics in business dimensions such as QPS, response delay, and slow query in the future.

### If I use TEM, can I still use other Tencent Cloud services such as TencentDB for Redis and CKafka?
TEM is perfectly compatible with other Tencent Cloud services such as TencentDB for Redis and CKafka for unrestricted access.


### What are the differences between TEM and TSF?
- TSF currently supports CVM-based and container-based deployment. These two deployment modes require resource preparations according to business peaks, where scaling is cumbersome.
- TEM delivers an on-demand, pay-as-you-go, and OPS-free user experience with no need to prepare resources.
