
IoT Hub assigns a unique product ID to each created product. You can customize the `Devicename` to identify devices and use the product ID + device ID + device certificate/key to authenticate devices. You need to select the device authentication method when creating a product. During connection, a device needs to report the information of the product, device, and corresponding key according to the specified method and can be connected to IoT Hub only after successful authentication. As different users have different requirements for device resources and security levels, IoT Hub provides multiple authentication schemes to meet the needs in different use cases.

IoT Hub provides the following three authentication schemes:
- Certificate authentication (device-level): it assigns a certificate + private key to each device and uses asymmetric encryption to authenticate the access. You need to burn different configuration information for each device.
- Key authentication (device-level): it assigns a device key to each device and uses symmetric encryption to authenticate the access. You need to burn different configuration information for each device.
- Dynamic registration authentication (product-level): it assigns a unified key to all devices under the same product, and a device gets a device certificate/key through a registration request for authentication. You can burn the same configuration information for the same batch of devices.

The three schemes have their own pros and cons in terms of ease of use, security, and device resource requirement. You can comprehensively evaluate them and choose the most appropriate one according to your own business scenarios. They are as compared below:

| Feature | Certificate Authentication | Key Authentication | Dynamic Registration Authentication |
|--------|--------|--------|--------|
| Burned device information | `ProductId`, `Devicename`, <br>device certificate, and device private key | `ProductId`, `Devicename`, and device key | `ProductId`, `Devicename`, and `ProductSecret` |
| Whether device creation is required | Yes | Yes | Devices can be automatically created according to the `Devicename` carried in the registration request. |
| Security | High | Average | Average |
| Use limit | Up to 1 million devices can be created under one product. | Up to 1 million devices can be created under one product. | Up to 1 million devices can be created under one product. You can customize the maximum number of devices automatically created through registration requests. |
| Device resource requirement | High, with TLS support required | Low | Low, with only AES support required |


