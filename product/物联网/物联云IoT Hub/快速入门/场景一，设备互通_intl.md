[//]: # (chinagitpath:XXXXX)

We aim to achieve the following features in a hypothetical smart home scenario (this is a hypothetical product used only to demonstrate IoT Hub's capabilities):
![come_home](https://mc.qcloudimg.com/static/img/71322deb86ac93b9cb5c63456d132827/1-1.png)

## 1. Solution

Two types of smart devices (Door and AirConditioner) can be created in IoT Hub SDK and connected with each other based on cross-device messages and rule engines as below:

![rule_engine_for_smart_home](https://mc.qcloudimg.com/static/img/d158634d34fbddbed17bfaa49cb24d90/airv1schema.png)
	
> **Note:**
> AirConditioner1 cannot achieve message communication by directly subscribing to the update messages of door1. See below for the explanation. [Feature Components - Permission Management](https://cloud.tencent.com/document/product/634/11915).

## 2. Steps

### 2.1 Create A Door Product and Device

1. Go to the [Console](https://console.cloud.tencent.com/iotcloud), create a product (Door) and select the encryption type as needed.

	![Create a door product](https://main.qcloudimg.com/raw/68b7fd89cca0d86fac8ca64366f64d06.png)

2. After creation, you can view the basic information of the product.

	![Product settings](https://main.qcloudimg.com/raw/dec1dcdca4da7fcfbbf787428aa2757a.png)

3. Create a device (door1) in the **Device list**.
	> **Note:** Key for the device will be returned after device creation under asymmetric encryption, and will be used for device communication. Key will not be stored in the IoT Hub backend. Remember to save it properly.
	![Return of device creation](https://mc.qcloudimg.com/static/img/b0b63b16c667a295e0dd66b56b7fad20/IoTDoorDevicePK.png)

4. Click **Manage** to query the device details.

	- Asymmetric Encryption:
	![Query devices](https://main.qcloudimg.com/raw/401dc0b548a5c7a2f2279ea237f0e487.png)
	
	- Symmetric Encryption:
	![Query devices](https://main.qcloudimg.com/raw/ed7e4eec30297f1c134f5922dd91dfa1.png)
	
	
### 2.2 Create an Air Conditioner Product and Device

1. Go to the [Console](https://console.cloud.tencent.com/iotcloud) and create an air conditioner product (AirConditioner) as illustrated in step 2.1.1.

	![Create an air conditioner product](https://main.qcloudimg.com/raw/31ddbfb16c38ece75a33c34ebcc723c6.png)
    	
2. Upon creation, you can view the basic information of the product.

	![Create a device](https://main.qcloudimg.com/raw/fa8d85cc6d9772d773ad354adda8f0d8.png)
    
3. Create a device (airConditioner1) in the **Device list** as illustrated in step 2.1.3.
    
4. Click **Manage** to query the device details.

	![Query devices](https://main.qcloudimg.com/raw/5eeb4f0836d7c067c32a2a2ae0c497b1.png)
    
In the device details querying page, device certificate and device private key are used for MQTT over TLS asymmetric encryption.  Symmetric key is used for symmetric encryption (for the differences between the two communication methods, see [Feature Components - Device Access](https://cloud.tencent.com/document/product/634/11915)).
> **Note:**
> The creation of the resources above can be done by the backend via restAPI. For details, see [API Overview](https://cloud.tencent.com/document/product/634/12056).

### 2.3 Create a Rule Engine

![Create a rule engine](https://main.qcloudimg.com/raw/31e3855c3c37905f106e7a050eb12489.png)

For detailed steps, see [Rule Engine Details](https://cloud.tencent.com/document/product/634/11917).

### 2.4 Download SDK
Download the SDK [here](https://cloud.tencent.com/document/product/634/11928).

### 2.5 Configure the C-SDK Sample Program

1. samples/scenarized/door_mqtt_sample.c is the MQTT-based logic code for the door.

2. samples/scenarized/door_coap_sample.c is the CoAP-based logic code for the door.

3. samples/scenarized/aircond_shadow_sample.c is the MQTT-based logic code for the air conditioner.

door_mqtt_sample.c and door_coap_sample.c are examples of message reporting through MQTT and CoAP respectively. The two samples achieve the same feature.

#### 2.5.1 Implement the C-SDK Door Sample Program Based on the MQTT Protocol

Edit door_mqtt_sample.c in the C-SDK sample program directory samples/scenarized, and then populate the following configuration items with the device information obtained in "Step 2.1 Create a door product and device" (the numbers after the meanings in the table below correspond to the numbers in the screenshot in step 2.1).

| Configuration Item | Meaning | 
| ---- | ------ | 
| QCLOUD_IOT_MY_PRODUCT_ID | Device ID; globally unique; available in the device details page **(1)** |
| QCLOUD_IOT_MY_DEVICE_NAME | Device name; available in the device details page **(3)** |
| QCLOUD_IOT_CERT_FILENAME | Device certificate name; downloaded from the device details page; only for asymmetric encryption **(4)** |
| QCLOUD_IOT_KEY_FILENAME | Device private key file name; downloaded from the device details page; only for asymmetric encryption **(2)** |
| QCLOUD_IOT_PSK | Device symmetric key; downloaded from the device details page, only for symmetric encryption **(5)** |

1. Complete the parameter initialization of the MQTT communication protocol. Device information needs to be entered in the `_setup_connect_init_params` function. For the specific macro definitions, see the table above:

	```
	MQTTInitParams initParams = DEFAULT_MQTTINIT_PARAMS;
	_setup_connect_init_params(&initParams);
	```

2. Complete the parameter initialization of the MQTT connect request and execute the construct:

	```
	void *client = IOT_MQTT_Construct(&initParams);
	```
3. As an example, the content of the message is assembled and published based on the action (come_home or leave_home) and targetDeviceName (name of the device that needs to be relayed to) parameters specified by you when executing the program. You can organize your own message content and topic to execute your own message publishing logic.

	```
	_publish_msg(action, targetDeviceName);
	```

4. Execute the make in the code's root directory, compile and then get the door_mqtt_sample executable program in the output/release/bin directory.

5. Execute ./door_mqtt_sample come_home airConditioner1 (the first input parameter is the action: come_home or leave_home; the second parameter is the target object of the message, which is assumed as airConditioner1 here). Please note that if TLS asymmetric encryption is used, the device certificate file and device private key file should be placed in the parent directory of certs.
The following implements the connecting and publishing features of the device "door". If the execution succeeds, the following result is displayed:

```
INF|2018-01-11 20:13:22|door_mqtt_sample.c|main(207): Cloud Device Construct Success
DBG|2018-01-11 20:13:22|mqtt_client_publish.c|qcloud_iot_mqtt_publish(317): publish topic seq=33254|topicName=K02I1V7PGO/door1/event|payload={"action": "come_home", "targetDevice": "airConditioner1"}
INF|2018-01-11 20:13:22|door_mqtt_sample.c|main(227): Wait for publish ack
INF|2018-01-11 20:13:22|door_mqtt_sample.c|event_handler(89): publish success, packet-id=33254
```

#### 2.5.2 Implement the C-SDK Door Sample Program Based on the CoAP Protocol

1. Complete the configuration of the CoAP communication initialization parameter "init_params". Edit door_coap_sample.c in the C-SDK sample program directory samples/scenarized, and then fill out the following configuration items with the device information obtained in "Step 2.1 Create a door product and device" (the numbers after the meanings in the table below correspond to the numbers in the screenshot in step 2.1).

| Configuration item | Meaning | 
| ---- | ------ | 
| QCLOUD_IOT_MY_PRODUCT_ID | Device ID is unique and available in the device details page **(1)** |
| QCLOUD_IOT_MY_DEVICE_NAME | Device name; available in the device details page **(3)** |
| QCLOUD_IOT_CERT_FILENAME | Device certificate name can be downloaded from the device details page and used only for asymmetric encryption **(4)** |
| QCLOUD_IOT_KEY_FILENAME | Device private key file name can be downloaded from the device details page and used only for asymmetric encryption **(2)** |
| QCLOUD_IOT_PSK | Device symmetric key can be downloaded from the device details page, and used only for symmetric encryption **(5)** |

2. Complete the creation of the CoAP connection and the client. The initialization parameter is as detailed in step 1.

	```
	void *coap_client = IOT_COAP_Construct(&init_params);
	```
3. As an example, the content of the message is assembled and published based on the action (come_home or leave_home) and targetDeviceName (name of the device that needs to be relayed to) parameters specified by you when executing the program. You can organize your own message content and topic to execute your own message publishing logic. The topic in the door_coap_sample.c sample is /$(productId)/$(deviceName)/event which publishes the messages.

    ```
	char topicName[128] = "";
	sprintf(topicName, "/%s/%s/event", QCLOUD_IOT_MY_PRODUCT_ID, QCLOUD_IOT_MY_DEVICE_NAME);
    Log_i("topic name is %s", topicName);
	rc = IOT_COAP_SendMessage(coap_client, topicName, &send_params);
    ```
4. Execute the make in the root directory and then get the door_coap_sample executable program in the output/release/bin directory.

5. Execute ./door_coap_sample come_home airConditioner1 (the first input parameter is the action: come_home or leave_home; the second parameter is the target object of the message, which is assumed as airConditioner1 here). Please note that if DTLS asymmetric encryption is used, the device certificate file and device private key file should be placed in the certs directory at the same level as the door_coap_sample executable program.
The following implements the connecting and publishing features of the device "door". If the execution succeeds, the following result is displayed:

```
INF|2018-01-12 18:07:17|coap_client.c|IOT_COAP_Construct(84): device auth successfully, connid: h4TFD
ERR|2018-01-12 18:07:17|door_coap_sample.c|main(119): 0x110c010
INF|2018-01-12 18:07:17|door_coap_sample.c|main(143): topic name is /D6WQAXE63D/skyTest1/event
INF|2018-01-12 18:07:17|coap_client_message.c|coap_message_send(390): add coap message id: 52124 into wait list ret: 0
DBG|2018-01-12 18:07:17|door_coap_sample.c|main(150): client topic has been sent, msg_id: 52124
DBG|2018-01-12 18:07:17|HAL_DTLS_mbedtls.c|HAL_DTLS_Read(356): mbedtls_ssl_read len 50 bytes
DBG|2018-01-12 18:07:17|coap_client_message.c|_coap_message_handle(292): receive coap piggy ACK message, id 52124
INF|2018-01-12 18:07:17|door_coap_sample.c|event_handler(54): message received ACK, msgid: 52124
DBG|2018-01-12 18:07:17|coap_client_message.c|_coap_message_list_proc(144): remove the message id 52124 from list
INF|2018-01-12 18:07:17|coap_client_message.c|_coap_message_list_proc(85): remove node
INF|2018-01-12 18:07:17|coap_client.c|IOT_COAP_Destroy(118): coap release!
```

#### 2.5.3 Implement the C-SDK Air Conditioner Sample Program Based on the MQTT Protocol

1. Initialize the MQTT protocol
2. Implement the MQTT connect logic

The operation is as detailed in "Step 2.5.1 Implement the C-SDK door sample program".

As an example, `_register_subscribe_topics` implements the subscription to AirConditioner/airConditioner1/control and registers the corresponding callback handler. After receiving a message from this topic, the callback determines whether the message content is "come_home" or "leave_home" and instructs the airConditioner to turn on or off accordingly. You can subscribe to messages from a custom topic within the function and register a custom callback.

```
rc = _register_subscribe_topics();
```

In the loop processing below, the `IOT_Shadow_Yield` function can monitor the subscribed topic, and callback function will be executed after receiving a corresponding topic message. In general, there is no need to change the processing logic. `_simulate_room_temperature` is a basic simulation of airConditioner’s indoor temperature and energy consumption changes. You can also implement other custom logics.

```
rc = IOT_Shadow_Yield(client, 200);

if (rc == QCLOUD_ERR_MQTT_ATTEMPTING_RECONNECT) {
    sleep(1);
    continue;
}
else if (rc != QCLOUD_ERR_SUCCESS) {
	Log_e("Exit loop caused of errCode: %d", rc);
}

if (sg_subscribe_event_result != MQTT_EVENT_SUBCRIBE_SUCCESS &&
    sg_subscribe_event_result != MQTT_EVENT_SUBCRIBE_TIMEOUT &&
    sg_subscribe_event_result != MQTT_EVENT_SUBCRIBE_NACK)
{
    sleep(1);
    continue;
}

_simulate_room_temperature(&sg_report_temperature);
Log_i("airConditioner state: %s", sg_airconditioner_openned ? "open" : "close");
Log_i("currentTemperature: %f, energyConsumption: %f", sg_report_temperature, sg_energy_consumption);

sleep(1);
```

3. Execute the make in the code's root directory, compile and then get the aircond_shadow_sample executable program in the output/release/bin directory.

4. Execute ./aircond_shadow_sample. Please note that if TLS asymmetric encryption is used, the device certificate file and device private key file should be placed in the parent directory of certs.

	```
	INF|2018-01-11 20:15:07|shadow_client.c|IOT_Shadow_Construct(169): Sync device data successfully
	INF|2018-01-11 20:15:07|aircond_shadow_sample.c|main(253): Cloud Device Construct Success
	DBG|2018-01-11 20:15:07|mqtt_client_subscribe.c|qcloud_iot_mqtt_subscribe(123): topicName=R1JMYJIOYJ/airConditioner1/control|packet_id=16076|pUserdata=(null)
	DBG|2018-01-11 20:15:07|shadow_client.c|_shadow_event_handler(63): shadow subscribe success, packet-id=16076
	INF|2018-01-11 20:15:07|aircond_shadow_sample.c|event_handler(109): subscribe success, packet-id=16076
	INF|2018-01-11 20:15:07|aircond_shadow_sample.c|main(288): airConditioner state: close
	INF|2018-01-11 20:15:07|aircond_shadow_sample.c|main(289): currentTemperature: 32.000000, energyConsumption: 0.000000
	```
	The code above implements the connecting and subscribing features of the device "airConditioner1". The program monitors the subscribed topic and outputs numbers related to the indoor temperature and energy consumption.


#### 2.5.4 Enable Device Interconnection

The steps above established a communication channel between door1 and airConditioner1.

1. The steps above established the communication channel between door1 and airConditioner1. Re-execute ./aircond_shadow_sample, execute ./door_mqtt_sample come_home airConditioner1 and view the output log.
2. It can be seen from the log that airConditioner1 has obtained the message from door1 and changed the `status` to "open", and the indoor temperature `currentTemperature` (adjusted to the configured default temperature) and the energy consumption "energyConsumption" are changed dynamically.

	```
	INF|2018-01-11 20:15:13|aircond_shadow_sample.c|main(288): airConditioner state: close
	INF|2018-01-11 20:15:13|aircond_shadow_sample.c|main(289): currentTemperature: 32.000000, energyConsumption: 0.000000
	INF|2018-01-11 20:15:14|aircond_shadow_sample.c|on_message_callback(162): Receive Message With topicName: R1JMYJIOYJ/airConditioner1/control, payload:{"action":"come_home","targetDevice":"airConditioner1"}
	INF|2018-01-11 20:15:14|aircond_shadow_sample.c|main(288): airConditioner state: open
	INF|2018-01-11 20:15:14|aircond_shadow_sample.c|main(289): currentTemperature: 31.000000, energyConsumption: 1.000000
	```


### 2.6 Configure the Android-SDK Sample Program

#### 2.6.1 Implement the Android-SDK Door Sample Program

com/qcloud/iot/samples/scenarized/Door.java is the door device class. Please enter the **PRODUCT_ID**, **DEVICE_NAME**, **DEVICE_CERT_NAME** and **DEVICE_KEY_NAME** obtained in the previous steps for product and device creation and place the device certificate and device private key file in the **assets** directory:

![](https://mc.qcloudimg.com/static/img/8289db39e3b0ea39fff78daf26a33a41/IoTDoor_AndroidConfig.png)

1. Perform an emptiness check on the MQTT connection instance in enterRoom(). If it is empty, perform initialization and initiate connect(); if it is not empty, determine whether the connection is valid, and if it is valid, publish the event topic.
   
2. As an example, the content of the message is assembled and published based on the action (come_home or leave_home) and targetDeviceName (name of the device that needs to be relayed to) parameters specified by you when executing the program. You can organize your own message content and topic to execute your own message publishing logic.

#### 2.6.2 Implement the Android-SDK Air Conditioner Sample Program

com/qcloud/iot/samples/scenarized/Airconditioner.java is the air conditioner device class. Just like in "Step 2.6.1 Implement the Android-SDK door sample program", you need to enter the information related to the product and device first.

1. Initialize the MQTT connection instance in the Airconditioner constructor and initiate connect();

2. After the MQTT connection is successfully established, subscribe to the control topic.

#### 2.6.3 Run the Sample Program

1. Click the Android Studio Run 'app' button to install the Demo.

2. Switch the bottom tab to the **device interconnection** Fragment and observe the log information in Demo and logcat. The following is the log information in logcat:
- airConditioner1 has been connected to IoT Hub and subscribed to the topic
```
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Start connecting to ssl://connect.iot.qcloud.com:8883
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: onSuccess!
com.qcloud.iot I/IoTEntryActivity: connected to ssl://connect.iot.qcloud.com:8883
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Starting subscribe topic: ******/airConditioner1/control
com.qcloud.iot I/IoTEntryActivity: onSubscribeCompleted, subscribe success
```

3. Click the **Enter** button to connect to IoT Hub and publish the control topic. The corresponding message is:
```
"{\"action\": \"come_home\", \"targetDevice\": \"airConditioner1\"}"
```
Observe the log information in Demo and logcat. The following is the log information in logcat:

- door1 publishes the topic (come_home)
```
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Start connecting to ssl://connect.iot.qcloud.com:8883
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: onSuccess!
com.qcloud.iot I/IoTEntryActivity: connected to ssl://connect.iot.qcloud.com:8883
```
- door1 publishes the topic (come_home)
```
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Starting publish topic: ******/door1/event Message: {"action": "come_home", "targetDevice": "airConditioner1"}
```
- airConditioner1 has received the topic forwarded by the rule engine
```
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Received topic: ******/airConditioner1/control, message: {"action":"come_home","targetDevice":"airConditioner1"}
com.qcloud.iot D/IoTEntryActivity: receive command: open airconditioner, count: 1
```

4. Click the **Leave** button to publish the control topic. The corresponding message is:
```
"{\"action\": \"leave_home\", \"targetDevice\": \"airConditioner1\"}"
```
Observe the log information in Demo and logcat. The following is the log information in logcat:
- door1 publishes the topic (leave_home)
```
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Starting publish topic: ******/door1/event Message: {"action": "leave_home", "targetDevice": "airConditioner1"}
```
- airConditioner1 has received the topic forwarded by the rule engine
```
com.qcloud.iot I/com.qcloud.iot.mqtt.TXMqttConnection: Received topic: ******/airConditioner1/control, message: {"action":"leave_home","targetDevice":"airConditioner1"}
com.qcloud.iot D/IoTEntryActivity: receive command: close airconditioner, count: 2
```

