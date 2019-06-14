## Overview

You can enable inventory for your bucket in the [COS Console](https://console.cloud.tencent.com/cos5). The inventory feature allows you to regularly output an inventory report of object attributes and configuration details for your bucket on a daily or weekly basis. For more information about inventory, see [Inventory Feature Overview](https://intl.cloud.tencent.com/document/product/436/30622). The following section will guide you through how to enable inventory for a bucket.

> - You can configure multiple inventory tasks in one bucket.
> - Such tasks do not directly read the object content during their execution; instead, they only scan the attribute information such as object metadata.

## Steps

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List** and then click the bucket (source bucket) for which you want to enable inventory.
![](https://main.qcloudimg.com/raw/9531d534a55a9f9665c52bdc384c7ba1.png)
3. Click the **Basic Configuration** tab, find the **Inventory Settings** item, and click **Add an Inventory**.
![](https://main.qcloudimg.com/raw/f38999a30e04fb3da8c765517fd42668.png)
4. On the **Add an Inventory** page, you can configure the following items:
![](https://main.qcloudimg.com/raw/6669721856e7a2d7ae6e0477b5c739c9.png)
 - **Inventory Name**: Name the output inventory report.
 - **Destination Prefix (Optional)**: Enter the prefix selected for the destination bucket, which can group the inventory files in a public location. The default value is used initially.
 - **Destination Bucket **: This is the bucket where the inventory is stored. The default value is the source bucket. The destination bucket must be in the same region as the source bucket.
 - ** Status**: You can choose to enable or disable the inventory.
 - **Advanced Settings**: You can configure more inventory information in the advanced settings. If you leave them alone, all the default settings will be used:
   - **Output Format**: The default value is CSV format.
   - **Object Version**: Select whether to include all object versions or only the current version in the inventory. If you do not make a selection, only the current version is included by default.
   - **Generation Cycle**: Select whether to export the inventory daily or weekly. If you do not make a selection, the report is exported daily by default.
   - **Filter**: Add a prefix to the filter to only inventory the objects whose names begin with the same string. If you do not enter a prefix, no filter is used by default.
   - **Inventory Encryption**: Select whether to encrypt the inventory on the server. Options include:
     - No encryption: The inventory is not encrypted. This is the default value.
     - SSE-COS: Encrypt the report using server-side encryption with COS-managed key. For more information, see [SSE-COS Encryption](https://intl.cloud.tencent.com/document/product/436/18145) in the COS Developer Guide.
   - **Inventory Information**: Select the object information to be included in the inventory report. Options include object size, storage class, ETag, cross-region replication status, multipart upload status, and last modified date. If you do not make a selection, all items are selected by default.
> An entity tag (ETag) is a hash of the object. It only reflects changes to the object's content but not the object's metadata. It may or may not be an MD5 digest of the object data. This depends on how the object was created and encrypted.
5. After confirming that the configuration information is correct, click **Save**.
