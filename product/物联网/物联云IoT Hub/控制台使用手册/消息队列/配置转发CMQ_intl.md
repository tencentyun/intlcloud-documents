[//]: # (chinagitpath:XXXXX)

## Authorizing Access to CMQ
If the IoT Hub account is using CMQ for the first time, the **Authorize access to CMQ** button will be displayed. Click it to authorize and enter the message queue configuration page.
![](https://main.qcloudimg.com/raw/1a0c70c7b450606a2a36126729ca94bb.png)

## Configuring Message Queue
There are two types of messages configured for CMQ: "device-reported message" and "device status change notification". After selecting the message type as needed, click the **Save Configuration** button and a confirmation window will pop up. Click **OK** and IoT Hub will push the selected type of messages to the default queue ```queue-iot-{productID}```.
> **Note:**
> 
> 1. The message type cannot be empty;
> 2. The modified message type cannot be the same as the last configured one.

![](https://main.qcloudimg.com/raw/6cd86325e42790cc56c3e9447ceb0caa.png)
After the creation is successful, the message queue page will display the details of the subscription. You can also modify the subscribed message type on this page.
![](https://main.qcloudimg.com/raw/d3c09f0b71dbc4ff09d5af4305218626.png)

## Deleting Message Queue
Click **Delete Current Configuration** to delete current message queue configuration.
![](https://main.qcloudimg.com/raw/a94cd916a39715edb1118dd01fa4cf02.png)

## CMQ SDK for Receiving Messages
- CMQ provides the following two APIs to **read messages from the queue**:
    [ReceiveMessage](https://cloud.tencent.com/document/product/406/5839): Read one message from the queue at a time.
    [BatchReceiveMessage](https://cloud.tencent.com/document/product/406/5924): Read multiple messages from the queue at a time.
    
- After reading a message in the message queue, you need to actively **delete the message** to remove it from the queue:   
    [DeleteMessage](https://cloud.tencent.com/document/api/406/5840): Delete one message from the queue.
    [BatchDeleteMessage](https://cloud.tencent.com/document/api/406/5841): Delete multiple (up to 16) messages from the queue at a time.
    
For more information about how to use the SDK demo of the message queue, see the provided [SDK demo](https://cloud.tencent.com/document/product/406/6107).

