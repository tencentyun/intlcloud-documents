[//]: # (chinagitpath:XXXXX)

## Overview
The rule engine allows rule configuration and can forward eligible device-reported data to the message queuing service [Ckafka](https://cloud.tencent.com/product/CKafka). Your application server can then read data in Ckafka and process data. Ckafka's strong handling capacity is leveraged to enable accessible communication.
The figure below shows the entire process of forwarding data to Ckafka by the rule engine:

![avatar](https://main.qcloudimg.com/raw/ae9179db06123982f14857891aeabb8a.png)

## Configuration
1. Log in to the [Rule Engine](https://console.cloud.tencent.com/iotcloud/rules/rule) console page and click the rule you want to configure.
![](https://main.qcloudimg.com/raw/0a0a0e5bc48aa0d4492ac0b8d3c7413c.png))
2. On the rule details page, click the **Add action** button. In the pop-up "Add action" window, select the action "Data forwarding to Ckafka", select the Ckafka instance and topic and click **Create**.
![avatar](https://main.qcloudimg.com/raw/6a4d5306bbaa262eafe9a5fa722419f3.png) 
**Notes:** When using the feature for the first time, you will be prompted to Ckafka access authorization. You need to click **Authorize access to Ckafka** before creation.
![avatar](https://main.qcloudimg.com/raw/29340fdc4f0e0fab626b3d122c10c3f1.png) 
![avatar](https://main.qcloudimg.com/raw/0a66a55631655ea584bb502f5e211825.png)
3. After the above configurations, the IoT Hub will forward eligible device-reported data to user-configred Ckafka. To know more about how to read data from your application server for processing, read: [Ckafka Getting Started](https://cloud.tencent.com/document/product/597/10112) for more information about how to read data on your own application server for processing.

