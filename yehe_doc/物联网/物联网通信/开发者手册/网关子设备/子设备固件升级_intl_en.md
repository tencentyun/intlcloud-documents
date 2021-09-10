## Overview

When a subdevice under a gateway has new features available or vulnerabilities that need to be fixed, firmware update can be quickly performed for it through the device firmware update service.


## How It Works

During the firmware update process, the gateway needs to use the following two topics to communicate with the cloud on behalf of the subdevice:
![OTA topic](https://main.qcloudimg.com/raw/716d837e1fcfd4b3441171436a8f3930.png)

Below is the sample code:
```php
$ota/report/${productID}/${deviceName}
This topic is used to publish (upstream) messages, through which the device reports the version number and the download/update progress to the cloud.
$ota/update/${productID}/${deviceName}
This topic is used to subscribe to (downstream) messages, through which the device receives the update message from the cloud.
```


## Process

Taking MQTT as an example, the update process of the subdevice is as follows:
>?For the specific directions of firmware update, please see [Device Firmware Update](https://intl.cloud.tencent.com/document/product/1105/41507).
>
![](https://main.qcloudimg.com/raw/08f08cfb2fe06fba6d9ced1a2bc76e16.png)




