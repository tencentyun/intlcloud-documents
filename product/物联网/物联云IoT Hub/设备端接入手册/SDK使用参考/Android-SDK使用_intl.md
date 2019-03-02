# Using the Device-side SDK

There are two scenarios for using device-side SDK:

- If app and IoT-SDK run in the same process, then app only has to rely on iot_core module.
- If app and IoT-SDK need to run in different processes, then app only has to rely on the iot_service module.

**Note:**
- The iot_service module relies on the iot_core module.
- The iot_core module relies on the MQTT protocol **eclipse.paho** implemented by the open-source community.

## SDK API Description

### MQTT API - TXMqttConnection

| No. | Method name | Description |
| ---- | ---------------------------- | -----------------------------------|
| 1 | connect | Establish an MQTT connection |
| 2 | reconnect | Re-establish an MQTT connection |
| 3 | disConnect | Close an MQTT connection |
| 4 | publish | Publish an MQTT message |
| 5 | subscribe | Subscribe to an MQTT topic |
| 6 | unSubscribe | Unsubscribe from an MQTT topic |
| 7 | getConnectStatus | Get the MQTT connection status |
| 8 | setBufferOpts | Set the buffer for disconnection status |
| 9 | initOTA | Initialize OTA function |
| 10 | reportCurrentFirmwareVersion | Report the current version information of the device to the backend server |
| 11 | reportOTAState | Report the upgrade status of the device to the backend server |

### Device Shadow API - TXShadowConnection

| No. | Method name | Description |
| ---- | -----------------------------------| ----------------------------------  |
| 1 | connect | Establish a shadow connection |
| 2 | disConnect | Close a shadow connection |
| 3 | getConnectStatus | Get the MQTT connection status |
| 4 | update | Update the device shadow document |
| 5 | get | Get the device shadow document |
| 6 | registerProperty | Register device attributes |
| 7 | unRegisterProperty | Unregister device attributes |
| 8 | reportNullDesiredInfo | Report the empty desired information after updating the delta information |
| 9 | setBufferOpts | Set the buffer for disconnection status |
| 10 | getMqttConnection | Get an TXMqttConnection instance |

### MQTT Remote Service Client - TXMqttClient

| No. | Method name | Description |
| ---- | -----------------------------------| -------------------------------- |
| 1 | setMqttActionCallBack | Set the MqttAction callback API |
| 2 | setServiceConnection | Set the remote service connection callback API |
| 3 | init | Initialize the remote service client |
| 4 | startRemoteService | Start the remote service |
| 5 | stopRemoteService | Stop the remote service |
| 6 | connect | Establish an MQTT connection |
| 7 | disConnect |  Close an MQTT connection |
| 8 | subscribe | Subscribe to an MQTT topic |
| 9 | unSubscribe | Unsubscribe from an MQTT topic |
| 10 | publish | Publish MQTT News |
| 11 | setBufferOpts | Set the buffer for disconnection status |
| 12 | clear | Release the resource |

### Shadow Remote Service Client - TXShadowClient

| No. | Method name | Description |
| ---- | -----------------------------------| -----------------------------------   |
| 1 | setShadowActionCallBack | Set the ShadowAction callback API |
| 2 | setServiceConnection | Set the remote service connection callback API |
| 3 | init | Initialize the remote service client |
| 4 | startRemoteService | Start the remote service |
| 5 | stopRemoteService | Stop the remote service |
| 6 | connect | Establish a shadow connection |
| 7 | disConnect |  Close a shadow connection |
| 8 | getMqttClient | Get an MQTT client instance |
| 9 | get | Get a device shadow |
| 10 | update | Update a device shadow |
| 11 | registerProperty | Register device attributes |
| 12 | unRegisterProperty | Unregister device attributes |
| 13 | reportNullDesiredInfo | Report the empty desired information after updating the delta information |
| 14 | setBufferOpts | Set the buffer for disconnection status |
| 15 | clear | Release the resource |

### MQTT Channel Firmware Upgrade - TXMqttClient

| No. | Method name | Description |
| ---- | -----------------------------------| -------------------------------- |
| 1 | initOTA | Initialize the OTA function |
| 2 | reportCurrentFirmwareVersion | Report the current version information of the device to the backend server |
| 3 | reportOTAState | Report the upgrade status of the device to the backend server |
