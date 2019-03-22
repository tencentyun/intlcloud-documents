## Overview
COS allows you to set access permission for objects, and this permission has a higher priority than that for buckets.
The object access permission is valid only when the access attempt is made via the default domain name. For any access attempt made via a CDN accelerated domain name or custom domain name, the bucket access permission has the first priority.

### Scenarios
You can set the specified object which allow public access in a private read/write bucket, or the specified objects which only allow access after authentication in a public read/write bucket.
### Type of access
- Inherit Permission: Bucket permission inherited by an object is consistent with bucket access permission. When accessing an object with an access permission of "Inherit Bucket Access Permission", COS matches the bucket access permission to respond to the access. A new object inherits access permission from its bucket by default.
- Public Read/Private Write: When an object with an access permission of "Public Read" is accessed, the object can be directly downloaded, regardless of the bucket access permission.
- Private Read/Write : When an object with an access permission of "Private Read/Write" is accessed, the object can only be accessed after [Request signature](https://intl.cloud.tencent.com/document/product/436/7778), regardless of the bucket access permission.
- Public Read/Write: Anyone (including anonymous visitors) has read and write permissions to the objects in the bucket. This is not recommended.

## Procedure
1. Log in to the [COS Console](https://intl.cloud.tencent.com/login), and then select the left pane **Bucket List** to go to the Bucket List page. Click the bucket of the object for which you want to modify access permission to enter the bucket.
![](https://main.qcloudimg.com/raw/e4f21abdfd08af484c1f4091b0d497e2.png)
2. Locate the object for which you want to set permission (such as example.exe), then click **Details** on the right of the object, and you can set permission on its details page. In case of a folder, directly set the permission by clicking **Set Permission** on the right.
![](https://main.qcloudimg.com/raw/dc2da2c85615da9433e141826221ff52.png)
3. Modify the permission, and then click **Save**.
![](https://main.qcloudimg.com/raw/09b25c4e5ebf683415971e79d558dc02.png)

