## Overview
The rule engine allows you to configure rules to forward eligible data reported by devices to [CKafka](https://intl.cloud.tencent.com/product/CKafka), and then your application server can read the data from CKafka for processing. This takes advantage of CKafka's high throughput to create a highly available message linkage.  

The figure below shows the entire process of forwarding data to CKafka by the rule engine:
![](https://main.qcloudimg.com/raw/dead88cb3fe3a5c986b6522565967193.png)

## Configuration
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Rule Engine** on the left sidebar.
2. Go to the rule engine page and click the rule to be configured.
3. On the rule details page, click **Add Action**.
>?You will be prompted to authorize access to CKafka upon the first use. You need to click **Authorize Access to CKafka** before you can proceed.
![](https://main.qcloudimg.com/raw/d4a20c9118f9989dba7064d13a4e836e.png)
4. In the pop-up **Add Action** window, select **Forward data to CKafka**, CKafka instance, and topic and click **Save**.
![avatar](https://main.qcloudimg.com/raw/b2f2b7e9da1d69b98762e28718afbd14.png) 
5. After the above configuration is completed, IoT Hub will forward eligible data reported by devices to the configured CKafka instance. You can refer to [Process Overview](https://intl.cloud.tencent.com/document/product/597/40039) to read and process the data on your own application server.



## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:
- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the "action for forwarding failure", then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.
