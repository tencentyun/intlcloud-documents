日志服务（Cloud Log Service，CLS）支持采集多个云产品的日志数据，例如：SCF 运行日志、CDN 实时日志、TKE 容器日志、CLB 访问日志等。用户可以使用 CLS 服务进行操作记录查看，运营数据统计分析，运行状况监控告警等多种日志数据处理功能。
当前 CLS 支持采集的云产品日志如下：

| 云产品名称                                              | 采集指引                                                     | 日志分析                                                     |
| :------------------------------------------------------ | :----------------------------------------------------------- | ------------------------------------------------------------ |
| 负载均衡（Cloud Load Balancer，CLB）                    | CLB 控制台配置，[配置指引](https://intl.cloud.tencent.com/document/product/214/35063)。 | [CLB 访问日志分析](https://intl.cloud.tencent.com/document/product/614/42746) |
| 内容分发网络（Content Delivery Network，CDN）           | CDN 控制台配置，[配置指引](https://intl.cloud.tencent.com/document/product/228/35380) 。 | [CDN 访问日志分析](https://intl.cloud.tencent.com/document/product/614/42748) |
| 全站加速网络（Enterprise Content Delivery Network，ECDN) | CDN 控制台配置，[配置指引](https://www.tencentcloud.com/document/product/228/35380) 。 | [CDN 访问日志分析](https://intl.cloud.tencent.com/document/product/614/42748) |
| 边缘安全加速平台（EdgeOne）                             | EdgeOne 控制台配置，[配置指引](https://www.tencentcloud.com/document/product/1145/46351) | -                                                            |
| 云服务器（Cloud Virtual Machine，CVM）                  | 安装配置 LogListener，[采集指引](https://www.tencentcloud.com/document/product/614/42133)。 | -                                                            |
| 容器服务（Tencent Kubernetes Engine，TKE）              | TKE 控制台配置，[配置指引](https://intl.cloud.tencent.com/document/product/457/32419) 。 | [TKE 事件日志分析](https://intl.cloud.tencent.com/document/product/614/42750)<br>[TKE 审计日志分析](https://intl.cloud.tencent.com/document/product/614/42751) |
| 云函数（Serverless Cloud Function，SCF）                | SCF 控制台配置，[配置指引](https://intl.cloud.tencent.com/document/product/583/34876) 。 | -                                                            |
| 云审计（CloudAudit）                                    | CloudAudit 控制台配置，[配置指引](https://intl.cloud.tencent.com/document/product/1021/42145)。 | -                                                            |
| 对象存储（Cloud Object Storage，COS）                   | COS 控制台配置，[配置指引](https://intl.cloud.tencent.com/document/product/614/42885)。 | [COS 访问日志分析](https://intl.cloud.tencent.com/document/product/614/42749) |
| 网络流日志（Flow Logs，FL）                             | FL 控制台配置，[配置指引](https://intl.cloud.tencent.com/document/product/682/18966)。 | [CCN 网络流日志分析](https://intl.cloud.tencent.com/document/product/614/48462) |
| 腾讯云 TI 平台（TI-ONE）                                  | TI-ONE 控制台配置，配置指引。 | -                                                            |
| Web 应用防火墙（Web Application Firewall，WAF）         | WAF 控制台配置，配置指引。 | -                                                            |
| 消息队列 CKafka（Cloud Kafka）                          | CKafka 控制台配置，配置指引。 | -                                                            |
| 物联网通信（Internet of Things Hub， IoT Hub）          | IoT Hub 控制台配置，[配置指引](https://intl.cloud.tencent.com/document/product/1105/41482)。 | -                                                            |