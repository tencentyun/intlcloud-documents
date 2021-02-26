## Overview
You can store all your static resources such as static scripts, audio/video files, images, and attachments in standard storage in COS, which features unlimited capacity and high-frequency reads/writes to provide scalable and reliable storage for static resources and reduce pressure on resource servers. In addition, static resources in COS can be connected to CDN for fast global delivery to clients.

## Billing
When COS serves as an origin server of CDN, billing consists of two parts: CDN billing (for acceleration) and COS billing (for origin-pulling).

### CDN Billing
When CDN obtains resources from a nearby CDN node and delivers them to clients, the traffic consumed will be charged by CDN billing. For more information, please see [CDN Billing](https://intl.cloud.tencent.com/document/product/228/2949).

### COS Billing
When CDN pulls resources from a COS origin server, the traffic consumed will be charged by COS billing. For more information, please see [COS Billing](https://intl.cloud.tencent.com/document/product/436/16871).
![](https://main.qcloudimg.com/raw/b56373823fef5c83d7499034abf708e6.png)




