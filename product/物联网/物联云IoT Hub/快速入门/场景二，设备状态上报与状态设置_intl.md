[//]: # (chinagitpath:XXXXX)

We may also need the following features:

![shadow_get_update](https://mc.qcloudimg.com/static/img/6ba8645ccd5d07eb8cc1a1fcede5ce6b/2-1.png)

## 1. Set Device's Target Temperature
### 1.1 Solution

![update_shadow](https://mc.qcloudimg.com/static/img/62cd3183a1932dacee4f4ff81487758b/2-2.png)

The management backend uses the cloud APIs provided by IoT Hub to update device shadow’s configuration and registration parameters, associate the corresponding callback function to update the configuration locally.
For the implementation of relevant cloud APIs for device shadow, please download [iotcloud_RestAPI_python.zip](https://mc.qcloudimg.com/static/archive/c6b492abe009de1c47b91b8bfd93c7d2/iotcloud_RestAPI_python.zip). You need to configure your profile according to the RestAPI Instructions. You can customize the features by modifying the parameters in airConditionerCtrl.py in the RestAPI folder.

### 1.2 C-SDK Operational Steps
#### 1.2.1 Implement the Program
The device shadow uses the code logic of sample/scenarized/aircond_shadow_sample_v2.c. It adds the following logic to sample/scenarized/aircond_shadow_sample.c:

As an example, the SDK internally calls `IOT_Shadow_Register_Property` to bind the shadow's configuration class property and callback function. When the shadow has configuration change to this property, the underlying layer of the SDK will perform the corresponding callback. The "temperatureDesire" field in the shadow is registered here, which means that when the app sets the target temperature for the device shadow, the local configuration can be corrected by the callback function to adjust the desired temperature. You can implement custom configuration-based property monitoring and callback binding.

```
rc = _register_config_shadow_property();
```

#### 1.2.2 Compile and Execute the Program

1. Execute the make in the root directory of the SDK, compile and get the aircond_shadow_sample_v2 executable program;
2. Execute ./aircond_shadow_sample_v2 in the ./output/release/bin directory. Please note that if MQTT asymmetric encryption is used, the root certificate, device certificate and device key file should be placed in the parent directory of ../../certs.
3. Execute ./door_mqtt_sample come_home airConditioner1 in the ./output/release/bin directory to turn on airConditioner.

	```
	INF|2018-01-11 20:52:50|aircond_shadow_sample_v2.c|main(377): Cloud Device Construct Success
	INF|2018-01-11 20:52:50|aircond_shadow_sample_v2.c|main(389): Cloud Device Register Delta Success
	```

4. Call restAPI to simulate the home appliance management backend and publish the target temperature configuration. For details, see "1.4 Publish the target temperature configuration" and observe the output log of the sample program:

	In the output log, it can be seen that the `on_temperature_actuate_callback ` function has been called, indicating that the delta topic sent by the shadow has been received, and the operation `modify desire temperature to: 10.000000` has been performed for updating the locally set temperature.

	```
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_temperature_actuate_callback(181): actuate callback jsonString=10},"desired":{"temperatureDesire":10},"reported":{"energyConsumption":0.0}},"timestamp":1515675847609,"version":5},"result":0,"timestamp":1515675871,"type":"get"}|dataLen=2
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_temperature_actuate_callback(184): modify desire temperature to: 10.000000
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_request_handler(123): Method=GET|Ack=ACK_ACCEPTED
	INF|2018-01-11 21:04:31|aircond_shadow_sample_v2.c|on_request_handler(124): received jsonString={"clientToken":"EJSKHKIS1M-0","payload":{"metadata":{"delta":{"temperatureDesire":{"timestamp":1515675847609}},"desired":{"temperatureDesire":{"timestamp":1515675847609}},"reported":{"energyConsumption":{"timestamp":1515674881485}}},"state":{"delta":{"temperatureDesire":10},"desired":{"temperatureDesire":10},"reported":{"energyConsumption":0.0}},"timestamp":1515675847609,"version":5},"result":0,"timestamp":1515675871,"type":"get"}

	```
	
	In the output log of airConditioner1 above, it can be seen that the configuration operation has taken effect and airConditioner has adjusted the locally set temperature.
	
### 1.3 Android-SDK Operational Steps
#### 1.3.1 Implement the Program
com/qcloud/iot/samples/shadow/ShadowSample.java is the device shadow class with the following main features:

1. Establish a Shadow connection: connect(), which internally calls the connect() API of TXShadowConnect;

2. Close the Shadow connection: closeConnect(), which internally calls the disconnect() API of TXShadowConnection;

3. Register the device property: registerProperty(), which internally calls the registerProperty() API of TXShadowConnection;

4. Get the device shadow: getDeviceShadow(), which internally calls the get() API of TXShadowConnection;

5. Regularly update the device shadow: loop(), which internally calls the update() API of TXShadowConnection;

#### 1.3.2 Compile and Execute the Program

Before running the app, please enter the **PRODUCT_ID**, **DEVICE_NAME**, **DEVICE_CERT_NAME** and **DEVICE_KEY_NAME** obtained in the previous steps for product and device creation and place the device certificate and device private key file in the **assets** directory:
                                                              
![](https://mc.qcloudimg.com/static/img/8289db39e3b0ea39fff78daf26a33a41/IoTDoor_AndroidConfig.png)

1. After entering the device-related information, click the Android Studio Run 'app' button to install and run the Demo;

2. Switch the bottom tab to the **device shadow** Fragment to use the features of the Shadow;

3. Each feature has a corresponding operation button. Click a button and observe the log output of the Demo and logcat;

4. For details on the operations of the restAPI, see "1.4 Publish the target temperature configuration" or "2.4 Query and get the device information".

### 1.4 Publish the Target Temperature Configuration
Call the restAPI [UpdateDeviceShadow](https://cloud.tencent.com/document/product/634/12055) to simulate the home appliance management backend and publish the target temperature configuration.
The restAPI request parameter is: `deviceName=airConditioner1, state={"desired" : {"temperatureDesire": 10}}, productName=AirConditioner`, which adjusts the control temperature to 10°C.

## 2. Report Device Status Information
### 2.1 Solution

![get_device_shadow](https://mc.qcloudimg.com/static/img/d2344da99a6a1eddf04551c6651ad7e1/iot_get_device_v2.png)

The device reports its own status data to the device shadow, and the home appliance management backend directly obtains data from the device shadow through the restAPI.

### 2.2 C-SDK Operational Steps
#### 2.2.1 Implement the Program
As an example, the energy consumption status is reported to the device shadow through the call of `IOT_Shadow_Update` by the following function in the SDK code sample/scenarized/aircond_shadow_sample_v2.c. Then, the corresponding callback function is registered to handle the response of the device shadow. You can customize the reported properties here.

```
_do_report_energy_consumption(...)
...
IOT_Shadow_Update(...)
```

#### 2.2.2 Compile and Execute the Program
1. Execute ./aircond_shadow_sample_v2. Please note that if MQTT asymmetric encryption is used, the root certificate, device certificate and device key file should be placed in the parent directory of ../../certs.

2. Call the relevant restAPI to obtain the status data of the shadow. For details, see "2.4 Query and get device information". Observe the output log of the sample program:

	![get_device_shadow_v1](https://mc.qcloudimg.com/static/img/056271af1bc4dc824ab479d2f0f0a9f2/2-6.png)
	
3. Execute ./door_mqtt_sample come_home/leave_home airConditioner1 and door1 communicates with airConditioner1, then airConditioner1 is instructed to turn on through the rule engine. The reported changes in energy consumption and indoor temperature can be observed in the log, and the shadow data is obtained again through the restAPI (as detailed in step 2):

	![get_device_shadow_v2](https://mc.qcloudimg.com/static/img/65954fa964691d52bce646f45246ab2d/airdelta.png)
	
	It can be seen that after airConditioner1 turns on, the air conditioner's energy consumption is dynamically reported to the shadow, and the data can be successfully queried and obtained through the restAPI.
	
### 2.3 Android-SDK Operational Steps
#### 2.3.1 Implement the Program

See the instructions in "Step 1.3.1 Implement the program".

#### 2.3.2 Compile and Execute the Program
 
See the instructions in "Step 1.3.2 Compile and execute the program".

### 2.4 Query and Get Device Information
Call the restAPI [GetDeviceShadow](https://cloud.tencent.com/document/product/634/12052) to get the status data of the shadow, which is used by the app to display the device's energy consumption status.
The restAPI request parameter is: `deviceName=airConditioner1, productName=AirConditioner`.



