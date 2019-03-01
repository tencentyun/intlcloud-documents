[//]: # (chinagitpath:XXXXX)

## 1. Application Scenarios and Features
- You have a LoRa chip, which reports and sends data between the device and the application platform and forwards the data to Tencent Cloud components for storage, distribution and analysis.  
- You only need to configure in the IoT Hub, obtain LoRa communication-related information and configure to the LoRa device. Then you can connect to the LoRa gateway deployed by Tencent in Shenzhen.
![Data flow](https://main.qcloudimg.com/raw/e8fd5d1c2bc162c9d0dd618553fb570a/LoRa_freamwork.png)

## 2. Procedures
### 2.1 Create a LoRa product and device
1. Go to the [Console](https://console.cloud.tencent.com/iotcloud) to create a LoRa product.  
![](https://main.qcloudimg.com/raw/f6e66177d91dad72cd423cdd714e0197/LoRa_product.png)
2. After successful creation, you can view the basic information of the product.  
![](https://main.qcloudimg.com/raw/28d192fec91cf730402391393c154318/LoRa_product_info.png)
3. Create a device (testLoRa1) in the **Device List** to return communication-related information.  
![](https://main.qcloudimg.com/raw/d54cba5ea51a16a508f3c47c6f5de3c3/LoRa_device.png)
![](https://main.qcloudimg.com/raw/33bd588f15bd7dd2f0fffa929bb16b81/LoRa_device_info.png)
4. Click **Manage** to query the device details.  
![](https://main.qcloudimg.com/raw/0aa423f1542beaa415e549fb233e5a6e/LoRa_device_info_m.png)

### 2.2 Create a rule engine
In this example, the reported data is forwarded to your application platform using HTTP POST requests with JSON packets.  
The rule engine also supports forwarding to Tencent Cloud's storage components and message queues.  
![](https://main.qcloudimg.com/raw/26acf7aa274fe686e857fda1e70b98d2/NB-IoT_forward_app.png)  
For detailed steps, see [Rule Engine Details](https://cloud.tencent.com/document/product/634/14446).
### 2.3 Create a gateway product and device
Creating gateway products and devices is similar to creating LoRa products and devices. For details, see [Creating a LoRa Product and Device](https://cloud.tencent.com/document/product/634/30210#2.1-.E5.88.9B.E5.BB.BA-lora-.E4.BA.A7.E5.93.81.E5.92.8C.E8.AE.BE.E5.A4.87).
### 2.4 Bind the gateway with LoRa
1. Go to the **Console** > **Product List** and click **Sub-products** on the gateway product.  
![](https://main.qcloudimg.com/raw/f9bb294a9e4b83b78b14aef60f54a8db/Gateway_sub_product.png)
2. Click **Add a Sub-product** and select the LoRa product just created.  
![](https://main.qcloudimg.com/raw/0b660fb0d3e8e1233426a6fc878b2301/Gateway_add_lora_product.png)
3. On the gateway device in the **Device List**, click **Sub-devices** > **Add a Sub-device** and select the LoRa device just created.  
![](https://main.qcloudimg.com/raw/7a52e633c5d3510637c1ff2e5bb5d329/Gateway_device_add_lora_device.png)
### 2.5 Grant publishing and subscribing permissions to the gateway
After binding gateway with LoRa, a gateway permission list set up is necessary for gateway to send LoRa messages.
Add the Plora/+/+/event publishing permission and Plora/+/+/control subscribing permission.
![](https://main.qcloudimg.com/raw/5e4bf8b2d4ad502a7bee7705eca85688/Gateway_topic_policy.png)
### 2.6 Access the device
After completing the configuration above, you can obtain the basic information of LoRaWAN communication such as DevEUI, AppKey, NwkKey and AppEUI and then connect to the LoRa network deployed by Tencent in Shenzhen.

