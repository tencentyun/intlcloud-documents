## Overview
COS allows you to set object access permissions, which have a higher priority than that for buckets.

>?
>- Object access permissions take effect only when the access is made via the default endpoint. For any access made via a CDN acceleration endpoint or a custom endpoint, bucket access permissions will take effect.
>- There are limits on the number of ACL rules. For more information, please see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Find the bucket where the target object is located and click the bucket name to enter the bucket details page.
3. Choose the **File List** tab, find the object for which you want to configure the access permission, and click **Details** on the right to enter the file details page (If it is a folder, click **Permissions** on the right).
![](https://main.qcloudimg.com/raw/f2f66b873867b3645fa69ec4f9ffe646.png)
4. In the **Object ACL** area, configure ACL as needed (for example, grant a sub-account the object permissions). Sub-account ID can be found in the [CAM console](https://console.cloud.tencent.com/cam). COS supports two types of permissions for objects:
 -**Public Permissions**: includes **Inherit**, **Private Read/Write**, and **Public Read/Private Write**. For more information about public permissions, please see [Access Permission Types](https://intl.cloud.tencent.com/document/product/436/13324#access-permission-types).
 -**User ACL**: The root account has all object permissions (full control) by default. You can also add sub-accounts and grant them permissions including read/write, read/write ACL, and even **full control**.
![](https://main.qcloudimg.com/raw/c9565ab1d2378ce672a301843bf3b072.png)
5. Click **Save**.
6. If you need to configure or modify access permissions for multiple objects at a time, you can select the objects on the **File List** page and then click **More Actions** > **Modify Access Permission**.
![](https://main.qcloudimg.com/raw/a00d8522c2698c39aa4687463bcb05e4.png)

