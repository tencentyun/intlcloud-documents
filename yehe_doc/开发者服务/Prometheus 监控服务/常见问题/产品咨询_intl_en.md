
### Does TMP support customizing the reported data?[](id:question2)

Yes. TMP supports customizing the reported metric monitoring data in multiple languages and displaying such data in the integrated Grafana dashboards.


### How does TMP collect monitoring data?

TMP can pull data through the Prometheus agent or write data through Pushgateway. It is fully compatible with open-source Prometheus in terms of collection method.

### Is there a separate exporter for each instance?

Each MySQL or Kafka instance has one exporter, while multiple Redis instances can share the same exporter.


### What is the difference between TMP and a self-built Prometheus service?

TMP is fully compatible with the open-source Prometheus ecosystem and is integrated with CM to help you quickly set up a monitoring system (for custom monitoring, component monitoring, basic monitoring, etc.). It supports Grafana, with preset common monitoring dashboards. It also supports diverse exporters, with preset common alarm templates. It well solves various problems with open-source Prometheus, such as complicated HA setup, poor performance, and labor-intensive Ops.

### Which Tencent Cloud products does TMP support?

TMP supports CVM, TencentDB for MongoDB, TencentDB for MySQL, TencentDB for PostgreSQL, TencentDB for Redis, ES, and TKE. For more information, see [Integration Center](https://intl.cloud.tencent.com/document/product/1116/43163).


### Can I integrate other data sources on the **Grafana** page of TMP?
No. We recommend you integrate them by using [Grafana](https://www.tencentcloud.com/document/product/1124).


### Can I pull monitoring data in Prometheus pull mode?

No, you can only pull data through APIs. For detailed directions, see [Querying Monitoring Data](https://intl.cloud.tencent.com/document/product/1116/43212).

### What is the series storage limit on pay-as-you-go TMP instances?
Each instance can have up to 4.5 million series. If you need to adjust it, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.

### Does TMP support integration with EKS?
Yes. Pay-as-you-go TMP instances support general clusters, EKS elastic clusters, edge clusters, and registered clusters.

