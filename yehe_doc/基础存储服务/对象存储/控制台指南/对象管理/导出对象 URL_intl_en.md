## Overview

The COS console allows you to export the URLs of objects in a bucket, including objects that have been uploaded or in a folder. Batch export is supported.

>? You can export up to 100 object URLs at a time, meaning you can select a maximum of 100 objects.
> If you need to export more than 100 object URLs, you can use APIs or SDKs. For more information, please see [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614).
> 


## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Select the desired objects, click **More Actions** > **Export URLs**.
![](https://qcloudimg.tencent-cloud.cn/raw/c57396478589b196ea4004b90ada6779.png)
6. In the pop-up window, configure the following information:
![](https://qcloudimg.tencent-cloud.cn/raw/f4c16f13088c60f5908921b5f5c2702d.png)
**Protocol**: HTTPS is selected by default. You can select HTTPS or HTTP as needed.
**Specified Domain**: the default origin domain is supported.
**Expiration Time**: The default value is 60 minutes. You can set it to an integer ranging from 5 to 60.
7. Click **Confirm** to export the object URLs.
8. In the exported file, you can view the object names and object URLs. Note that you need to view the URLs within the validity period.
