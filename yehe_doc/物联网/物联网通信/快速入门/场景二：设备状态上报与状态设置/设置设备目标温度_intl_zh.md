### C SDK 操作步骤
#### 程序实现
1. 设备影子相关使用 sample/scenarized/aircond_shadow_sample_v2.c 的代码逻辑。它在 sample/scenarized/aircond_shadow_sample.c 添加如下逻辑：
2. 作为样例，SDK 内部调用 `IOT_Shadow_Register_Property` 对 shadow 的配置类属性和回调函数进行绑定。当 shadow 有该属性的配置变更时候，SDK 底层会执行相应的回调处理。这里注册了 shadow 里面 “temperatureDesire” 字段，意味着当 App 对设备影子设置目标温度的时候，能通过回调函数更正本地的配置数据，调整期望温度。用户可实现自定义的配置型属性监听和回调绑定。
```
rc = _register_config_shadow_property();
```

####  程序编译与执行

1. 在 SDK 程序根目录下执行 make，编译得到 aircond_shadow_sample_v2 可执行程序。
2. 在目录 ./output/release/bin 下执行 ./aircond_shadow_sample_v2，注意如果用 MQTT 非对称加密方式，请保证根证书、设备证书和设备密钥文件在 ../../certs 上层目录下。
3. 在目录 ./output/release/bin 下执行 ./door_mqtt_sample come_home airConditioner1，让 airConditioner 处于运作状态。
```
	INF|2018-01-11 20:52:50|aircond_shadow_sample_v2.c|main(377): Cloud Device Construct Success
	INF|2018-01-11 20:52:50|aircond_shadow_sample_v2.c|main(389): Cloud Device Register Delta Success
```
4. 调用 restAPI 模拟家电管理后台发布目标温度配置，具体操作详见发布设备目标温度配置，同时观察示例程序输出日志：

从输出的日志中，可以看到`on_temperature_actuate_callback `函数被调用，表示收到 shadow 下发的 delta topic，然后执行更新本地的设定温度操作 `modify desire temperature to: 10.000000`
```
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_temperature_actuate_callback(181): actuate callback jsonString=10},"desired":{"temperatureDesire":10},"reported":{"energyConsumption":0.0}},"timestamp":1515675847609,"version":5},"result":0,"timestamp":1515675871,"type":"get"}|dataLen=2
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_temperature_actuate_callback(184): modify desire temperature to: 10.000000
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_request_handler(123): Method=GET|Ack=ACK_ACCEPTED
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_request_handler(124): received jsonString={"clientToken":"EJSKHKIS1M-0","payload":{"metadata":{"delta":{"temperatureDesire":{"timestamp":1515675847609}},"desired":{"temperatureDesire":{"timestamp":1515675847609}},"reported":{"energyConsumption":{"timestamp":1515674881485}}},"state":{"delta":{"temperatureDesire":10},"desired":{"temperatureDesire":10},"reported":{"energyConsumption":0.0}},"timestamp":1515675847609,"version":5},"result":0,"timestamp":1515675871,"type":"get"}
```

从上面 airConditioner1 输出日志，可见配置操作生效，airConditioner 调节本地的配置温度。

###  Android SDK 操作步骤
####  程序实现
[ShadowSample.java](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/src/main/java/com/tencent/iot/hub/device/android/app/shadow/ShadowSample.java) 是设备影子类，主要功能有：
1. 建立 Shadow 连接：connect()，内部调用 TXShadowConnect 的 connect() 接口。
2. 断开 Shadow 连接：closeConnect()，内部调用 TXShadowConnection 的 disconnect() 接口。
3. 注册设备属性：registerProperty()，内部调用 TXShadowConnection 的 registerProperty() 接口。
4. 获取设备影子：getDeviceShadow(), 内部调用 TXShadowConnection 的 get() 接口。
5. 定时更新设备影子：loop()，内部调用 TXShadowConnection 的 update() 接口。

#### 程序编译与执行
在运行 App 前，请先填入之前创建产品和设备步骤中得到的 **PRODUCT_ID**, **DEVICE_NAME**，**DEVICE_CERT_NAME** 和 **DEVICE_KEY_NAME**，并将设备证书、设备私钥文件放置在 **assets** 目录中：                                                             
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
1. 填入设备相关信息后，即可运行 Demo，单击 Android Studio Run 【App】 按钮安装运行 Demo。
2. 切换底部 Tab 到**设备影子** Fragment，便可操作 Shadow 相关功能。
3. 各功能均有对应的操作按钮，单击相应按钮，观察 Demo 及 logcat 日志输出。
4. restAPI 接口操作说明，若为发布目标温度配置详见 [发布目标温度配置](https://intl.cloud.tencent.com/document/product/1105/41468)；若为查询获取设备信息详见 [查询获取设备信息](https://intl.cloud.tencent.com/document/product/1105/41468)。

### 发布目标温度配置
调用 restAPI 接口 UpdateDeviceShadow 模拟家电管理后台发布目标温度配置，
restAPI 请求参数：`deviceName=airConditioner1, state={"desired" : {"temperatureDesire": 10}}, productName=AirConditioner`, 期望调整控制温度为 10°。

