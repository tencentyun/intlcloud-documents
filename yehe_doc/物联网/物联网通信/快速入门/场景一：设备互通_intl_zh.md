
## 操作场景
假设一个智能家居的场景（非实际产品，仅用于阐述物联网通信功能），如需实现如下图功能，您可以参考本文档进行操作。
![come_home](https://main.qcloudimg.com/raw/7a705176f8cba804b72d1e4519e93151.png)


## 解决方案
基于腾讯物联网通信，我们可以通过 SDK 创建两类智能设备（Door、AirConditioner），基于设备间的消息和规则引擎实现设备之间的联动，如下图所示：
![rule_engine_for_smart_home](https://main.qcloudimg.com/raw/f4c5186f03f8636eb8f8d80622b49b02.png)


>! airConditioner1 不可以通过直接订阅 door1 的 update 消息来完成消息通信，原因请参考 [功能组件 > 权限管理](https://intl.cloud.tencent.com/document/product/1105/41500) 。


## 操作步骤
### 创建门产品和设备
1. 登录 [物联网通信控制台](https://console.cloud.tencent.com/iotcloud)，单击左侧菜单栏【产品列表】。
2. 进入产品列表页，单击【创建新产品】。
3. 创建产品（Door）并根据需要选择认证方式，输入产品描述，单击【确定】。
![](https://main.qcloudimg.com/raw/09278773f9519493fe9a4568a3fdf72a.png)
4. 创建成功后，可以查看产品的基本信息。
5. 单击进入（Door）产品，选择【设备列表】子页面，创建设备（door1）。
>!在非对称加密类型下创建设备会返回设备密钥，此密钥用于设备通信，并且不会在物联网通信后台存储，请妥善保管。
6. 单击【管理】，可查询设备详情。
 - 证书认证类型：
 ![查询设备](https://main.qcloudimg.com/raw/09f9d0410c549ec14d3ca5aa4b5d3e05.png)
 - 密钥认证类型：
 ![查询设备](https://main.qcloudimg.com/raw/ec3689bef07ee4ed30b6e06741be6a0a.png)
	
	
### 创建空调产品和设备
1. 登录 [物联网通信控制台](https://console.cloud.tencent.com/iotcloud)，单击左侧菜单栏【产品列表】。
2. 进入产品列表页，单击【创建新产品】
3. 创建空调产品（AirConditioner），并根据需要选择认证方式，输入产品描述，单击【确定】。
![](https://main.qcloudimg.com/raw/a5cd89c2416d52d5644184102e13fc8c.png)
4. 创建成功后，可以查看产品的基本信息。
5. 在【设备列表】下，创建设备（airConditioner1）。
6. 单击【管理】，可查询设备详情。
![查询设备](https://main.qcloudimg.com/raw/49b0f103c397322acafb8490f26205d7.png)
   

查询设备详情页面，设备证书、设备私钥用于 MQTT 的 TLS 非对称加密；对称密钥用于对称加密通信（两种通信方式差别请参考 [功能组件 > 设备接入](https://intl.cloud.tencent.com/document/product/1105/41500）。


>!以上资源的创建可通过 restAPI 由后台创建，具体请参见API 概览。

### 创建规则引擎
具体步骤请参考 [规则引擎概述](https://intl.cloud.tencent.com/document/product/1105/41484)。

### 下载 SDK
SDK 下载方式请参考 [SDK 下载](https://intl.cloud.tencent.com/document/product/1105/41840)。

### 编译运行 C SDK 示例

C SDK 示例程序
- samples/scenarized/door_mqtt_sample.c 是门设备基于 MQTT 协议相关逻辑代码。
- samples/scenarized/aircond_shadow_sample.c 是空调设备基于 MQTT 协议相关逻辑代码。

以**密钥认证设备**为例，在 Linux 环境编译运行设备互通的示例程序。

#### 1. 编译 SDK
修改 CMakeLists.txt，确保以下选项存在：
```plaintext
set(BUILD_TYPE                   "release")
set(COMPILE_TOOLS                "gcc") 
set(PLATFORM 	                "linux")
set(FEATURE_MQTT_COMM_ENABLED ON)
set(FEATURE_MQTT_DEVICE_SHADOW ON)
set(FEATURE_AUTH_MODE "KEY")
set(FEATURE_AUTH_WITH_NOTLS OFF)
set(FEATURE_DEBUG_DEV_INFO_USED  OFF)
```
执行以下脚本编译：
```plaintext
./cmake_build.sh 
```
示例输出 aircond_shadow_sample 和 door_mqtt_sample 位于`output/release/bin`文件夹中。

#### 2. 填写设备信息
将上面创建的 airConditioner1 设备的设备信息，填写到一个 JSON 文件 aircond_device_info.json 中。
```plaintext
"auth_mode":"KEY",	
"productId":"GYT9V6D4AF",
"deviceName":"airConditioner1",	
"key_deviceinfo":{    
		"deviceSecret":"vXeds12qazsGsMyf5SMfs6OA6y"
}
```
再将 door1 设备的设备信息，填写到另一个 JSON 文件 door_device_info.json 中。
```plaintext
"auth_mode":"KEY",	
"productId":"S3EUVBRJLB",
"deviceName":"door1",	
"key_deviceinfo":{    
		"deviceSecret":"i92E3QMNmxi5hvIxUHjO8gTdg"
}
```

#### 3. 执行 aircond_shadow_sample 示例程序
在 aircond_shadow_sample 的代码里面，`_register_subscribe_topics` 实现了对主题 /{productID}/{deviceName}/control 的订阅，并且注册对应的回调处理函数。收到该 topic 消息后，判断消息内容是 “come_home” 或者 “leave_home” 而分别让 airConditioner 开启或者关闭。`_simulate_room_temperature` 则简单模拟了下室内温度的变化和 airConditioner 的能耗。用户也可以实现其他自定义逻辑。

因为设备互通场景涉及到两个 sample 同时运行，可以先在当前终端 console 运行空调示例，可以看到示例订阅了主题，然后就处于循环等待状态，空调的初始状态是 close 关闭状态：
```plaintext
 ./output/release/bin/aircond_shadow_sample -c ./device_info.json
INF|2019-09-16 23:25:17|device.c|iot_device_info_set(67): SDK_Ver: 3.1.0, Product_ID: GYT9V6D4AF, Device_Name: airConditioner1
INF|2019-09-16 23:25:19|mqtt_client.c|IOT_MQTT_Construct(125): mqtt connect with id: Nh9Vc success
DBG|2019-09-16 23:25:19|mqtt_client_subscribe.c|qcloud_iot_mqtt_subscribe(138): topicName=$shadow/operation/result/GYT9V6D4AF/airConditioner1|packet_id=56171
DBG|2019-09-16 23:25:19|shadow_client.c|_shadow_event_handler(63): shadow subscribe success, packet-id=56171
INF|2019-09-16 23:25:19|aircond_shadow_sample.c|event_handler(96): subscribe success, packet-id=56171
INF|2019-09-16 23:25:19|shadow_client.c|IOT_Shadow_Construct(172): Sync device data successfully
INF|2019-09-16 23:25:19|aircond_shadow_sample.c|main(256): Cloud Device Construct Success
DBG|2019-09-16 23:25:19|mqtt_client_subscribe.c|qcloud_iot_mqtt_subscribe(138): topicName=GYT9V6D4AF/airConditioner1/control|packet_id=56172
DBG|2019-09-16 23:25:19|shadow_client.c|_shadow_event_handler(63): shadow subscribe success, packet-id=56172
INF|2019-09-16 23:25:19|aircond_shadow_sample.c|event_handler(96): subscribe success, packet-id=56172
INF|2019-09-16 23:25:19|aircond_shadow_sample.c|main(291): airConditioner state: close
INF|2019-09-16 23:25:19|aircond_shadow_sample.c|main(292): currentTemperature: 32.000000, energyConsumption: 0.000000
```

#### 4. 执行 door_mqtt_sample 示例程序，模拟回家事件
打开另一个终端 console，运行门的示例，根据程序启动参数"-t airConditioner1 -a come_home"，可以看到示例往 /{productID}/{deviceName}/event 主题发送了 JSON 消息 {"action": "come_home", "targetDevice": "airConditioner1"}，表示将回家的消息通知目标设备 airConditioner1。

```plaintext
./output/release/bin/door_mqtt_sample -c  ./output/release/bin/device_info.json -t airConditioner1 -a come_home
INF|2019-09-16 23:29:11|device.c|iot_device_info_set(67): SDK_Ver: 3.1.0, Product_ID: S3EUVBRJLB, Device_Name: door1
INF|2019-09-16 23:29:11|mqtt_client.c|IOT_MQTT_Construct(125): mqtt connect with id: d89Wh success
INF|2019-09-16 23:29:11|door_mqtt_sample.c|main(229): Cloud Device Construct Success
DBG|2019-09-16 23:29:11|mqtt_client_publish.c|qcloud_iot_mqtt_publish(329): publish topic seq=46683|topicName=S3EUVBRJLB/door1/event|payload={"action": "come_home", "targetDevice": "airConditioner1"}
INF|2019-09-16 23:29:11|door_mqtt_sample.c|main(246): Wait for publish ack
INF|2019-09-16 23:29:11|door_mqtt_sample.c|event_handler(81): publish success, packet-id=46683
```

#### 5. 观察空调设备的消息接收，模拟消息响应
观察 aircond_shadow_sample 的打印输出，可以看到已经收到由云端转发的 door1 发送的回家消息，并且将状态`state`由"close"转为"open"，室温`currentTemperature`（往缺省配置温度调整）与能耗`energyConsumption`也有相关动态变化。
```plaintext
INF|2019-09-16 23:29:11|aircond_shadow_sample.c|main(291): airConditioner state: close
INF|2019-09-16 23:29:11|aircond_shadow_sample.c|main(292): currentTemperature: 32.000000, energyConsumption: 0.000000
INF|2019-09-16 23:29:12|aircond_shadow_sample.c|on_message_callback(140): Receive Message With topicName:GYT9V6D4AF/airConditioner1/control, payload:{"action":"come_home","targetDevice":"airConditioner1"}
INF|2019-09-16 23:29:12|aircond_shadow_sample.c|main(291): airConditioner state: open
INF|2019-09-16 23:29:12|aircond_shadow_sample.c|main(292): currentTemperature: 31.000000, energyConsumption: 1.000000
```

### 配置 Android SDK 示例程序

#### 实现 Android SDK 门示例程序
[Door.java](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/src/main/java/com/tencent/iot/hub/device/android/app/scenarized/Door.java)  是门设备类，请先填入之前创建产品和设备步骤中得到的 **PRODUCT_ID**, **DEVICE_NAME**，**DEVICE_CERT_NAME** 和 **DEVICE_KEY_NAME**，并将设备证书、设备私钥文件放置在 **assets** 目录中：
```
/**
 * 产品ID
 */
private static final String PRODUCT_ID = "YOUR_PRODUCT_ID";
/**
 * 设备名称
 */
protected static final String DEVICE_NAME = "YOUR_DEVICE_NAME";

/**
 * 密钥
 */
private static final String SECRET_KEY = "YOUR_DEVICE_PSK";
/**
 * 设备证书名
 */
private static final String DEVICE_CERT_NAME = "YOUR_DEVICE_NAME_cert.crt";

/**
 * 设备私钥文件名
 */
private static final String DEVICE_KEY_NAME = "YOUR_DEVICE_NAME_private.key";
```


1. 在 enterRoom() 对 MQTT 连接实例进行判空检查，若为空，则进行初始化操作，并发起连接 connect()；若不为空，则判断连接是否有效，有效则发布 event 主题。 
2. 作为样例，根据用户执行程序时，指定的 action（come_home 或者 leave_home）和 targetDeviceName（需要中转到的设备名） 参数值，对消息的内容组装和发布。用户可自行组织消息内容和 topic，执行自己的发布消息逻辑。

####  实现 Android SDK 空调示例程序
[Airconditioner.java](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/src/main/java/com/tencent/iot/hub/device/android/app/scenarized/Airconditioner.java) 是空调设备类，与 [实现 Android-SDK 门示例程序](https://intl.cloud.tencent.com/document/product/1105/41467) 一样，需先填入产品和设备相关信息。
1. 在 Airconditioner 的构造方法中对 MQTT 连接实例进行初始化并发起连接 connect()。
2. MQTT 连接成功后，订阅 control 主题。


#### 运行示例程序
1. 单击 Android Studio Run 的【App】按钮，并安装 Demo。
2. 切换底部 Tab ，进入设备互通 Fragment，观察 Demo 及 logcat 中日志信息，以下为 logcat 中日志信息：
airConditioner1 连接 IoT 并订阅主题
```plaintext
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Start connecting to ssl://connect.iot.qcloud.com:8883
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: onSuccess!
com.qcloud.iot I/IoTEntryActivity: connected to ssl://connect.iot.qcloud.com:8883
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Starting subscribe topic: ******/airConditioner1/control
com.qcloud.iot I/IoTEntryActivity: onSubscribeCompleted, subscribe success
```
3. 单击【进门】，连接 IoT 并发布 control 主题，对应 message 为：
```plaintext
"{\"action\": \"come_home\", \"targetDevice\": \"airConditioner1\"}"
```
4. 观察 Demo 及 logcat 中日志信息，以下为 logcat 日志信息：
  - door1 连接 IoT
```plaintext
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Start connecting to ssl://connect.iot.qcloud.com:8883
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: onSuccess!
com.qcloud.iot I/IoTEntryActivity: connected to ssl://connect.iot.qcloud.com:8883
```
  - door1 发布主题（come_home）
```plaintext
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Starting publish topic: ******/door1/event Message: {"action": "come_home", "targetDevice": "airConditioner1"}
```
 - airConditioner1 接收到经规则引擎转发过来的主题
```plaintext
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Received topic: ******/airConditioner1/control, message: {"action":"come_home","targetDevice":"airConditioner1"}
com.qcloud.iot D/IoTEntryActivity: receive command: open airconditioner, count: 1
```
5. 单击【出门】，发布 control 主题，对应 message 为：
```plaintext
"{\"action\": \"leave_home\", \"targetDevice\": \"airConditioner1\"}"
```
6. 观察 Demo 及 logcat 中日志信息，以下为 logcat 日志信息：
 - door1 发布主题（leave_home）
```plaintext
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Starting publish topic: ******/door1/event Message: {"action": "leave_home", "targetDevice": "airConditioner1"}
```
 - airConditioner1 接收到经规则引擎转发过来的主题
```plaintext
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Received topic: ******/airConditioner1/control, message: {"action":"leave_home","targetDevice":"airConditioner1"}
com.qcloud.iot D/IoTEntryActivity: receive command: close airconditioner, count: 2
```
