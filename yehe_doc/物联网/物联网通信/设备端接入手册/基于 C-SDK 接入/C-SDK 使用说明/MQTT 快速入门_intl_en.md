This document describes how to create devices and permissions in the IoT Hub console and quickly try out device connection to IoT Hub over the MQTT protocol for message sending and receiving based on the **mqtt_sample** of the C-SDK.

## Operations in Console

### Creating product and device
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Products** on the left sidebar.
2. On the product list page, click **Create Product**.
3. On the pop-up product adding page, select the node type and product type, enter the product name, select the authentication method and data format, and enter the product description.
Then, click **Confirm** (select as shown below for directly connected general devices).
![](https://main.qcloudimg.com/raw/1c76747cd324aa3b25810f055cd1bf1a.jpg)
4. After the product is created, click **Devices** at the bottom of the generated product page.
5. On the device list page, click **Add Device**.
 - If the authentication method is certificate authentication, after the device name is entered, be sure to click **Download** in the pop-up window. The device key and device certificate in the downloaded package are used for authenticating the device during connection to IoT Hub.
![](https://main.qcloudimg.com/raw/d49979433cab6852b2919f049e818a5c.png)
 - If the authentication method is key authentication, after the device name is entered, the key of the added device will be displayed in the pop-up window.
![](https://main.qcloudimg.com/raw/b544ebdd175993147a71a4dfe2af2b80.jpg)





### Creating topic
1. On the generated product page, click **Permissions**.
2. On the permission list page, click **Add Topic Permission**.
3. In the topic permission pop-up window, enter `data`, set the operation permission to **Subscribe and Publish**, and click **Confirm**.
![](https://main.qcloudimg.com/raw/1a7fdffc12b9154e6455e7c2cbdecc22.jpg)
4. Then, the `productID/\${deviceName}/data` topic will be created, and you can view all permissions of the product in the permission list on the product page.


## Compiling and Running Demo

The following describes how to compile and run the `mqtt_sample` demo in the Linux environment (with a key-authenticated device as example).

#### 1. Compile the SDK
(1) Modify `CMakeLists.txt` to ensure that the following options exist:
```
set(BUILD_TYPE                   "release")
set(COMPILE_TOOLS                "gcc") 
set(PLATFORM 	                "linux")
set(FEATURE_MQTT_COMM_ENABLED ON)
set(FEATURE_AUTH_MODE "KEY")
set(FEATURE_AUTH_WITH_NOTLS OFF)
set(FEATURE_DEBUG_DEV_INFO_USED  OFF)
```
(2) Run the following script for compilation.
```
./cmake_build.sh 
```
(3) The demo output is in the `output/release/bin` folder.

#### 2. Enter the device information
Enter the information of the device created above on the IoT Hub platform in `device_info.json`.
```
"auth_mode":"KEY",	
"productId":"S3EUVBRJLB",
"deviceName":"test_device",	
"key_deviceinfo":{    
"deviceSecret":"vX6PQqazsGsMyf5SMfs6OA6y"
    }
```

#### 3. Run the `mqtt_sample` demo
```
./output/release/bin/mqtt_sample 
INF|2019-09-12 21:28:20|device.c|iot_device_info_set(67): SDK_Ver: 3.1.0, Product_ID: S3EUVBRJLB, Device_Name: test_device
DBG|2019-09-12 21:28:20|HAL_TLS_mbedtls.c|HAL_TLS_Connect(204): Setting up the SSL/TLS structure...
DBG|2019-09-12 21:28:20|HAL_TLS_mbedtls.c|HAL_TLS_Connect(246): Performing the SSL/TLS handshake...
DBG|2019-09-12 21:28:20|HAL_TLS_mbedtls.c|HAL_TLS_Connect(247): Connecting to /S3EUVBRJLB.iotcloud.tencentdevices.com/8883...
INF|2019-09-12 21:28:20|HAL_TLS_mbedtls.c|HAL_TLS_Connect(269): connected with /S3EUVBRJLB.iotcloud.tencentdevices.com/8883...
INF|2019-09-12 21:28:20|mqtt_client.c|IOT_MQTT_Construct(125): mqtt connect with id: p8t0W success
INF|2019-09-12 21:28:20|mqtt_sample.c|main(303): Cloud Device Construct Success
DBG|2019-09-12 21:28:20|mqtt_client_subscribe.c|qcloud_iot_mqtt_subscribe(138): topicName=$sys/operation/result/S3EUVBRJLB/test_device|packet_id=1932
INF|2019-09-12 21:28:20|mqtt_sample.c|_mqtt_event_handler(71): subscribe success, packet-id=1932
DBG|2019-09-12 21:28:20|system_mqtt.c|_system_mqtt_sub_event_handler(80): mqtt sys topic subscribe success
DBG|2019-09-12 21:28:20|mqtt_client_publish.c|qcloud_iot_mqtt_publish(337): publish packetID=0|topicName=$sys/operation/S3EUVBRJLB/test_device|payload={"type": "get", "resource": ["time"]}
DBG|2019-09-12 21:28:20|system_mqtt.c|_system_mqtt_message_callback(63): Recv Msg Topic:$sys/operation/result/S3EUVBRJLB/test_device, payload:{"type":"get","time":1568294900}
INF|2019-09-12 21:28:21|mqtt_sample.c|main(316): system time is 1568294900
DBG|2019-09-12 21:28:21|mqtt_client_subscribe.c|qcloud_iot_mqtt_subscribe(138): topicName=S3EUVBRJLB/test_device/data|packet_id=1933
INF|2019-09-12 21:28:21|mqtt_sample.c|_mqtt_event_handler(71): subscribe success, packet-id=1933
DBG|2019-09-12 21:28:21|mqtt_client_publish.c|qcloud_iot_mqtt_publish(329): publish topic seq=1934|topicName=S3EUVBRJLB/test_device/data|payload={"action": "publish_test", "count": "0"}
INF|2019-09-12 21:28:21|mqtt_sample.c|_mqtt_event_handler(98): publish success, packet-id=1934
INF|2019-09-12 21:28:21|mqtt_sample.c|on_message_callback(195): Receive Message With topicName:S3EUVBRJLB/test_device/data, payload:{"action": "publish_test", "count": "0"}
INF|2019-09-12 21:28:22|mqtt_client_connect.c|qcloud_iot_mqtt_disconnect(437): mqtt disconnect!
INF|2019-09-12 21:28:22|system_mqtt.c|_system_mqtt_sub_event_handler(98): mqtt client has been destroyed
INF|2019-09-12 21:28:22|mqtt_client.c|IOT_MQTT_Destroy(186): mqtt release!
```

#### 4. Observe message sending
The following log information shows that the demo reported data to `/{productID}/{deviceName}/data` through the `Publish` message type of MQTT, and that the server received and successfully processed the message. 
```
INF|2019-09-12 21:28:21|mqtt_sample.c|_mqtt_event_handler(98): publish success, packet-id=1934
```

#### 5. Observe message receiving
The following log information shows that as the message reached the subscribed topic, it was pushed to the demo as-is by the server and entered the corresponding callback function.
```
INF|2019-09-12 21:28:21|mqtt_sample.c|on_message_callback(195): Receive Message With topicName:S3EUVBRJLB/test_device/data, payload:{"action": "publish_test", "count": "0"}
```

#### 6. Observe logs in the console
Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud), click the product name, and click **Cloud Log** on the top to view the message just reported.
![](https://main.qcloudimg.com/raw/c6f7b9b71a96a1efc7611f38871c0ea0.jpg)




