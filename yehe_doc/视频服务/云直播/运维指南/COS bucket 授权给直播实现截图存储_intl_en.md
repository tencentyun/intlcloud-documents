This document describes how to store screenshots or porn detection data in a COS bucket. You need to create a COS bucket, authorize CSS to store data in it, and then configure live screencapture and porn detection settings in the CSS console. After that, screenshots and porn detection data can be stored in the bucket. This feature is available in the new console.

### Creating a COS Bucket
1. Log in to the COS console and click [**Bucket List**](https://console.cloud.tencent.com/cos5/bucket).
2. Click **Create Bucket**. In the pop-up window, enter the basic information, select a permission for the bucket, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/a447693216193809de86e422149f5a25.png)
3. Complete the advanced settings (optional) and click **Next**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/29fe705f2b98c29bc7ae913e39fc99d0.png)
4. Confirm the configuration information and click **Create**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/fb2c3a34e7502234600b93cfff7900b6.png)
>!
>- In the example above, the bucket name is `test` (`-130****592` is not part of the name).  
>- Complete the above settings based on your needs.
5. To enable CDN acceleration, click the name of your bucket or **Configure** in the bucket list, select **Domains and Transfer** > **Default CDN Acceleration Domain** on the left sidebar, click **Edit**, toggle on **Status**, and compete the settings. For detailed directions, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505). After the configuration, click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/dc7a8ff49c0832d2322d03a0714d2f76.png)

 

### Authorizing CSS to store screenshots in COS

1. Grant the CSS root account (ID: `3508645126`) write access to the COS bucket.

  1. In the **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)**, find the bucket you created, and click **Configure**. On the bucket configuration page, select **Permission Management** > **[Bucket ACL(Access Control List)](https://console.cloud.tencent.com/cos5/bucket/setting?type=aclconfig&anchorType=accessPermission&bucketName=text-1258968577&projectId=&path=%2F®ion=ap-guangzhou)**, click **Add User**, select **Root account** as the user type, **enter the root account ID `3508645126`**, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/f31e4a9251f1c959954b958b284bfb44.png)
![](https://qcloudimg.tencent-cloud.cn/raw/8c8b4331c37cfb3f07169eb8726017df.png)
Alternatively, in the bucket list, click **Manage Permissions**, select the bucket you created, enable **Public Permission** and **User ACL**, click **Add User**, select **Root account** as the user type, **enter the root account ID `3508645126`**, click **Save** to save the configuration, and then click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/3af1130fae59890e7658d4681aadf844.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0025f6d26a3cf83f7e213c32e7f7eddf.png)
>! **`3508645126` is the `APPID` of CSS. You need to enter this ID for the authorization to succeed.**

   2. For how to use an API to set bucket access, see [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737).

2. Get the information of the COS bucket to which CSS is granted access.
   1. Click the name of the bucket you created in the bucket list and go to **[Overview](https://console.cloud.tencent.com/cos5/bucket/setting?type=bucketoverview&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)** to view its information. The endpoint contains the bucket name, COS `APPID`, and bucket region.
![](https://qcloudimg.tencent-cloud.cn/raw/2b1fa50e6551966b3a7fe946f59d6260.png)
    - Bucket name：`test`
    - COS appid：`130****592`
    - Bucket region: `eu-moscow`
   2. Provide the above information to CSS and the system will store live screenshots in the COS bucket you created.
