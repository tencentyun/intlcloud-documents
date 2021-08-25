
Currently, IoT Hub supports connection over the standard CoAP protocol. For more information, please see [RFC 7252](https://tools.ietf.org/html/rfc7252).

## Differences from Standard CoAP

1. Currently, only message reporting is supported, i.e., reporting SDK messages to IoT Hub.
2. The POST method is supported, while GET/PUT/DELETE methods are not. 

## Security Level of CoAP Channel

1. DTLS protocol is supported to establish a secure connection.
2. Asymmetric encryption is supported.

## Connection Parameters

1. Server address. For devices in the Guangzhou region, enter `${ProductId}.iotcloud.tencentdevices.com`. Here, `${ProductId}` is a variable parameter, and you should replace it with the product ID automatically generated when you create the product.
2. The connection port is 5684.

## URI Specification

The CoAP message is sent to the URI in the format of `/${productId}/${deviceName}/xxx`, where `productId` is the product ID registered in the console, and `deviceName` is the name of the device under the `productId`.

By default, after a product is created, all devices under it will have the permissions of the following topic classes:

1. `${productId}/${deviceName}/event` for publishing
2. `${productId}/${deviceName}/control` for subscribing
3. `${productId}/${deviceName}/data` for publishing and subscribing

In other words, the URI corresponds to the MQTT topic.



