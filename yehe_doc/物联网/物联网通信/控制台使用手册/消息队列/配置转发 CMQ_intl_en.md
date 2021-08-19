

## Overview
This document describes how to authorize access to and configure CMQ.

## Prerequisites
The IoT Hub account must never have used CMQ.

## Directions
### Authorizing access
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iothub), select **Products** > **Message Queue**, and click **Authorize Access to CMQ**.
2. After successful authorization, you will be redirected to the message queue configuration page.
![](https://main.qcloudimg.com/raw/c27554c0ba6f9a65f88c63a9804c6786.png)

### Configuring message queue
1. On the message queue configuration page, select the message type as needed. CMQ has the following two message types.
 - Device-reported message
 - Device status change notification
2. After selecting the message type, select the CMQ region and queue and click **Save**.
3. A confirmation window will pop up. After you click **Confirm**, IoT Hub will push the selected type of messages to the selected queue (if you don't select any queue, the default queue `queue-iot-{productID}` will be used).


>!
- The message type cannot be empty.
- The modified message type cannot be the same as the last configured one.
- After successful creation, the message queue page will display the details of the subscription. You can also modify the subscribed message type on this page.

### Deleting message queue
To delete the current message queue configuration, click **Delete**.


## Relevant Information
#### SDK introduction
The relevant CMQ SDK features for receiving messages are as described below:
CMQ provides the following two APIs to **read messages from the queue**:
- [ReceiveMessage](https://intl.cloud.tencent.com/document/product/406/5839): reads one message from the queue at a time.
- [BatchReceiveMessage](https://intl.cloud.tencent.com/document/product/406/5924): reads multiple messages from the queue at a time.

After a message in the message queue is read, you need to actively delete it before it can be removed from the message queue:
- [DeleteMessage](https://intl.cloud.tencent.com/zh/document/product/406/5836): deletes one message from the queue.
- [BatchDeleteMessage](https://intl.cloud.tencent.com/document/product/406/8407): deletes multiple (up to 16) messages from the queue at a time.

For more information on how to use the CMQ SDK demo, please see [HTTP SDK](https://intl.cloud.tencent.com/document/product/406/6107).

