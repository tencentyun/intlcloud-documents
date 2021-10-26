
In addition to the device connection feature, the SDK for Python also provides gateway subdevice and device shadow features with the following APIs.

## MQTT APIs 

MQTT APIs are defined in the [hub.py](https://github.com/tencentyun/iot-device-python/blob/master/hub/hub.py) class and support publishing and subscribing. If you want to support the device shadow feature, you need to use the [shadow.py](https://github.com/tencentyun/iot-device-python/blob/master/hub/services/shadow/shadow.py) class and its methods as detailed below:

| Method | Description |
| ---------------- | ------------------------ |
| connect           | Establishes MQTT connection                |
| disconnect           | Closes MQTT connection               |
| subscribe           | Subscribes to topic over MQTT                |
| unsubscribe           | Unsubscribes from topic over MQTT                |
| publish           | Publishes message over MQTT                |
| registerMqttCallback           | Registers MQTT callback function               |
| registerUserCallback           | Registers user callback function                 |
| isMqttConnected           | Checks whether MQTT is normally connected                |
| getConnectState | Gets MQTT connection status |
| setReconnectInterval           | Sets MQTT reconnection attempt interval               |
| setMessageTimout           | Sets message sending timeout period                 |
| setKeepaliveInterval           | Sets MQTT keepalive interval               |


## MQTT Gateway APIs 

- Devices that don't have direct access to the Ethernet can be connected to the network of the local gateway device first and then connected to the IoT Hub platform through the communication feature of the gateway device.
- For the subdevices that join or leave the LAN, they need to be bound or unbound through the platform.

>!After a subdevice is connected once, as long as the gateway is successfully connected subsequently, the backend will show that the subdevice is online until it is disconnected.
>
MQTT gateway APIs are defined in the [gateway.py](https://github.com/tencentyun/iot-device-python/blob/master/hub/services/gateway/gateway.py) class as detailed below:

| Method | Description |
| -------------------- | ------------------------ |
| gatewayInit              |Initializes gateway             |
| isSubdevStatusOnline              |Determines whether subdevice is connected             |
| updateSubdevStatus              |Updates subdevice's connection status             |
| gatewaySubdevGetConfigList              |Gets subdevice list from configuration file             |
| gatewaySubdevOnline              |Proxies subdevice connection            |
| gatewaySubdevOffline              |Proxies subdevice disconnection             |
| gatewaySubdevBind              |Binds subdevice             |
| gatewaySubdevUnbind              |Unbinds subdevice             |
| gatewaySubdevSubscribe              |Proxies subdevice subscription             |

## Dynamic Registration APIs

If you want to use the dynamic registration feature, you need to use the APIs in the [hub.py](https://github.com/tencentyun/iot-device-python/blob/master/hub/hub.py) class as detailed below:

| Method | Description |
| --------------------- | ------------------------------------ |
| dynregDevice               |Gets the dynamic registration information of device                             |

## OTA APIs
If you want to use the OTA feature, you need to use the APIs in the [hub.py](https://github.com/tencentyun/iot-device-python/blob/master/hub/hub.py) class as detailed below:

| Method | Description |
| --------------------- | ------------------------------------ |
| otaInit               |Initializes OTA                            |
| otaIsFetching               |Determines whether the download is in progress                             |
| otaIsFetchFinished               |Determines whether the download is completed                             |
| otaReportUpgradeSuccess               |Reports update success message                             |
| otaReportUpgradeFail               | Reports update failure message                             |
| otaIoctlNumber               | Gets the information of the downloaded firmware in `int` type, such as the size                           |
| otaIoctlString               | Gets the information of the downloaded firmware in `String` type, such as MD5                        |
| otaResetMd5               | Resets MD5 information                           |
| otaMd5Update               | Updates MD5 information                           |
| httpInit               | Initializes HTTP                            |
| otaReportVersion               | Reports the information of current firmware version                             |
| otaDownloadStart               | Starts firmware download                             |
| otaFetchYield               | Reads firmware                             |
