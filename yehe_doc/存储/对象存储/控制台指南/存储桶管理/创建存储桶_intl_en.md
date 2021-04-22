### Introduction
You can create buckets on the Bucket List page on the COS Console. For more information on buckets, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).

>! Up to 200 buckets are allowed under the same user account (regardless of region).

### Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List** to enter the bucket list page, and then click **Create Bucket**.
![](https://main.qcloudimg.com/raw/2a0f325c6ee63a337a049669ccaa8800.png)
3. In the pop-up Create Bucket dialog box, configure the following information:
 - **Name**: Enter a custom bucket name; this cannot be modified once configured. For naming instructions, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312).
 - **Region**: Select the COS region corresponding to the physical zone where your business (or number of users) is concentrated. This cannot be modified once configured. For more information on regions, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
 - **Access Permissions**: Three access permissions are available for buckets by default: "Private Read/Write", "Public Read/Private Write" and "Public Read/Write". This can be modified after configured. For more information, see [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).
 - **Bucket Tag**: A bucket tag is used as an identifier to manage buckets. For more information, see [Setting Bucket Tags](https://intl.cloud.tencent.com/document/product/436/30928).
 - **Server-Side Encryption**: Currently, the only supported bucket encryption method is SSE-COS encryption (i.e., server encryption using COS-managed keys). For more information on server encryption, see [Server Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
![](https://main.qcloudimg.com/raw/0fbdeff59404678e08cf6542692f53d1.png)
4. Verify that all the information entered is correct, and then click **OK** to create the bucket. You will then be able to view the newly created bucket on the Bucket List page.
![](https://main.qcloudimg.com/raw/5dc9b23efc7adf0a3e206306c66a2030.png)
