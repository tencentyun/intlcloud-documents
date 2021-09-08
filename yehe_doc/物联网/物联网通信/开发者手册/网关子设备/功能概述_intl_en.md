## Device Classification

The IoT Hub platform divides devices into the following two categories (i.e., node categories) according to their functionality:

- **General device**: this device category is further divided into two types: devices that have the ability to connect to the platform, and devices that can connect to the platform through gateway devices.
- **Gateway device**: this category of device can directly connect to the platform and can accept subdevices for them to join the LAN.

## Overview

Devices that don't have direct access to the Ethernet can be connected to the network of the local gateway device first and then connected to the IoT Hub platform through the communication feature of the gateway device. For the subdevices that join or leave the LAN, the gateway device can bind or unbind them on the platform and report the topological relationships with them, so as to implement the real-time monitoring of all devices in the LAN by the platform.

## Connection Method

- Gateway devices can be connected to the IoT Hub platform in the same way as general devices. For more information, please see [Device Connection](https://intl.cloud.tencent.com/document/product/1105/41842). After a gateway device is connected, it can connect/disconnect subdevices in the same LAN to/from the platform and manage the topological relationships between them.
- Subdevices can be connected to the platform through a gateway device after successful authentication in the following two ways:
  **Device-level key authentication**
    The gateway device gets the device certificate or key of the subdevice, generates the subdevice binding signature string, reports it to the platform, and completes the identity verification on behalf of the subdevice.
  **Product-level key authentication**
    The gateway device gets the `ProductKey` (product key) of the subdevice, generates a signature, and sends a dynamic registration request to the platform. After successful authentication, the platform will return the `DeviceCert` or `DeviceSecret` of the subdevice, based on which the gateway will generate the subdevice binding signature string and report it to the platform. Then, after successful verification, the subdevice can be connected.

