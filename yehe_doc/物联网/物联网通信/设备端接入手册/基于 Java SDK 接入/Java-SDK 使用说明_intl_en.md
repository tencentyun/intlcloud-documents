
In addition to the device connection feature, the SDK for Java also provides gateway subdevice and device shadow features with the following APIs.

## MQTT APIs 

The APIs related to MQTT are defined in the `TXMqttConnection` class and support publishing and subscribing. If you want to support the device shadow feature, you need to use the `TXShadowConnection` class and its methods. `TXMqttConnection` class APIs are as detailed below:

| Method | Description |
| ---------------- | ------------------------ |
| connect | Establishes MQTT connection |
| reconnect | Reestablishes MQTT connection |
| disConnect | Closes MQTT connection |
| publish | Publishes MQTT message |
| subscribe | Subscribes to MQTT topic |
| unSubscribe | Unsubscribes from MQTT topic |
| getConnectStatus | Gets MQTT connection status |
| setBufferOpts | Sets buffer for disconnection status |


## MQTT Gateway APIs 

- Devices that don't have direct access to the Ethernet can be connected to the network of the local gateway device first and then connected to the IoT Hub platform through the communication feature of the gateway device.
- For the subdevices that join or leave the LAN, they need to be bound or unbound through the platform.

>!After a subdevice is connected once, as long as the gateway is successfully connected subsequently, the backend will show that the subdevice is online until it is disconnected.
>
The APIs related to MQTT gateway are defined in the `TXGatewayConnection` class as detailed below:

| Method | Description |
| -------------------- | ------------------------ |
| connect | Establishes gateway MQTT connection |
| reconnect | Reestablishes gateway MQTT connection |
| disConnect | Closes gateway MQTT connection |
| publish | Publishes MQTT message |
| subscribe | Subscribes to MQTT topic |
| unSubscribe | Unsubscribes from MQTT topic |
| getConnectStatus | Gets MQTT connection status |
| setBufferOpts | Sets buffer for disconnection status |
| gatewaySubdevOffline | Connects subdevice |
| gatewaySubdevOnline | Disconnects subdevice |
| gatewayBindSubdev | Binds subdevice |
| gatewayUnbindSubdev | Unbinds subdevice |

## Device Shadow APIs

If you want to support the device shadow feature, you need to use the APIs in the `TXShadowConnection` class as detailed below:

| Method | Description |
| --------------------- | ------------------------------------ |
| connect | Establishes MQTT connection |
| reconnect | Reestablishes MQTT connection |
| disConnect | Closes MQTT connection |
| publish | Publishes MQTT message |
| subscribe | Subscribes to MQTT topic |
| unSubscribe | Unsubscribes from MQTT topic |
| update | Updates device shadow document |
| get | Gets device shadow document |
| reportNullDesiredInfo | Reports the empty `desired` information after updating `delta` information |
| setBufferOpts | Sets buffer for disconnection status |
| getMqttConnection | Gets `TXMqttConnection` instance |
| getConnectStatus | Gets MQTT connection status |
