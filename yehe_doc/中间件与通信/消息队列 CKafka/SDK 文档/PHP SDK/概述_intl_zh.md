Php 客户端可以通过消息队列 CKafka 提供的多种接入点接入并收发消息。

| 项目     | **默认接入点**         | **SASL 接入点**                                               |
| :------- | ---------------------- | ------------------------------------------------------------ |
| 网络     | VPC                    | VPC                                                          |
| 协议     | PLAINTEXT              | SASL_PLAINTEXT                                               |
| 端口     | 9092                   | 请在 [CKafka 控制台](https://console.cloud.tencent.com/ckafka) 实例基本信息页面的【接入方式模块】获取 SASL 接入点信息。<br>![](	https://main.qcloudimg.com/raw/de38f866a5cd865aae5dc00eb1c10fd0.png) |
| SASL 机制 | 不适用                 | PLAIN：一种简单的用户名密码校验机制。                        |
| Demo     | [PLAINTEXT](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/phpkafkademo)          | [SASL_PLAINTEXT/PLAIN](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/phpkafkademo)                                     |
| 文档     | [默认接入点收发消息](https://intl.cloud.tencent.com/document/product/597/40062) | [SASL 接入点 PLAIN 机制收发消息](https://intl.cloud.tencent.com/document/product/597/40063)                              |
