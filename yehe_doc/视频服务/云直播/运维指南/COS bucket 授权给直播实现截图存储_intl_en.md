This document describes how to store screenshots or porn detection data in a COS bucket. You need to create a COS bucket, authorize CSS to store data in it, and then configure live screencapture and porn detection settings in the CSS console. After that, screenshots and porn detection data can be stored in the bucket. This feature is available in the new console.

### Creating a COS Bucket
1. Log in to the COS console and click **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)**.
2. Click **Create Bucket**, enter the basic information and access permission settings in the pop-up window, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/a447693216193809de86e422149f5a25.png)
3. Select optional advanced configuration items as needed and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/29fe705f2b98c29bc7ae913e39fc99d0.png)
4. Confirm the configuration information and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/fb2c3a34e7502234600b93cfff7900b6.png)

>!
>- The bucket name above is `test` (excluding `-130****592`).  
>- You can configure above settings based on your needs.

5. You can enable CDN acceleration for the COS bucket. Click a bucket name in the list or click **Configure**, select **Domains and Transfer** > **Default CDN Acceleration Domain** on the left sidebar, click **Edit**, then toggle **Status** on and configure settings below. After the configuration, click **Save** to enable CDN acceleration. For detailed directions, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).
![](https://qcloudimg.tencent-cloud.cn/raw/dc7a8ff49c0832d2322d03a0714d2f76.png)


### Authorizing CSS to Store Screenshots

1. Grant write permission for storing screenshots to the root account (ID: `3508645126`).
   1. Select an authorized bucket in the **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)**, and click **Configure** to go to the bucket configuration page. Click **Permission Management** > **[Bucket ACL (Access Control List)](https://console.cloud.tencent.com/cos5/bucket/setting?type=aclconfig&anchorType=accessPermission&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)**. Click **Add User**, select **Root account** as the user type, **enter the root account ID `3508645126`**, and then click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/8c8b4331c37cfb3f07169eb8726017df.png)

Alternatively, click **Authorization Management** to enter the authorization management page, select the bucket to be authorized, enable **Public Permissions** and **User ACL**, and add users. Select the root account as the user type, **enter the root account ID `3508645126`**, and click **Save** and **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/0025f6d26a3cf83f7e213c32e7f7eddf.png)

>! **Enter the root account ID `3508645126` to authorize. This ID is also the `APPID` of CSS.**

   2. For more information on the API to set the bucket access permission, please see [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737).
2. Get the information of the authorized COS bucket.
   1. You can go to the **[Overview](https://console.cloud.tencent.com/cos5/bucket/setting?type=bucketoverview&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)** page of a COS bucket to view its information. **Endpoint** on this page contains bucket name, COS `APPID`, and bucket region.
![](https://qcloudimg.tencent-cloud.cn/raw/2b1fa50e6551966b3a7fe946f59d6260.png)
    - Bucket name: `test`
    - COS APPID: `130****592`
    - Bucket region: `eu-moscow`
   2. After you configure the above three fields, the system will store CSS screenshots in the authorized COS bucket.
