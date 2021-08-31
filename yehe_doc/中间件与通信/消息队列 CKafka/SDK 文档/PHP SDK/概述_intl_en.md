The PHP SDK can access CKafka via different types of access points to send and receive messages.

| Item     | **Default Access Point**         | **SASL Access Point**                                               |
| :------- | ---------------------- | ------------------------------------------------------------ |
| Network     | VPC                    | VPC                                                          |
| Protocol     | PLAINTEXT              | SASL_PLAINTEXT                                               |
| Port     | 9092                   | Please obtain the SASL access point information in the **Access Mode** area in the **Basic Info** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka).<br>![](https://main.qcloudimg.com/raw/de38f866a5cd865aae5dc00eb1c10fd0.png) |
| SASL mechanism | N/A                 | PLAIN (a simple username/password authentication mechanism)                       |
| Demo     | [PLAINTEXT](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/phpkafkademo)          | [SASL_PLAINTEXT/PLAIN](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/phpkafkademo)                                     |
| Document     | [Using the Default Access Point to Send and Receive Messages](https://intl.cloud.tencent.com/document/product/597/40062) | [Using the SASL Access Point and PLAIN Mechanism to Send and Receive Messages](https://intl.cloud.tencent.com/document/product/597/40063)                             |
