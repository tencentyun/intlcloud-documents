### Directions for SDK for C
#### Program implementation
As an example, the energy consumption status is reported to the device shadow through the call of `IOT_Shadow_Update` by the following function in the SDK code `sample/scenarized/aircond_shadow_sample_v2.c`. Then, the corresponding callback function is registered to handle the response of the device shadow. You can customize the reported attributes here.
```
_do_report_energy_consumption(...)
...
IOT_Shadow_Update(...)
```

#### Program compilation and execution
1. Run `./aircond_shadow_sample_v2`. Please note that if MQTT asymmetric encryption is used, the root certificate, device certificate, and device key files should be placed in the parent directory of `./../certs`.
2. Call the relevant RESTful API to get the status data of the shadow. For detailed directions, please see "Querying and getting device information". Observe the output log of the demo:
![get_device_shadow_v1](https://mc.qcloudimg.com/static/img/056271af1bc4dc824ab479d2f0f0a9f2/2-6.png)
3. Run `./door_mqtt_sample come_home/leave_home airConditioner1`. `door1` will communicate with `airConditioner1`, and then `airConditioner1` will be instructed to turn on through the rule engine. The reported changes in energy consumption and indoor temperature can be observed in the log, and the shadow data is obtained again through the RESTful API (as detailed in step 2):
![get_device_shadow_v2](https://mc.qcloudimg.com/static/img/65954fa964691d52bce646f45246ab2d/airdelta.png)

It can be seen that after `airConditioner1` is turned on, the air conditioner energy consumption is dynamically reported to the shadow, and the data can be successfully queried and obtained through the RESTful API.

### Directions for SDK for Android
#### Program implementation
Please see the instructions in [Directions for SDK for Android - Program implementation](https://intl.cloud.tencent.com/document/product/1105/41468).

#### Program compilation and execution
Please see the instructions in [Directions for SDK for Android - Program compilation and execution](https://intl.cloud.tencent.com/document/product/1105/41468).

### Querying and getting device information
Call the RESTful API GetDeviceShadow to get the status data of the shadow, which is used by the application to display the device's energy consumption.
The RESTful API request parameter is: `deviceName=airConditioner1, productName=AirConditioner`.
