### How do I select the instance specification?

You can use the specification calculator in the [console](https://console.cloud.tencent.com/ckafka/migration) to calculate the required production specification.
<img src="https://main.qcloudimg.com/raw/15b721ef605d238f01f888b6a54a334e.png" width="550px">

CKafka instances are divided into Standard Edition and Pro Edition according to their specifications. For the comparison between the two editions, please see [Product Specifications](https://intl.cloud.tencent.com/document/product/597/41815).

Please select an appropriate product specification as needed. For the billing rules of different specifications, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745).

### What are the modes of instance upgrade? What are their differences?

The multiple migration modes of the Standard and Pro Editions are lossless, non-stop, and imperceptible to the client.

Standard Edition uses a shared cluster. If the available resources in the cluster are sufficient, instances will be upgraded by increasing the quota, with no data migration involved; therefore, upgrade can be completed in several minutes normally. If the available resources in the cluster are insufficient, the system will prompt that the resources are insufficient, and you need to submit a ticket for data migration and resource allocation on the backend and then perform normal Standard Edition instance upgrade in the console.

Pro Edition uses a dedicated cluster. When the system algorithm finds that the current dedicated resource pool cannot sustain the resource quota after instance upgrade, it will automatically add resources to the resource pool and migrate instance data. Therefore, Pro Edition has two instance upgrade modes:

- When the resources are sufficient, instances will be upgraded by increasing the quota, which can be completed in several minutes.
- When the resources are insufficient, data migration will be involved, which may take several minutes to hours subject to the size of heaped data in the cluster.

If data migration is required, you can customize the migration time:

![](https://main.qcloudimg.com/raw/50035915db52c093577406f0707722f2.png)

If data migration is required, you can select a migration mode and set scheduled migration. There are two migration modes:

- Stable: CKafka will limit the speed of data migration during the upgrade to ensure that instances have optimal bandwidth performance. This option is recommended if you do not want to affect business operations.
- High-Speed: CKafka will not limit the speed of data migration during the upgrade, thus affecting the bandwidth available for data production and consumption of instances. This option is recommended for off-peak hours or when service suspension is allowed.

As migration will use cluster bandwidth and disk resources, you may worry about that the migration will affect the business during peak hours. In this case, you can set scheduled migration; for example, you can set the start time of instance upgrade to midnight. For detailed directions of instance upgrade, please see [Upgrading Instance](https://intl.cloud.tencent.com/document/product/597/40650).

### Do instances support data compression?

Currently, CKafka supports open-source Snappy and lz4 message compression formats. As gzip compression has high CPU usage, it is not supported currently. If compression is enabled, it may increase the server pressure in some cases; for example, if the producer protocol version is high, but the consumer protocol version is low, downward version conversion may occur during consumption, increasing the server pressure. Therefore, we recommend you disable message compression before performing a stress test.

Configuration method: in the configuration file of the producer, set the `compression.type` parameter to `snappy` or `lz4`. The default value is `none`, indicating that the feature is disabled.

We recommend you preferentially select Snappy for compression. After compression is enabled, the server CPU utilization and the production and consumption time may increase. Therefore, please enable it with caution.

