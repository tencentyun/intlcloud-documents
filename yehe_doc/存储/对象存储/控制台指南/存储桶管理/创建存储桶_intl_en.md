## Overview
This document describes how to create a bucket on the **Bucket List** page in the COS console. For more information on buckets, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).

>! Each account can create up to 200 buckets regardless of the region.
>

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click **Create Bucket**.
4. In the pop-up window, configure the following information:
 1. Basic information
![](https://qcloudimg.tencent-cloud.cn/raw/3cd1360bc4c2fe796ee2f2d97975727d.png)
	 - **Region**: Select a COS region corresponding to the physical location where your business or users are distributed. This parameter cannot be modified once configured. For more information on regions, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
	 - **Name**: Enter a custom bucket name, which cannot be modified once configured. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83).
	 - **Access Permission**: A bucket provides three types of access permissions by default, i.e., **Private Read/Write**, **Public Read/Private Write**, and **Public Read/Write**. The configured permission can be modified later. For more information, see [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).
	 - **Domain Name**: This value is generated automatically. After creating a bucket, you can use this domain name to access the bucket.
 2. Advanced settings
>? Advanced settings are optional and can be set as needed.
>
![](https://qcloudimg.tencent-cloud.cn/raw/f8acbd14ecadbbdf0445f567f5853898.png)
    - **Versioning**: If this feature is enabled, and you upload an object with the same name as an existing object, the historical version will be retained.
	- **Logging**: Logging helps you log all kinds of requests for bucket operations.
  	- **Bucket Tag**: A tag is used as an identifier to manage buckets. For more information, see [Setting Bucket Tags](https://intl.cloud.tencent.com/document/product/436/30928).
  	- **Server-Side Encryption**: Currently, the supported bucket encryption method is SSE-COS encryption (i.e., server-side encryption using COS-managed encryption keys). For more information on server-side encryption, see [Server-Side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
 3. Configuration confirmation
![](https://qcloudimg.tencent-cloud.cn/raw/20e65888c7a948dfe5ce67402df5167b.png)
Confirm the bucket configurations. If you need to change anything, click **Previous** and modify as needed.
5. Confirm the information and click **Create** to create the bucket. Then, you can view the created bucket on the **Bucket List** page.
![](https://qcloudimg.tencent-cloud.cn/raw/7d7f83ffab77e7892d7d2dd8f5ca633d.png)

