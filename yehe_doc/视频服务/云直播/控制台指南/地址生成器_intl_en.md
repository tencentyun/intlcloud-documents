This document describes how to store screenshots or porn detection data in a COS bucket. You need to create a COS bucket, authorize CSS to store data in it, and then configure live screencapture and porn detection settings in the CSS console. After that, screenshots and porn detection data can be stored in the bucket. This feature is available in the new console.

### Creating a COS Bucket
1. Log in to the COS console, and then click [Bucket List](https://console.cloud.tencent.com/cos5/bucket).
2. Click **Create Bucket**, configure settings in the pop-up, and then click **OK**.
![](https://main.qcloudimg.com/raw/422f9ca892a0a9a46cc411712fbb1c06.png)
>!
>- The bucket name above is `test` (excluding `-125****577`).  
>- You can configure above settings based on your needs.
3. You can enable CDN acceleration for the COS bucket. Click a bucket name in the list or click **Configure**, select **Domains and Transfer** > **Default CDN Acceleration Domain** on the left sidebar, click **Edit**, then toggle **Status** on and configure settings below. After the configuration, click **Save** to enable CDN acceleration. For detailed directions, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).
![](https://main.qcloudimg.com/raw/96538f69d6de9e987f206aa8b26bfa5d.png)

 

### Authorizing CSS to Store Screenshots

1. Grant write permission for storing screenshots to the root account (ID: `-125****577`).
   1. Select an authorized bucket in the **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)**, and click **Configure** to go to the bucket configuration page. Click **Permission Management** > **[Bucket ACL(Access Control List)](https://console.cloud.tencent.com/cos5/bucket/setting?type=aclconfig&anchorType=accessPermission&bucketName=text-1258968577&projectId=&path=%252F®ion=ap-guangzhou)**. Click **Add User**, select **Root account** as the user type, <b>enter the root account ID `-125****577`</b>, and then click **Save**.
![](https://main.qcloudimg.com/raw/76b93786e2d54c9166fcf0ed63b12d97.png)
![](https://main.qcloudimg.com/raw/b00fcba492552d1a7105132d1f69e714.png)
Alternatively, you can click **Manage Permissions** on the **Bucket List** page, and select the buckets to authorize. Toggle **Public Permissions** and **User ACL** on, and then add a user. Select **Root account** as the user type, <b>enter the root account ID `-125****577`</b>, and then click **Save**.
![](https://main.qcloudimg.com/raw/b00fcba492552d1a7105132d1f69e714.png)
![](https://main.qcloudimg.com/raw/75667a8ec647a60700ce6ff5557c0f46.png)
>! <b>Enter the root account ID `125****577` to authorize. This ID is also the `APPID` of CSS.</b>

   1. For more information on the API to set the bucket access permission, please see [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737).
2. Get the information of the authorized COS bucket.
   3. You can go to the **[Overview](https://console.cloud.tencent.com/cos5/bucket/setting?type=bucketoverview&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)** page of a COS bucket to view its information. **Endpoint** on this page contains bucket name, COS `APPID`, and bucket region.
![](https://main.qcloudimg.com/raw/d533e4b8c386454085d1e8604503d892.png)
    - Bucket name：`test`
    - COS APPID：`125****577`
    - Bucket region：`ap-nanjing`

   4. After you configure the above 3 fields, the system will store CSS screenshots in the authorized COS bucket.
