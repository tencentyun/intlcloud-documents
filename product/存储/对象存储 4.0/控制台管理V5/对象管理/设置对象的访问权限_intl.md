## Overview
COS allows you to set access permission for objects, and this permission has a higher priority than that for buckets. COS supports two permission types:

- Public Permissions: Inherit, Private Read/Write, Public Read/Private Write. For more information, see [Access Permission Types](https://intl.cloud.tencent.com/document/product/436/13324#access-permission-types) in the "Object Overview".
- User Permissions: The root account has all the permissions (full control) for objects by default. In addition, you can add sub-accounts that are granted permissions to read/write data and read/write permissions, and even full access to buckets.



>- The object access permission is valid only when the access attempt is made via the default domain name. For any access attempt made via a CDN accelerated domain name or custom domain name, the bucket access permission has the first priority.
>- There are quantitative restrictions on access policy rules, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518) for details

## Procedure
1. Log in to the [COS Console](https://intl.cloud.tencent.com/login), and then select the left pane **Bucket List** to go to the Bucket List page. 
2. Click the bucket of the object for which you want to modify access permission to enter the bucket.
3. Locate the object for which you want to set permission, then click **Details** on the right of the object, and you can set permission on its details page. In case of a folder, directly set the permission by clicking **Set Permission** on the right.
![](https://main.qcloudimg.com/raw/a295c398bffe042cb320fd7fb12ce879.png)
4. Modify the permission, and then click **Save**.
![](https://main.qcloudimg.com/raw/09b25c4e5ebf683415971e79d558dc02.png)

