

## MQTT-WebSocket Overview

The IoT Hub platform supports MQTT communication based on WebSocket, so that devices can use the MQTT protocol for message transfer on the basis of the WebSocket protocol. In this way, browser-based applications can implement data communication with the platform and devices connected to the platform. In addition, WebSocket uses ports 443/80, which means that messages can pass through most firewalls during transfer.

## MQTT-WebSocket Connection

As both the MQTT-WebSocket and MQTT-TCP protocols ultimately transfer messages based on MQTT, they have the same parameters for MQTT connection. The main difference lies in the protocol and port of the MQTT connection to the platform. Key-authenticated devices use WS for connection, while certificate-authenticated devices use WSS, i.e., WS+TLS.

#### Guide to connecting certificate-authenticated device

1. Download files such as the certificate and device private key.
2. Connect to the domain name. For devices in the Guangzhou region, connect to `${ProductId}.ap-guangzhou.iothub.tencentdevices.com:443`, where `${ProductId}` is the product ID.
3. Set the MQTT connection parameters:
The connection parameter settings are the same as those for MQTT-TCP connection. For more information, please see the MQTT connection section in [MQTT-Based Device Connection over TCP](https://intl.cloud.tencent.com/document/product/1105/41824).
```plaintext
UserName:${productid}${devicename};${sdkappid};${connid};${expiry}
PassWord: password (you can set any value)
ClientId:${ProductId}${DeviceName}
KeepAlive: time to keep the connection alive. Value range: 0–900s
```


#### Guide to connecting key-authenticated device
1. Get the device key.
2. Connect to the domain name. For devices in the Guangzhou region, connect to `${ProductId}.ap-guangzhou.iothub.tencentdevices.com:80`, where `${ProductId}` is the product ID.
3. Set the MQTT connection parameters:
The connection parameter settings are the same as those for MQTT-TCP connection. For more information, please see the "Guide to connecting key-authenticated device" section in [MQTT-Based Device Connection over TCP](https://intl.cloud.tencent.com/document/product/1105/41824).
```plaintext
UserName:${productid}${devicename};${sdkappid};${connid};${expiry}
PassWord:${token};hmac signature algorithm
ClientId:${ProductId}${DeviceName}
KeepAlive: time to keep the connection alive. Value range: 0–900s
```



