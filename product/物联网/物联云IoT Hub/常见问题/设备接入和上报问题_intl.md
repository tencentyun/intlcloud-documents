[//]: # (chinagitpath:XXXXX)

### Resources occupied by the device-side SDK:
- MQTT + certificate = 20 KB (Stack) + 81 KB (Heap) = 101 KB
- MQTT + PSK (TLS) = 20 KB (Stack) + 78 KB (Heap) = 98 KB
- MQTT + PSK (NOTLS) = 20 KB (Stack) + 72 KB (Heap) = 92 KB
- CoAP + certificate = 20 KB (Stack) + 81 KB (Heap) = 101 KB
- CoAP + PSK (TLS) = 20 KB (Stack) + 77 KB (Heap) = 97 KB
- HTTPS = 24 KB (Stack) + 81 KB (Heap) = 105 KB

### My device’s RAM is small. What can be done to reduce SDK’s RAM usage?
Two suggestions. When we look at the SDK’s RAM usage, we found that getaddrinfo system function occupies 64 KB of Heap memory, which is used for IPV6. If SDK only uses IPV4, you can consider to remove the getaddrinfo memory allocation operation, which saves about 20-64 KB of RAM, subject to connection method.

Additionally, you can use the MQTT + PSK (NOTLS) method, which saves about 6 KB of RAM when there is no TLS data encryption. However, it is at the expense of data security which may lead to data theft and tampering. Use it at your discretion.

### Software environment required by device connection.
The device-side SDK has two main requirements for the software environment: support multi-tasking operating systems and support TCP/IP protocol stack.

Common reasons for failed TLS connection:
1. Wrong certificate or key. Common errors include extra spaces in the key or mismatch between the certificate file name and file name in the code.
2. For certificate-based connections, clock sync is not performed locally, causing the TLS connection to fail. The ntp client (clock sync software) needs to be installed locally.

### What if the device connection times out?
First, confirm that the local network can connect to IoT Hub. Below are some commonly used tools:
- ping iotcloud-mqtt.gz.tencentdevices.com   This is to check whether the server is accessible;
- telnet iotcloud-mqtt.gz.tencentdevices.com 443   This is to check port connection;
- If the execution results of the commands above are normal, you may also need to check the local firewall policy.
- If it is confirmed that the local network is normal, the default connection timeout value may be too low. You can try to modify the value of the macro definition in the src/sdk-impl/qcloud_iot_export.h file.
- #define QCLOUD_IOT_MQTT_COMMAND_TIMEOUT   (5 * 1000)
- #define QCLOUD_IOT_TLS_HANDSHAKE_TIMEOUT    (5 * 1000)

### What if device keeps disconnecting?
The device-side SDK provided by IoT Hub has the reconnection logic in case of device disconnection. If you are using your own SDK, you need to add the reconnection logic on your own.

### What if the device keeps going online and offline?
The IoT access layer has the logic of exclusive device login. If the same device ID is logged in to in different places, the existing login will be kicked offline by the new login. Therefore, if the device keeps disconnecting, you can check if there are different users or threads trying to login under the same device ID.

### Why does the device fail to send messages?
Common reasons include:
1. The topic that sends the messages does not have the publishing permission. You can go to the device's permission list in the console and check whether the device has the publishing permission.

>Note: You need to grant the publishing permission to the data topic in the IoT Hub Demo before it can be subscribed to successfully.

2. The topic is written incorrectly. Make sure that there is no extra or missing character such as extra space, '/' or omitted letter for topic written in the code.
3. The IoT access layer has a heartbeat mechanism. The device will be disconnected if the device does not submit a heartbeat packet within specified time period.





