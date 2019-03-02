[//]: # (chinagitpath:XXXXX)

## MQTT Protocol Version

Currently, IoT Hub supports MQTT standard protocol access (compatible with the v3.1.1 protocol). For details, see [MQTT 3.1.1](http://mqtt.org/?spm=5176.doc30540.2.3.BU9nwt) protocol document.

## Differences from Standard MQTT

1. PUB, SUB, PING, PONG, CONNECT, DISCONNECT and UNSUB messages of MQTT are supported
2. cleanSession is supported
3. will and retain msg are not supported
4. QOS2 is not supported

## MQTT Channel and Security Level

TLSV1, TLSV1.1 and TLSV1.2 protocols are supported to establish a secure connection with high security level.

## TOPIC Specification

By default, after a product is created, all devices under the product have the permissions of the following topic classes:
1. `${productId}/${deviceName}/control` for subscription
2. `${productId}/${deviceName}/event` for publishing
3. `$shadow/operation/${productId}/${deviceName}` for publishing.
    Categorized by the internal type of the packet: update/get, which correspond to the operation of updating and pulling the device shadow document.
4. `$shadow/operation/result/${productId}/${deviceName}` for subscription.
    Categorized by internal type of the packet: update/get/delta; update and get correspond to the operation of updating and pulling the device shadow document; after you modify the device shadow document through the restAPI, the server will publish messages through this topic where the type is delta

