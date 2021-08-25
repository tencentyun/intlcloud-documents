
IoT Hub supports the MQTT v3.1.1 protocol and supports the quality of service levels of QoS 0 and QoS 1 (but not QoS 2). Using an MQTT persistent session can save the subscription status of devices and subscribed messages that devices have not received. When a device goes offline and goes online again, it can restore the previous session to receive subscribed messages sent when it was offline.

## Creating MQTT Persistent Session on Device

When a device is connected to IoT Hub, the `CleanSession` flag in the variable header part of the `Connect` message can be set to 0. IoT Hub will determine the session status of the device according to the `ClientId` when the device is connected. If there is no session currently, it will create a persistent session. If there is an existing session, it will communicate with the device based on the session process.

## IoT Hub Response Description

After the device sends a `Connect` message, IoT Hub will return a `Connack` message, in which the connection confirmation flag `SessionPresent` indicates whether IoT Hub includes the session status corresponding to the `ClientId` when the device is connected. If `SessionPresent` is 0, no persistent session is created, and the device needs to establish the session status again. If `SessionPresent` is 1, a persistent session has been created.
- After the device is successfully connected, if it enters an existing persistent session, IoT Hub will send the stored QoS 1 messages and unacknowledged QoS 1 messages to the device.
- After the device is successfully connected, if a new persistent session is created, IoT Hub will save the subscription status of the device and store the QoS 1 (excluding QoS 0) messages that the device has subscribed to when it is offline. When it goes online again, IoT Hub will send the stored QoS 1 messages and unacknowledged QoS 1 messages to it.

>?
>- IoT Hub sends the stored QoS 1 messages sequentially at 500 ms intervals.
>- Only QoS 1 messages can be stored in a persistent session. Up to 150 messages can be stored for a maximum of 24 hours for each device.

## Closing MQTT Persistent Session

The MQTT persistent session can be closed in the following two ways:
- When connecting the device to IoT Hub, set the `CleanSession` flag in the variable header part of the `Connect` message to 1.
- When the device is disconnected for **more than 24 hours**, the persistent session will be closed automatically.

>?Device disconnections include disconnection caused by the device sending the `disconnect` message and disconnection caused by the device communication timeout.
