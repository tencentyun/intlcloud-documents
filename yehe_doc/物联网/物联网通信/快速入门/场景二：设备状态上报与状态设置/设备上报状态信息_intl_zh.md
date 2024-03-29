###  C SDK 操作步骤
####  程序实现
作为样例，SDK 代码 sample/scenarized/aircond_shadow_sample_v2.c 里面，通过下面函数调用 `IOT_Shadow_Update` 对能耗状态上报到设备影子。并且注册相应的回调函数处理设备影子的回应。用户可在此自定义上报属性。
```
_do_report_energy_consumption(...)
...
IOT_Shadow_Update(...)
```

#### 程序编译与执行
1. 执行 ./aircond_shadow_sample_v2，注意如果用 MQTT 非对称加密方式，请保证根证书和设备证书和设备密钥文件在 ../../certs 上层目录下。
2. 调用 restAPI 相关接口获取 shadow 的状态数据，具体操作详见“查询获取设备信息”，同时观察示例程序输出日志：
![get_device_shadow_v1](https://mc.qcloudimg.com/static/img/056271af1bc4dc824ab479d2f0f0a9f2/2-6.png)
3. 执行 ./door_mqtt_sample come_home/leave_home airConditioner1，door1 与 airConditioner1 通信通过规则引擎驱动 airConditioner1 开启运作。能从日志观察能耗和室温相关的上报变化，再次通过 restAPI 获取 shadow 数（具体操作如第2步所示）：
![get_device_shadow_v2](https://mc.qcloudimg.com/static/img/65954fa964691d52bce646f45246ab2d/airdelta.png)

可见当 airConditioner1 运作后，空调能耗被动态上报到了 shadow 中，可顺利通过 restAPI 查询获取数据。

###  Android SDK 操作步骤
####  程序实现
请参照 [Android SDK 操作步骤 - 程序实现](https://intl.cloud.tencent.com/document/product/1105/41468) 中功能说明。

#### 程序编译与执行
请参照 [Android SDK 操作步骤 - 程序编译与执行](https://intl.cloud.tencent.com/document/product/1105/41468) 中功能说明。

### 查询获取设备信息
调用 restAPI 接口GetDeviceShadow 可获取到 shadow 的状态数据，用于 App 展示设备能耗状态。
restAPI 请求参数：`deviceName=airConditioner1, productName=AirConditioner`。
