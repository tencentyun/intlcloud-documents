## Introduction
COS allows you to set access permissions for objects, and this setting has a higher priority than that for buckets.
The object access permission is valid only when an access attempt is made to the default domain name. For any access attempt made to a CDN-accelerated or custom domain name, the bucket access permission will prevail.

By setting object access permission, you can, for example, set the specific objects which allow public access in a "private read/write" bucket or set the specific objects which only allow access after authentication in a "public read/write" bucket. Object permissions include the following types:
- Inherited bucket permission: The object has the same access permission as the bucket. When you access an object with the "inherited bucket permission", COS will match the bucket permission to respond to the access. A new object inherits the permission from its bucket by default.
- Public read/private write: When you access an object with the public read permission, the object can be directly downloaded, regardless of the bucket permission.
- Private read/write: When you access an object with the private read/write permission, the object can only be accessed after [signature authentication](https://cloud.tencent.com/document/product/436/6054), regardless of the bucket permission.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos4/index) and select **Bucket List** on the left sidebar to enter the bucket list page. Click the bucket of the object for which you want to modify access permission (such as example) to enter the bucket.
2. Locate the object for which you want to set permission (such as example.exe), click **More** > **Set Permission** on its right, and the **Set Permission** dialog box will pop up.
![Set object permission 1](https://main.qcloudimg.com/raw/a295c398bffe042cb320fd7fb12ce879.png)
3. Modify the access permission and click **OK** to save the changes.
![Set object permission 2](https://main.qcloudimg.com/raw/09b25c4e5ebf683415971e79d558dc02.png)
