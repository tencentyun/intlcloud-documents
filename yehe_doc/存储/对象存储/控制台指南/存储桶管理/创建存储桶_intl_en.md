## Overview
You can create a bucket on the **Bucket List** page in the COS console. For more information about buckets, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).

>! Each account can create up to 200 buckets regardless of the region.
>

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List** to enter the bucket list page, and then click **Create Bucket**.
3. In the pop-up window, configure the following information:
 1. Basic information
![](https://qcloudimg.tencent-cloud.cn/raw/3cd1360bc4c2fe796ee2f2d97975727d.png)
- **Region**: a COS region corresponding to the physical location where your business or users are distributed. This parameter cannot be modified once configured. For more information about regions, please see [Regions and Access Endpoints](https://cloud.tencent.com/document/product/436/6224).
- **Name**: a custom bucket name, which cannot be modified once configured. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83).
- **Access Permissions**: Three access permissions are available for buckets by default: "Private Read/Write", "Public Read/Private Write", and "Public Read/Write". You can modify it if needed. For more information, please see [Setting Access Permission](https://cloud.tencent.com/document/product/436/13315).
- **Domain Name**: The value is generated automatically. After creating a bucket, you can use this domain name to access the bucket.
 2. Advanced settings
>? Advanced settings are optional and can be set as needed.

![](https://qcloudimg.tencent-cloud.cn/raw/f8acbd14ecadbbdf0445f567f5853898.png)

- **Versioning**: If this field is enabled, and you upload an object whose name already exists, the historical version will be retained.
- **Logging**: stores logs of bucket-related requests.
- **Bucket Tag**: A tag is used as an identifier to manage buckets. For more information, please see [Setting Bucket Tags](https://intl.cloud.tencent.com/document/product/436/30928).
- **Server-Side Encryption**: Currently, the only supported bucket encryption method is SSE-COS encryption (i.e., server encryption using COS-managed keys). For more information on server encryption, see [Server Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

 3. Configuration confirmation
![](https://qcloudimg.tencent-cloud.cn/raw/20e65888c7a948dfe5ce67402df5167b.png)
Confirm the bucket configurations. If there is anything you need to modify, click **Previous** and modify as needed.
4. Verify the information entered and then click **OK** to create the bucket. You will then be able to view the created bucket on the **Bucket List** page.
![](https://qcloudimg.tencent-cloud.cn/raw/7d7f83ffab77e7892d7d2dd8f5ca633d.png)

