## Overview
The maximum upload size is the maximum data volume that can be uploaded in a single client request. You can restrict it to improve the data transfer efficiency and optimize the network transfer.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **Network optimization** on the left sidebar.
2. On the network optimization page, select the target site and click **Settings** in the maximum upload size module.
![](https://qcloudimg.tencent-cloud.cn/raw/264a3540260aab5edb1314d4870bda28.png)
3. In the maximum upload size pop-up window, enable **Size limit**, enter an upper limit value, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/26d31b3c805094698bf48c50fc86bf0a.png)

**Parameter description:**
 - Size limit: It is enabled by default. If it is disabled, you can upload data in any size (the platform uses streaming transfer).
 - Upper limit: After the size limit is enabled, you can set an upper limit between 1 and 500 MB.

## Notes
The configuration here takes effect before the origin server configuration.
