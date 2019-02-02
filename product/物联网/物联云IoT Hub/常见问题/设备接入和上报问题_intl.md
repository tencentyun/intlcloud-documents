[//]: # (chinagitpath:XXXXX)

### How many resources does the device-side SDK use?
- MQTT + certificate = 20 KB (Stack) + 81 KB (Heap) = 101 KB
- MQTT + PSK (TLS) = 20 KB (Stack) + 78 KB (Heap) = 98 KB
- MQTT + PSK (NOTLS) = 20 KB (Stack) + 72 KB (Heap) = 92 KB
- CoAP + certificate = 20 KB (Stack) + 81 KB (Heap) = 101 KB
- CoAP + PSK (TLS) = 20 KB (Stack) + 77 KB (Heap) = 97 KB
- HTTPS = 24 KB (Stack) + 81 KB (Heap) = 105 KB

### My device has a small RAM. Is there any way to reduce the memory usage by the SDK?
There are two suggestions for optimization. First, the getaddrinfo system function allocates 64 KB of Heap memory which is used for IPV6; if the SDK only uses IPV4, you can consider removing the memory allocation operation by getaddrinfo, which saves about 20-64 KB of RAM subject to the connection method.

Second, you can use the MQTT + PSK (NOTLS) method, which saves about 6 KB of RAM if there is no TLS data encryption. However, this will sacrifice data security and lead to the risk of data theft and tampering. Please be cautious when doing so.

### What are the requirements of device access for the software environment?
The device-side SDK has two main requirements for the software environment: support for a multi-tasking operating systems and support for the TCP/IP protocol stack.

Common reasons for TLS connection failures include:
1. The certificate or key used is incorrect. Some of the common errors are extra spaces in the key or mismatch between the certificate file name and the file name written in the code.
2. For certificate-based connections, clock sync is not performed locally, causing the TLS connection to fail. The ntp client (clock sync software) needs to be installed locally.

### What if the device connection times out?
First, confirm that the local network can connect to IoT Hub. Below are some commonly used tools:
- ping iotcloud-mqtt.gz.tencentdevices.com   This is to check whether the server is reachable;
- telnet iotcloud-mqtt.gz.tencentdevices.com 443   This is to check the port connectivity;
- If the execution results of the commands above are normal, you may also need to check the local firewall policy.
- If it is confirmed that the local network is normal, the default connection timeout value may be too low. You can try to modify the value of the macro definition in the src/sdk-impl/qcloud_iot_export.h file.
- #define QCLOUD_IOT_MQTT_COMMAND_TIMEOUT   (5 * 1000)
- #define QCLOUD_IOT_TLS_HANDSHAKE_TIMEOUT    (5 * 1000)

### What if there is no automatic reconnection after the device is disconnected?
The device-side SDK provided by IoT Hub has the reconnection logic in case of device disconnection. If you are using your own SDK, you need to add the reconnection logic on your own.

### What if the device keeps going online and offline?
The IoT access layer has the logic of exclusive device login. If the same device ID is logged in to in different places, the existing login will be kicked offline by the new login. Therefore, if the device keeps going online and offline, you can check whether there are different users or threads performing login operations using the same device ID.

### Why does the device fail to send messages?
Common reasons include:
1. The topic that sends the messages does not have the publishing permission. You can go to the device's permission list in the console and check whether the device has the publishing permission.

>Note: You need to grant the publishing permission to the data topic in the IoT Hub Demo before it can be subscribed to successfully.

2. The topic is written incorrectly. Check that the topic written in the code has no extra characters such as spaces, '/' or omitted letters.
3. The connection is broken. The IoT access layer has a heartbeat mechanism. If the device does not submit a heartbeat packet within a specified time period, it will be disconnected.





