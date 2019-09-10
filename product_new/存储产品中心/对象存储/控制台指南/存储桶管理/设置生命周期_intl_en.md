## Overview
You can use the lifecycle management feature when you need to change the storage class or delete specified objects regularly to reduce costs. COS will automatically change the storage class or delete specified objects within the specified time frame according to the rules you set. For more information, see [Lifecycle Overview](https://cloud.tencent.com/document/product/436/17028).

>A lifecycle can be set to a maximum of 3,650 days.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List** to enter the bucket list page.
3. Locate the bucket for which you want to enable the lifecycle feature. Click the bucket name to enter its details page.
![](https://main.qcloudimg.com/raw/695c2f7e68ef417a9f1a0809fcd804fc.png)
4. Click **Basic Configuration** on the top, scroll down to **Lifecycle** and then click **Add Rules**.
![](https://main.qcloudimg.com/raw/3610ab8aaa27d8541d46cca70546388d.png)
5. Add lifecycle rules as needed. The configuration items are described as follows:
 - **Rule Name**: Enter a name for the lifecycle rule.
 - **Applied to**: This lifecycle rule can be applied to the entire bucket or objects with a specific prefix in the bucket, such as examplevault. If you select **Specified Prefix**, you need to enter a prefix.
 - **Prefix**: For more information on object keys (or prefixes), see [Object Overview](https://cloud.tencent.com/document/product/436/13324#.E7.9B.B8.E5.85.B3.E8.AF.B4.E6.98.8E). For more information on the configuration rules for the lifecycle, see [Rule Description](https://cloud.tencent.com/document/product/436/17029#.E8.A7.84.E5.88.99.E6.8F.8F.E8.BF.B0).
 - **Manage current version**: You can transition or delete objects in the current version by enabling **Manage current version**. You can transition the objects in a bucket from COS Standard to COS Infrequency Access or Archive Storage, and delete the objects upon their expiration.
 Storage classes include **COS Standard** > **COS Infrequent Access** > **Archive Storage** (from hot storage to cold storage). Storage classes can only be changed from hot to cold. Calculation of days is based on the modification time of files in COS.
 - **Manage previous versions**: You can transition or delete objects of previous versions by enabling **Manage historical versions**. If it is not enabled, only objects of the latest version are processed by default.
 - **Clean up expired object delete markers**: If you delete certain version of an object, all previous ones of this version will expire, and the delete markers for the expired objects are retained. Although delete markers do not incur storage costs, removal of them can improve the performance of `LIST` operations.
  - **Delete incomplete multipart uploads**: If some parts of the files fail to be uploaded due to some reasons, you can use this feature to delete the parts associated with these multipart uploads periodically.
![](https://main.qcloudimg.com/raw/ee7d6f5683018d39605ac4bbc471eab2.png)
6. After the lifecycle rules are configured, click **OK** and you will see the lifecycle rules.
![](https://main.qcloudimg.com/raw/0f3e245ff4626a65afa5c43984b17226.png)
7. When you want to disable a lifecycle rule, click **Edit** to change the status of the rule to **Disable** or delete the lifecycle rule.
![](https://main.qcloudimg.com/raw/6034fc8c38a95c077b78628748ed2248.png)
