## Overview
COS allows you to set object access permissions, which have a higher priority than those for buckets.

>?
> - Object access permissions take effect only when the access is made via the default endpoint. For any access made via a CDN acceleration endpoint or a custom endpoint, bucket access permissions will take effect.
> - There are limits on the number of ACL rules. For more information, please see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).
> 

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List** to go to the bucket list page.
3. Locate the bucket where the object resides and click the bucket name to go to the bucket management page.
4. In the left sidebar, choose **File List** to go to the file list page.
5. Locate the object for which you want to configure the access permission, and click **Details** on the right to go to the file details page (If it is a folder, click **Permissions** on the right).
![](https://main.qcloudimg.com/raw/f2f66b873867b3645fa69ec4f9ffe646.png)
6. In the **Object ACL(Access Control List)** area, configure access permissions as needed.
For example, you can grant object permissions to a sub-account. The sub-account ID can be viewed in the [CAM console](https://console.cloud.tencent.com/cam).
![](https://main.qcloudimg.com/raw/c9565ab1d2378ce672a301843bf3b072.png)
COS supports two types of permissions for objects:
 - **Public Permission**: includes **Inherit**, **Private Read/Write**, and **Public Read/Private Write**. For more information about public permissions, please see [Access Permission Types](https://intl.cloud.tencent.com/document/product/436/13324).
 - **User ACL**: The root account has all object permissions (full control) by default. You can also add sub-accounts and grant them permissions including read/write, read/write ACL, and even **full control**.
7. Click **Save**.
If you need to configure or modify access permissions for multiple objects at a time, you can select the objects on the **File List** page and then click **Modify Access Permission** from the **More Actions** drop-down list at the top.
![](https://main.qcloudimg.com/raw/a00d8522c2698c39aa4687463bcb05e4.png)
