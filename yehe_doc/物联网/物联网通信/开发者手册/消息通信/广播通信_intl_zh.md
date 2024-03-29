

## 功能概述

物联网通信平台提供了广播通信 Topic，服务器通过调用广播通信 API 发布广播消息，同一产品下订阅了广播 Topic 的在线设备便可收到服务器通过广播 Topic 发布的广播消息。
![](https://main.qcloudimg.com/raw/9555398a506ede980f72e550512082bb.png)


## 广播 Topic

广播通信的 Topic 内容为：``$broadcast/rxd/${ProductId}/${DeviceName}``其中`${ProductId}与${DeviceName}`代表具体的产品 ID 和设备名称的内容。

## 广播通信示例

示例为基于 Linux 平台利用设备端 [C-SDK](https://intl.cloud.tencent.com/document/product/1105/41840) 完成接入，并结合腾讯云 [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=PublishBroadcastMessage&SignVersion=) 工具完成接口的调用，具体使用步骤如下。

### 控制台创建设备

#### 场景说明

- 用户有多个空调设备接入物联网通信平台，则需要服务器向所有的空调设备发送一条相同的指令来关闭空调。
- 服务器调用PublishBroadcastMessage接口，指定产品`ProductId`和广播消息`Payload`，该产品订阅了所有广播 Topic 的在线设备就会收到消息内容为`Payload`的广播消息。


#### 创建产品和设备

请参考 [设备互通](https://intl.cloud.tencent.com/document/product/1105/41467) 文档创建空调产品，并依次创建 airConditioner1，airConditioner2 等多个空调设备。


### 编译运行示例程序（以密钥认证设备为例）

#### 1. 编译 SDK

修改 CMakeLists.txt 确保以下选项存在：

```
set(BUILD_TYPE                   "release")
set(COMPILE_TOOLS                "gcc") 
set(PLATFORM 	                 "linux")
set(FEATURE_MQTT_COMM_ENABLED ON)
set(FEATURE_BROADCAST_ENABLED ON)
set(FEATURE_AUTH_MODE "KEY")
set(FEATURE_AUTH_WITH_NOTLS OFF)
set(FEATURE_DEBUG_DEV_INFO_USED  OFF)
```

执行脚本编译：

```
./cmake_build.sh 
```

示例输出`broadcast_sample`位于`output/release/bin`文件夹中。

#### 2. 填写设备信息

将上面创建的 airConditioner1 设备的设备信息填写到一个 JSON 文件`aircond_device_info1.json`中：

```
{
    "auth_mode":"KEY",	
    "productId":"KL4J2****8",
    "deviceName":"airConditioner1",	
    "key_deviceinfo":{    
        "deviceSecret":"zOZXUaycuwlePt****8dBA=="
    }
}
```

将 airConditioner2 的设备信息填写到一个 JSON 文件`aircond_device_info2.json`中：

```
{
    "auth_mode":"KEY",	
    "productId":"KL4J2****8",
    "deviceName":"airConditioner2",	
    "key_deviceinfo":{    
        "deviceSecret":"+IiVNsyKRh0AW****IE07A=="
    }
}
```

依次将其他的设备信息填到对应的 JSON 文件。

#### 3. 执行`broadcast_sample`示例程序

因为该场景涉及到多个 sample 同时运行，可以打开多个终端运行`broadcast_sample`示例，看到所有的示例都订阅了`$broadcast/rxd/${productID}/${deviceName}`主题，并处于等待状态。
设备 airConditioner1 输出如下：

```
./broadcast_sample -c ./aircond_device_info1.json -l 100
INF|2020-08-03 22:50:28|qcloud_iot_device.c|iot_device_info_set(50): SDK_Ver: 3.2.0, Product_ID: KL4J2****8, Device_Name: airConditioner1
DBG|2020-08-03 22:50:28|HAL_TLS_mbedtls.c|HAL_TLS_Connect(200): Setting up the SSL/TLS structure...
DBG|2020-08-03 22:50:28|HAL_TLS_mbedtls.c|HAL_TLS_Connect(242): Performing the SSL/TLS handshake...
DBG|2020-08-03 22:50:28|HAL_TLS_mbedtls.c|HAL_TLS_Connect(243): Connecting to /KL4J2****8.iotcloud.tencentdevices.com/8883...
INF|2020-08-03 22:50:28|HAL_TLS_mbedtls.c|HAL_TLS_Connect(265): connected with /KL4J2****8.iotcloud.tencentdevices.com/8883...
INF|2020-08-03 22:50:28|mqtt_client.c|IOT_MQTT_Construct(113): mqtt connect with id: 9**** success
INF|2020-08-03 22:50:28|broadcast_sample.c|main(197): Cloud Device Construct Success
DBG|2020-08-03 22:50:28|mqtt_client_subscribe.c|qcloud_iot_mqtt_subscribe(142): topicName=$broadcast/rxd/KL4J2****8/airConditioner1|packet_id=*****
INF|2020-08-03 22:50:28|broadcast_sample.c|_mqtt_event_handler(49): subscribe success, packet-id=*****
DBG|2020-08-03 22:50:28|broadcast.c|_broadcast_event_callback(37): broadcast topic subscribe success
```

设备 airConditioner2 输出如下：

```
./broadcast_sample -c ./aircond_device_info2.json -l 100
INF|2020-08-03 22:51:24|qcloud_iot_device.c|iot_device_info_set(50): SDK_Ver: 3.2.0, Product_ID: KL4J2****8, Device_Name: airConditioner2
DBG|2020-08-03 22:51:24|HAL_TLS_mbedtls.c|HAL_TLS_Connect(200): Setting up the SSL/TLS structure...
DBG|2020-08-03 22:51:24|HAL_TLS_mbedtls.c|HAL_TLS_Connect(242): Performing the SSL/TLS handshake...
DBG|2020-08-03 22:51:24|HAL_TLS_mbedtls.c|HAL_TLS_Connect(243): Connecting to /KL4J2****8.iotcloud.tencentdevices.com/8883...
INF|2020-08-03 22:51:24|HAL_TLS_mbedtls.c|HAL_TLS_Connect(265): connected with /KL4J2****8.iotcloud.tencentdevices.com/8883...
INF|2020-08-03 22:51:25|mqtt_client.c|IOT_MQTT_Construct(113): mqtt connect with id: f**** success
INF|2020-08-03 22:51:25|broadcast_sample.c|main(197): Cloud Device Construct Success
DBG|2020-08-03 22:51:25|mqtt_client_subscribe.c|qcloud_iot_mqtt_subscribe(142): topicName=$broadcast/rxd/KL4J2****8/airConditioner2|packet_id=*****
INF|2020-08-03 22:51:25|broadcast_sample.c|_mqtt_event_handler(49): subscribe success, packet-id=******
DBG|2020-08-03 22:51:25|broadcast.c|_broadcast_event_callback(37): broadcast topic subscribe success
```

#### 4. 调用云API `PublishBroadcastMessage` 发送广播消息

打开腾讯云 [API 控制台](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=PublishBroadcastMessage&SignVersion=)，填写个人密钥和设备参数信息，选择在线调用并发送请求。


#### 5. 观察空调设备的消息接收

观察设备 airConditioner1 的打印输出，可以看到已经收到服务器发送的消息。

```plaintext
DBG|2020-08-03 22:55:32|broadcast.c|_broadcast_message_cb(25): topic=$broadcast/rxd/KL4J2****8/airConditioner1
INF|2020-08-03 22:55:32|broadcast.c|_broadcast_message_cb(26): len=6, topic_msg=closed
INF|2020-08-03 22:55:32|broadcast_sample.c|_broadcast_message_handler(134): broadcast message=closed
```

观察设备 airConditioner2 的打印输出，可以看到同时收到服务器发送的消息。

```plaintext
DBG|2020-08-03 22:55:32|broadcast.c|_broadcast_message_cb(25): topic=$broadcast/rxd/KL4J2****8/airConditioner2
INF|2020-08-03 22:55:32|broadcast.c|_broadcast_message_cb(26): len=6, topic_msg=closed
INF|2020-08-03 22:55:32|broadcast_sample.c|_broadcast_message_handler(134): broadcast message=closed
```

#### 6. 空调设备关闭

接收到指令的设备解析指令进行处理。




