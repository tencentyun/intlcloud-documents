## Overview
You can use the lifecycle management feature when you need to change the types of storage or delete specified objects regularly to reduce costs. COS will automatically change the storage class of or delete specified objects at the specified time according to the rule you set. For more information, see [Lifecycle Overview](https://cloud.tencent.com/document/product/436/17028).

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List**, and click the bucket you want to configure to enter the bucket detail page.
![](https://main.qcloudimg.com/raw/94520df563736af8c38de12cda21912f.png)
2. Click **Basic Configuration** on the top to enter the Basic Configuration page of the bucket, scroll down to find **Lifecycle** and then click **Add Rule**.
![](https://main.qcloudimg.com/raw/1185903895d32b0534c3d33ae515c064.png)
3. Edit the lifecycle rule as needed.
![](https://main.qcloudimg.com/raw/254a576562691687102ef66c8ab902f0.png)

4. Rule Name: You can set a name for your lifecycle rule for easy management.

 - **Scope**: This lifecycle rule can be applied to the entire bucket or objects with a specific prefix under the bucket, such as `doc/`. If you select "Specified prefix", you need to enter a prefix. For more information about object keys, see [Notes](https://cloud.tencent.com/document/product/436/13324#.E7.9B.B8.E5.85.B3.E8.AF.B4.E6.98.8E). For more information about lifecycle configuration rules, see [Rule Description](https://cloud.tencent.com/document/product/436/17029#.E8.A7.84.E5.88.99.E6.8F.8F.E8.BF.B0).

 - **Manage Files**: You can set the number of days after which storage type of files in the bucket shall be changed or files shall be deleted. Storage types are COS Standard, COS Infrequent Access, and Archive Storage, ranking from hot to cold storage. Storage types can only be changed from hot to cold.  Calculation of days is based on files’ modification time in the COS.

 - **Delete Fragments**: Files can be uploaded partially due to various reasons. You can set to delete such incomplete files periodically.

5. After configuring the lifecycle rule, click **OK**. When you need to disable a lifecycle rule, change the status of corresponding rule to **Disable**.
![](https://main.qcloudimg.com/raw/ad284f4bb9d82ae603a4e764f978532e.png)

