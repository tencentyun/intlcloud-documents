## Overview

When a subdevice under a gateway has new features available or vulnerabilities that need to be fixed, firmware update can be quickly performed for it through the device firmware update service.


## How It Works

During the firmware update process, the gateway needs to use the following two topics to communicate with the cloud on behalf of the subdevice:
![OTA topic](https://main.qcloudimg.com/raw/04b41acfb677914a49f5c2ee890dc6a7.png)

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
![](https://main.qcloudimg.com/raw/4201f843615d0b54a9a4274e8c2d4b4d.png)




