## Overview

You can enable inventory for your bucket in the [COS console](https://console.cloud.tencent.com/cos5). The inventory feature allows you to regularly (daily/weekly) publish inventory reports about the object attributes, configurations, and more. For more information about inventory, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622). The following describes how to enable the inventory feature for a bucket.

> !
>- You can configure multiple inventory jobs for a single bucket.
>- Inventory jobs do not directly read the object content during execution. Instead, they only scan the attribute information such as the object metadata.
>- Currently, the inventory feature is not available for Finance Cloud regions.

## Prerequisites

You have created a bucket. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List** and then click the desired bucket (source bucket) for which you want to enable inventory.
3. Choose the **Basic Configurations** tab and then click **Inventory** > **Add Inventory**.
   ![](https://main.qcloudimg.com/raw/73aa7b3f19389dfdd42d4066e6437329.png)
4. On the **Add Inventory** page, configure the following parameters:
  - **Inventory Name**: name of the published inventory report
  - **Destination Bucket**: bucket where the inventory is stored. Defaults to the source bucket. The destination bucket must be in the same region as the source bucket.
 - **Report Prefix (Optional)**: prefix selected for the destination bucket. The prefix can be used to group the inventory files in a public location. The default value is used initially.
 - **Status**: enables/disables the inventory feature.
 - **Advanced Settings**: advanced configurations for inventory. If not set, the default values will be used.
   - **Output Format**: The default value is **CSV**.
   - **Object Version**: whether to include all object versions or only the current version in the inventory. If not set, only the current version will be included.
   - **Generate Lifecycle**: specifies whether to export the inventory **Everyday** (default) or **Everyweek**. For example, an inventory added at 15:00 today will be generated and delivered to the destination bucket before 6:00 tomorrow in most cases.
   - **Filter Prefix (Optional)**: filters only objects with the specified prefix in the inventory. If not set, no prefix filter will be applied.
   - **Filter Time (Optional)**: filters only objects modified after the specified time or within the specified period in the inventory. If not set, no time filter will be applied.
   - **Inventory Encryption**: whether to encrypt the inventory on the server. Options include:
     - None: The inventory is not encrypted (default).
     - SSE-COS: Encrypt the inventory report using server-side encryption with COS-managed key. For more information, please see [SSE-COS Encryption](https://intl.cloud.tencent.com/document/product/436/18145) in the COS Developer Guide.
   - **Inventory Information**: object information to be included in the inventory report. Options include object size, storage class, ETag, cross-bucket replication status, multipart upload status, and last updated time. If not specified, all will be selected.
     ![](https://main.qcloudimg.com/raw/a219e0eb29661c254f0a70f094cf1ae0.png)

> !`ETag` (entity tag) is the hash value of the object. It only reflects changes in the object content but not the object metadata. The value of `ETag` is not necessarily the MD5 checksum of the object. The value can be different if the uploaded object is encrypted.

5. Click **Save**. In this way, COS will publish inventory reports and deliver them to the destination bucket you set daily or weekly.
>?For more information about the format and content of the generated inventory reports, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).
