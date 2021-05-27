A Python client can access multiple access points provided by CKafka to receive and send messages.

| Item | **Default Access Point** | **SASL Access Point** |
| :------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Network | VPC | VPC |
| Protocol | PLAINTEXT | SASL_PLAINTEXT |
| Port | 9092 | Please get the SASL access point information in the **Access Mode** section on the **Basic Info** tab on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka) <br>![](https://main.qcloudimg.com/raw/777d60f973af7b07a3ebf2d41a861b21.png) |
| SASL mechanism | N/A | PLAIN: a simple username and password authentication mechanism |
| Demo | [PLAINTEXT](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/pythonkafkademo/default) | [SASL_PLAINTEXT/PLAIN](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/pythonkafkademo/sasl) |
| Documentation | [Receiving/Sending Message at Default Access Point](https://intl.cloud.tencent.com/document/product/597/40452) | [Receiving/Sending Message at SASL Access Point Through PLAIN Mechanism](https://intl.cloud.tencent.com/document/product/597/40453) |

