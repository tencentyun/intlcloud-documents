## Overview

You can use the COS console to set or modify bucket access permissions of the following two types.

- **Public permissions**: Include private read/write, public read/private write and public read/write. For more information, see **Types of Permission** under [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).

- **User ACLs**: The root account has all bucket permissions (full control) by default. You can add sub-accounts and grant them permissions including read/write, read/write ACL, and even **full control**.

>?
>- If the bucket permission is private read/write or a specified account is granted the permission, an object request needs to carry a signature for identity verification. For more information on signature, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>- If the bucket permission is public read/private write or public read/write, an object request doesn't need to carry a signature, and anonymous users can directly access the object at the URL. However, your data may be leaked. Therefore, proceed with caution.


## Granting Permissions for a Single Bucket

**Directions**

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**.
3. Locate the bucket for which you want to set or modify access permissions, and then click the bucket name.
4. Select **Permission Management** > **Bucket ACL (Access Control List)** and you can set both public permissions and user ACLs for the bucket. For example, you can add a sub-account, whose ID can be viewed in the [CAM console](https://console.cloud.tencent.com/cam).
![](https://main.qcloudimg.com/raw/34e464b33c4b9bffe72c734d1c1dcb2d.png)
5. Click **Save**.

## Granting Permissions for Multiple Buckets

**Directions**

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**.
3. Click **Manage Permissions** above the bucket list.

4. In the pop-up window, select the buckets that you want to grant permissions for. Then, scroll down to set both public permissions and user ACLs. For example, you can add a sub-account, whose ID can be viewed in the [CAM console](https://console.cloud.tencent.com/cam).
![](https://main.qcloudimg.com/raw/23eff9055312eaa122e247f9cf0ebf53.png)
5. Once completed, click **OK**.

