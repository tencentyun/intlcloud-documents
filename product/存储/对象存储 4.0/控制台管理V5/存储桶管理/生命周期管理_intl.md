## Overview
You can use the lifecycle management feature when you need to change the types of storage or delete specified objects regularly to reduce costs. COS will automatically change the storage class of or delete specified objects at the specified time according to the rule you set. 

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List**, and click the bucket you want to configure to enter the bucket detail page.
![](https://main.qcloudimg.com/raw/695c2f7e68ef417a9f1a0809fcd804fc.png)
2. Click **Basic Configuration** on the top to enter the Basic Configuration page of the bucket, scroll down to find **Lifecycle** and then click **Add Rule**.
![](https://main.qcloudimg.com/raw/3610ab8aaa27d8541d46cca70546388d.png)
3. Edit the lifecycle rule as needed.
![](https://main.qcloudimg.com/raw/ee7d6f5683018d39605ac4bbc471eab2.png)

4. Rule Name: You can set a name for your lifecycle rule for easy management.

 - **Scope**: This lifecycle rule can be applied to the entire bucket or objects with a specific prefix under the bucket, such as `doc/`. If you select "Specified prefix", you need to enter a prefix.
 - **Manage Files**: You can set the number of days after which storage type of files in the bucket shall be changed or files shall be deleted. Storage types are COS Standard, COS Infrequent Access, and Archive Storage, ranking from hot to cold storage. Storage types can only be changed from hot to cold.  Calculation of days is based on files’ modification time in the COS.

 - **Delete Fragments**: Files can be uploaded partially due to various reasons. You can set to delete such incomplete files periodically.

5. After configuring the lifecycle rule, click **OK**. When you need to disable a lifecycle rule, change the status of corresponding rule to **Disable**.
![](https://main.qcloudimg.com/raw/8aa8f810d2afb1c6dd680bde1fc681d7.png)

