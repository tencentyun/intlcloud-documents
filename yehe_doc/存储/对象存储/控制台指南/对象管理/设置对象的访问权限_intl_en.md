## Overview
COS allows you to configure access permissions for objects, which have a higher priority than that for buckets.

>
>-The object access permission is valid only when the user accesses via the default domain name. When the access is made via a CDN accelerated domain name or custom domain name, the bucket access permission takes priority.
>-For more information, see [Specifications and Limits](https://cloud.tencent.com/document/product/436/14518).

## Steps




1. Log into the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Find the bucket for which you need to configure object access permissions, click its bucket name to enter the details page.
![](https://main.qcloudimg.com/raw/156823c7ad23708feb85f5d682c61d50.png)
3. In [File List], find the object whose permission needs to be configured, and click [Details] on the right to enter the file details page (If it is a folder, click [Permissions] on the right).
![](https://main.qcloudimg.com/raw/6065855393a30c809d60b4d0027628a6.png)
4. Click the [Object Permissions] configuration item above, and configure access permissions based on actual needs (such as granting sub-account object permissions, sub-account ID can be found in [Cloud Access Management](https://console.cloud.tencent.com/cam) Console). COS supports two types of permissions for objects:
 -**Public Permissions**: Inherited permission, private read/write, and public read/private write. For more information on public permissions, see [Access Permission Types](https://intl.cloud.tencent.com/document/product/436/13324).
 -**User Permissions**: The root account has all object permissions (full access) by default. In addition, COS allows you to grant sub-accounts data read/write, permission read/write, and even **full access** permissions.
![](https://main.qcloudimg.com/raw/c9565ab1d2378ce672a301843bf3b072.png)
5. Click [Save] to configure the object access permissions.
6. If you need to configure or modify access permissions for multiple objects in batches, you can check multiple objects and select [Modify Access Permissions] under [More Actions].

