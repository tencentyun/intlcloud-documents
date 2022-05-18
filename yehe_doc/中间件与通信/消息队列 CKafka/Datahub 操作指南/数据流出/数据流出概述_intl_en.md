The low-latency processing capability of CKafka makes it easier to process (consume) distributed data from multiple data sources. Under the same performance conditions, CKafka provides more durable persistent storage and lower end-to-end latency than a centralized data aggregation system.

DataHub offers data distribution capacities. It can distribute data such as real-time web access logs, application logs, and various types of events to downstream Tencent Cloud products by using SCF or a sink connector. You can then write an application or use the Oceanus engine to process such data and generate real-time data processing results such as charts, alarms, and statistics.

![](https://qcloudimg.tencent-cloud.cn/raw/813660dbc2b33dc4c3758c49faf1dbf0.png)

Currently, data can be distributed to the following targets:

- [ES](https://intl.cloud.tencent.com/document/product/597/46826)
- [TDW](https://intl.cloud.tencent.com/document/product/597/46827)
- [CDWCH](https://intl.cloud.tencent.com/document/product/597/46828)
- [CLS](https://intl.cloud.tencent.com/document/product/597/46829)
- EventBridge: Data distributed to EventBridge can be further distributed to the following targets:
  - [COS](https://intl.cloud.tencent.com/document/product/597/46833)
  - [CLS](https://intl.cloud.tencent.com/document/product/597/46834)
  - [ES](https://intl.cloud.tencent.com/document/product/597/46835)

> ? Data distribution to EventBridge is supported only in Beijing, Shanghai, and Guangzhou regions and relies on SCF and other Tencent Cloud products, which should be activated first.



## Restrictions and Billing

- The dump speed is subject to the limit of the peak bandwidth of the CKafka instance. If the consumption is too slow, check the peak bandwidth settings.
- Data distribution to EventBridge is provided based on the SCF service that offers a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). For more information on the fees for excessive usage, see the [billing rules](https://intl.cloud.tencent.com/document/product/583/17299) of SCF.
