[//]: # (chinagitpath:XXXXX)

## CoAP Protocol Version
Currently, IoT Hub supports CoAP standard protocol access. For details, see [RFC7252](https://tools.ietf.org/html/rfc7252) protocol document.

## Differences from Standard CoAP
1. Currently, only the reporting of messages is supported, i.e. reporting the SDK messages to IoT Hub.
2. The POST method is supported, while GET/PUT/DELETE methods are not. 

## CoAP Channel and Security Level

1. DTLS protocol is supported to establish a secure connection.
2. Asymmetric encryption is supported.

## URI Specification
The CoAP message is sent to the URI which is in the format of `/${productId}/${deviceName}/xxx`. productId is the product ID registered in the console and deviceName is the name of the device under the productId product.

By default, after a product is created, all devices under the product have the permissions of the following Topic classes:
1. `${productId}/${deviceName}/event` for publishing
2. `${productId}/${deviceName}/control` for subscribing

In other words, the URI corresponds to the MQTT topic.

