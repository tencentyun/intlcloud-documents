
## Overview
This document describes how to authorize access to and configure CKafka.

## Prerequisites
The IoT Hub account must never have used CKafka.

## Directions
### Authorizing access
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud), select **Products** > **Message Queue**, and click **Authorize Access to CKafka**.
2. After successful authorization, you will be redirected to the message queue configuration page.
![](https://main.qcloudimg.com/raw/ba7aebeffc47ddc6af091548999898cc.png)

### Configuring message queue
#### Configuring push type
1. On the message queue configuration page, select the message type as needed. CKafka has the following two message types.
  - Device-reported message
  - Device status change notification
2. After selecting the message type, select the CKafka instance and topic and click **Save**.
3. A confirmation window will pop up. After you click **Confirm**, IoT Hub will immediately push the selected type of messages to the selected topic.

>! 
- The message type cannot be empty.
- The modified message type cannot be the same as the last configured one.

 

#### Configuring push instance
>?If the current account has no instances, go to the [CKafka console](https://console.cloud.tencent.com/ckafka) to purchase and create one.

1. On the message queue page, select the instance for push.
2. After the instance is successfully created, the message queue page will display the details of the subscription.
3. On the message queue page, you can click **Modify Message Type** and **Modify Instance Type** to modify the subscribed message type and instance type.




### Deleting message queue
To delete the current message queue configuration, click **Delete**.


## Relevant Information
For more information on how to use the CKafka SDK, please see [Process Overview](https://intl.cloud.tencent.com/document/product/597/40039).
