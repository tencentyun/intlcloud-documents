
In addition to the device connection feature, the SDK for Android also provides gateway subdevice, device shadow, and OTA features with the following APIs.

### MQTT APIs  

#### TXMqttConnection

| Method | Description |
| ---------------------------- | -------------------------------- |
| connect | Establishes MQTT connection |
| reconnect | Reestablishes MQTT connection |
| disConnect | Closes MQTT connection |
| publish | Publishes MQTT message |
| subscribe | Subscribes to MQTT topic |
| unSubscribe | Unsubscribes from MQTT topic |
| getConnectStatus | Gets MQTT connection status |
| setBufferOpts | Sets buffer for disconnection status |
| initOTA | Initializes OTA feature |
| reportCurrentFirmwareVersion | Reports current device version information to backend server |
| reportOTAState | Reports device update status to backend server |


### MQTT Gateway APIs 

#### TXGatewayConnection

| Method | Description |
| ---------------------------- | -------------------------------- |
| connect | Establishes gateway connection |
| reconnect | Reestablishes gateway connection |
| disConnect | Closes gateway MQTT connection |
| publish | Publishes MQTT message |
| subscribe | Subscribes to MQTT topic |
| unSubscribe | Unsubscribes from MQTT topic |
| getConnectStatus | Gets MQTT connection status |
| setBufferOpts | Sets buffer for disconnection status |
| initOTA | Initializes OTA feature |
| reportCurrentFirmwareVersion | Reports current device version information to backend server |
| reportOTAState | Reports device update status to backend server |
| addSubDev | Adds subdevice |
| removeSubdev | Removes subdevice |
| findSubdev | Finds subdevice |
| gatewaySubdevOffline | Connects subdevice |
| gatewaySubdevOnline | Disconnects subdevice |


### Device Shadow APIs 

#### TXShadowConnection

| Method | Description |
| --------------------- | ---------------------------------------- |
| connect | Establishes shadow connection |
| disConnect | Closes shadow connection |
| getConnectStatus | Gets MQTT connection status |
| update | Updates device shadow document |
| get | Gets device shadow document |
| registerProperty | Registers device attribute |
| unRegisterProperty | Unregisters device attribute |
| reportNullDesiredInfo | Reports empty `desired` information after updating `delta` information |
| setBufferOpts | Sets buffer for disconnection status |
| getMqttConnection | Gets `TXMqttConnection` instance |

### MQTT Remote Service Client 

#### TXMqttClient

| Method | Description |
| --------------------- | -------------------------- |
| setMqttActionCallBack | Sets `MqttAction` callback API |
| setServiceConnection | Sets remote service connection callback API |
| init | Initializes remote service client |
| startRemoteService | Starts remote service |
| stopRemoteService | Stops remote service |
| connect | Establishes MQTT connection |
| disConnect | Closes MQTT connection |
| subscribe | Subscribes to MQTT topic |
| unSubscribe | Unsubscribes from MQTT topic |
| publish | Publishes MQTT message |
| setBufferOpts | Sets buffer for disconnection status |
| clear | Releases resource |

### Shadow Remote Service Client 

#### TXShadowClient

| Method | Description |
| ----------------------- | ---------------------------------------- |
| setShadowActionCallBack | Sets `ShadowAction` callback API |
| setServiceConnection | Sets remote service connection callback API |
| init | Initializes remote service client |
| startRemoteService | Starts remote service |
| stopRemoteService | Stops remote service |
| connect | Establishes shadow connection |
| disConnect | Closes shadow connection |
| getMqttClient | Gets MQTT client instance |
| get | Gets device shadow |
| update | Updates device shadow |
| registerProperty | Registers device attribute |
| unRegisterProperty | Unregisters device attribute |
| reportNullDesiredInfo | Reports empty `desired` information after updating `delta` information |
| setBufferOpts | Sets buffer for disconnection status |
| clear | Releases resource |

### Firmware Update over MQTT Channel 

#### TXMqttClient

| Method | Description |
| ---------------------------- | -------------------------------- |
| initOTA | Initializes OTA feature |
| reportCurrentFirmwareVersion | Reports current device version information to backend server |
| reportOTAState | Reports device update status to backend server |
