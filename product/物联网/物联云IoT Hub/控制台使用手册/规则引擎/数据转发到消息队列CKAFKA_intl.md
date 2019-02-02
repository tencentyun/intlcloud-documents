[//]: # (chinagitpath:XXXXX)

## Overview
The rule engine allows you to configure rules to forward the eligible device-reported data to the [Ckafka](https://cloud.tencent.com/product/CKafka) message queuing service, and then your application server can read the data from Ckafka for processing. This takes advantage of Ckafka's high throughput to create a highly available message linkage for you.  
The figure below shows the entire process of forwarding data to Ckafka by the rule engine:

![avatar](https://main.qcloudimg.com/raw/ae9179db06123982f14857891aeabb8a.png)

## Configuration
1. Log in to the [Rule Engine](https://console.cloud.tencent.com/iotcloud/rules/rule) console page and click the rule you want to configure.
![](https://main.qcloudimg.com/raw/0a0a0e5bc48aa0d4492ac0b8d3c7413c.png))
2. On the rule details page, click the **Add action** button. In the "Add action" window that pops up, select the action "Data forwarding to Ckafka", select the Ckafka instance and topic and click **Create**.
![avatar](https://main.qcloudimg.com/raw/6a4d5306bbaa262eafe9a5fa722419f3.png) 
**Note:** You will be prompted to authorize access to Ckafka upon the first use. You need to click **Authorize access to Ckafka** before you can create.
![avatar](https://main.qcloudimg.com/raw/29340fdc4f0e0fab626b3d122c10c3f1.png) 
![avatar](https://main.qcloudimg.com/raw/0a66a55631655ea584bb502f5e211825.png)
3. After the configuration above is completed, the IoT Hub platform will forward the data reported by the device that meets the rule conditions to the Ckafka instance configured; you can see [Ckafka Getting Started](https://cloud.tencent.com/document/product/597/10112) for more information about how to read data on your own application server for processing.

