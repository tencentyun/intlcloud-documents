## Overview
COS allows you to set access permission for objects, and this permission has a higher priority than that for buckets.
The object access permission is valid only when the access attempt is made via the default domain name. For any access attempt made via a CDN accelerated domain name or custom domain name, the bucket access permission has the first priority.

### Scenarios
You can set the specified object which allow public access in a private read/write bucket, or the specified objects which only allow access after authentication in a public read/write bucket.
### Type of access
- Inherit Permission: Bucket permission inherited by an object is consistent with bucket access permission. When accessing an object with an access permission of "Inherit Bucket Access Permission", COS matches the bucket access permission to respond to the access. A new object inherits access permission from its bucket by default.
- Public Read/Private Write: When an object with an access permission of "Public Read" is accessed, the object can be directly downloaded, regardless of the bucket access permission.
- Private Read/Write : When an object with an access permission of "Private Read/Write" is accessed, the object can only be accessed after [signature authentication](/document/product/436/6054), regardless of the bucket access permission.
- Public Read/Write: Anyone (including anonymous visitors) has read and write permissions to the objects in the bucket. This is not recommended.

## Procedure
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), and then select the left pane **Bucket List** to go to the Bucket List page. Click the bucket of the object for which you want to modify access permission to enter the bucket.
![](//mc.qcloudimg.com/static/img/d156619ab35a0e1195a70d0e8d8954ca/image.png)
2. Locate the object for which you want to set permission (such as example.exe), then click **Details** on the right of the object, and you can set permission on its details page. In case of a folder, directly set the permission by clicking **Set Permission** on the right.
![](//mc.qcloudimg.com/static/img/f9fe9cdf0d3535cc4bc93547ab7bd84c/image.png)
3. Modify the permission, and then click **Save**.
![](//mc.qcloudimg.com/static/img/ed7e026b114a6d43741e7fd8ffe4bba5/image.png)

