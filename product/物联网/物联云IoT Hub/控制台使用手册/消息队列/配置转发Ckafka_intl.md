[//]: # (chinagitpath:XXXXX)

## Authorizing Access to CKafka
If the IoT Hub account is using CKafka for the first time, the **Authorize access to CKafka** button will be displayed. Click it to authorize and enter the message queue configuration page.
![](https://main.qcloudimg.com/raw/18ebabb52a1e61270193e87edee1feda.png)

## Configuring Message Queue
### Configuring Push Type
There are two types of messages configured for CKafka: "device-reported message" and "device status change notification". After selecting the message type as needed, click the **Activate Now** button and a confirmation window will pop up. After **OK** is clicked, IoT Hub will immediately push the selected type of messages to the default queue ```topic-iot-{productID}```.
> **Note:**
> 
> 1. The message type cannot be empty;
> 2. The modified message type cannot be the same as the last configured one.

### Configuring Push Instance
Select the instance you want to push. If the current account has no instances, go to [CKafka Console](https://console.cloud.tencent.com/ckafka) to purchase and create instances. After the creation is successful, the message queue page will display the details of the subscription. You can also modify the subscribed message type and instance type on this page, as shown in the red box below.

![](https://main.qcloudimg.com/raw/a1c77802fe5f4faefabebfbff5eb4979.png)


After the creation is successful, the message queue page will display the details of the subscription. You can also modify the subscribed message type and push instances on this page.
![](https://main.qcloudimg.com/raw/3f345181b089fdc96e25327f5b8807ec.png)

![](https://main.qcloudimg.com/raw/9bca2d06398c2bc0802a52989d6f78b6.png)

## Deleting Message Queue
Click **Delete Current Configuration** to delete the current message queue configuration.
![](https://main.qcloudimg.com/raw/a94cd916a39715edb1118dd01fa4cf02.png)


## CKafka SDK for Receiving Messages
For more information about how to use the message queue SDK, see the provided [Getting Started](https://cloud.tencent.com/document/product/597/10112).

