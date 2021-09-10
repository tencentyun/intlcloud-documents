## Overview
If you need to set a device target temperature and report device status information in a smart home scenario (this is not a real product but only used to demonstrate IoT Hub's capabilities), you can follow the steps in this document.

![shadow_get_update](https://main.qcloudimg.com/raw/74ee56cdeb3836ce4c7dc5a21d9540fd.png)

## Setting Device Target Temperature
### Solution
![update_shadow](https://main.qcloudimg.com/raw/93d2e910859d326de663f3793d4be9b1.png)
The management backend updates the configuration and registration parameters of the device shadow and associates the corresponding callback functions through the TencentCloud APIs provided by IoT Hub to update the configuration locally.
For the implementation of relevant TencentCloud APIs for device shadow, please download [iotcloud_RestAPI_python.zip](https://mc.qcloudimg.com/static/archive/c6b492abe009de1c47b91b8bfd93c7d2/iotcloud_RestAPI_python.zip). You need to configure your profile according to the RESTful API description. You can customize the features by modifying the parameters in `airConditionerCtrl.py` in the `RestAPI` folder.


### Directions for SDK for C
#### Program implementation
1. The device shadow uses the code logic of `sample/scenarized/aircond_shadow_sample_v2.c`. It adds the following logic to `sample/scenarized/aircond_shadow_sample.c`:
2. As an example, the SDK internally calls `IOT_Shadow_Register_Property` to bind the shadow's configuration class attribute and callback function. When the shadow has a configuration change of this attribute, the underlying layer of the SDK will perform the corresponding callback. The `temperatureDesire` field in the shadow is registered here, which means that when the application sets the target temperature for the device shadow, the local configuration can be corrected by the callback function to adjust the desired temperature. You can also implement custom configuration-based attribute listening and callback binding.
```
rc = _register_config_shadow_property();
```

#### Program compilation and execution

1. Run `make` in the root directory of the SDK, compile, and get the `aircond_shadow_sample_v2` executable program.
2. Run `./aircond_shadow_sample_v2` in the `./output/release/bin` directory. Please note that if MQTT asymmetric encryption is used, the root certificate, device certificate, and device key files should be placed in the parent directory of `./../certs`.
3. Run `./door_mqtt_sample come_home airConditioner1` in the `./output/release/bin` directory to turn on `airConditioner`.
```
	INF|2018-01-11 20:52:50|aircond_shadow_sample_v2.c|main(377): Cloud Device Construct Success
	INF|2018-01-11 20:52:50|aircond_shadow_sample_v2.c|main(389): Cloud Device Register Delta Success
```
4. Call the RESTful API to simulate the home appliance management backend and publish the target temperature configuration. For detailed directions, please see "Publishing target temperature configuration" and observe the output log of the demo:

In the output log, it can be seen that the `on_temperature_actuate_callback` function has been called, indicating that the `delta` topic sent by the shadow has been received, and the operation `modify desire temperature to: 10.000000` has been performed for updating the locally set temperature.
```
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_temperature_actuate_callback(181): actuate callback jsonString=10},"desired":{"temperatureDesire":10},"reported":{"energyConsumption":0.0}},"timestamp":1515675847609,"version":5},"result":0,"timestamp":1515675871,"type":"get"}|dataLen=2
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_temperature_actuate_callback(184): modify desire temperature to: 10.000000
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_request_handler(123): Method=GET|Ack=ACK_ACCEPTED
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_request_handler(124): received jsonString={"clientToken":"EJSKHKIS1M-0","payload":{"metadata":{"delta":{"temperatureDesire":{"timestamp":1515675847609}},"desired":{"temperatureDesire":{"timestamp":1515675847609}},"reported":{"energyConsumption":{"timestamp":1515674881485}}},"state":{"delta":{"temperatureDesire":10},"desired":{"temperatureDesire":10},"reported":{"energyConsumption":0.0}},"timestamp":1515675847609,"version":5},"result":0,"timestamp":1515675871,"type":"get"}
```

In the above output log of `airConditioner1`, it can be seen that the configuration operation has taken effect and `airConditioner` has adjusted the locally set temperature.

### Directions for SDK for Android
#### Program implementation
[ShadowSample.java](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/src/main/java/com/tencent/iot/hub/device/android/app/shadow/ShadowSample.java) is the device shadow class with the following main features:
1. Establish a shadow connection: connect(), which internally calls the `connect()` API of `TXShadowConnect`.
2. Close the shadow connection: closeConnect(), which internally calls the `disconnect()` API of `TXShadowConnection`.
3. Register the device attribute: registerProperty(), which internally calls the `registerProperty()` API of `TXShadowConnection`.
4. Get the device shadow: getDeviceShadow(), which internally calls the `get()` API of `TXShadowConnection`.
5. Regularly update the device shadow: loop(), which internally calls the `update()` API of `TXShadowConnection`.

#### Program compilation and execution
Before running the application, please enter the **PRODUCT_ID**, **DEVICE_NAME**, **DEVICE_CERT_NAME**, and **DEVICE_KEY_NAME** obtained in the previous steps for product and device creation and place the device certificate and device private key files in the **assets** directory:                                                             
```
/**
 * Product ID
 */
private static final String PRODUCT_ID = "YOUR_PRODUCT_ID";
/**
 * Device name
 */
protected static final String DEVICE_NAME = "YOUR_DEVICE_NAME";

/**
 * Key
 */
private static final String SECRET_KEY = "YOUR_DEVICE_PSK";
/**
 * Device certificate name
 */
private static final String DEVICE_CERT_NAME = "YOUR_DEVICE_NAME_cert.crt";

/**
 * Device private key file name
 */
private static final String DEVICE_KEY_NAME = "YOUR_DEVICE_NAME_private.key";
```
1. After entering the device information, click the **Run** icon in Android Studio to install and run the demo.
2. Switch the bottom tab to the **device shadow** fragment to use the features of the shadow.
3. Each feature has a corresponding operation button. Click a button and observe the log output of the demo and logcat.
4. For more information on the operations of the RESTful APIs, please see [Publishing target temperature configuration](https://intl.cloud.tencent.com/document/product/1105/41468) or [Querying and getting device information](https://intl.cloud.tencent.com/document/product/1105/41468).

### Publishing target temperature configuration
Call the RESTful API UpdateDeviceShadow to simulate the home appliance management backend and publish the target temperature configuration.
The RESTful API request parameter is: `deviceName=airConditioner1, state={"desired" : {"temperatureDesire": 10}}, productName=AirConditioner`, which adjusts the control temperature to 10°C.


### Solution
![get_device_shadow](https://main.qcloudimg.com/raw/41111ad8d4d9a9414d6eb1cd1e45215b.png)
The device reports its own status data to the device shadow, and the home appliance management backend directly gets data from the device shadow through the RESTful API.

### Directions for SDK for C
#### Program implementation
As an example, the energy consumption status is reported to the device shadow through the call of `IOT_Shadow_Update` by the following function in the SDK code `sample/scenarized/aircond_shadow_sample_v2.c`. Then, the corresponding callback function is registered to handle the response of the device shadow. You can customize the reported attributes here.
```
_do_report_energy_consumption(...)
...
IOT_Shadow_Update(...)
```

#### Program compilation and execution
1. Run `./aircond_shadow_sample_v2`. Please note that if MQTT asymmetric encryption is used, the root certificate, device certificate, and device key files should be placed in the parent directory of `./../certs`.
2. Call the relevant RESTful API to get the status data of the shadow. For detailed directions, please see "Querying and getting device information". Observe the output log of the demo:
![get_device_shadow_v1](https://mc.qcloudimg.com/static/img/056271af1bc4dc824ab479d2f0f0a9f2/2-6.png)
3. Run `./door_mqtt_sample come_home/leave_home airConditioner1`. `door1` will communicate with `airConditioner1`, and then `airConditioner1` will be instructed to turn on through the rule engine. The reported changes in energy consumption and indoor temperature can be observed in the log, and the shadow data is obtained again through the RESTful API (as detailed in step 2):
![get_device_shadow_v2](https://mc.qcloudimg.com/static/img/65954fa964691d52bce646f45246ab2d/airdelta.png)

It can be seen that after `airConditioner1` is turned on, the air conditioner energy consumption is dynamically reported to the shadow, and the data can be successfully queried and obtained through the RESTful API.

### Directions for SDK for Android
#### Program implementation
Please see the instructions in [Directions for SDK for Android - Program implementation](https://intl.cloud.tencent.com/document/product/1105/41468).

#### Program compilation and execution
Please see the instructions in [Directions for SDK for Android - Program compilation and execution](https://intl.cloud.tencent.com/document/product/1105/41468).

### Querying and getting device information
Call the RESTful API GetDeviceShadow to get the status data of the shadow, which is used by the application to display the device's energy consumption.
The RESTful API request parameter is: `deviceName=airConditioner1, productName=AirConditioner`.
