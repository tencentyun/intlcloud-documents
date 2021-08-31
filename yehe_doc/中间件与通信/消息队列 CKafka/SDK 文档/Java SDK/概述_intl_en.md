The Java SDK can access CKafka via different types of access points to send and receive messages.

| Item     | **Default Access Point**         | **SASL Access Point**                                               |
| :------- | ---------------------- | ------------------------------------------------------------ |
| Network     | VPC                    | VPC                                                          |
| Protocol     | PLAINTEXT              | SASL_PLAINTEXT                                               |
| Port     | 9092                   | Please obtain the SASL access point information in the **Access Mode** area in the **Basic Info** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka).<br>![](https://main.qcloudimg.com/raw/777d60f973af7b07a3ebf2d41a861b21.png) |
| SASL mechanism | N/A                 | PLAIN (a simple username/password authentication mechanism)                       |
| Demo     | [PLAINTEXT](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/javakafkademo)          | [SASL_PLAINTEXT/PLAIN](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/javakafkademo)                                     |
| Document     | [Using the Default Access Point to Send and Receive Messages](https://intl.cloud.tencent.com/document/product/597/40056) | [Using the SASL Access Point and PLAIN Mechanism to Send and Receive Messages](https://intl.cloud.tencent.com/document/product/597/40057)                             |
