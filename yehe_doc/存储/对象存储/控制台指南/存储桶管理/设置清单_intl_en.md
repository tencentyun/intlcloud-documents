## Overview

You can enable inventory for your bucket in the [COS console](https://console.cloud.tencent.com/cos5). The inventory feature allows you to regularly (daily/weekly) publish inventory reports about the object attributes, configurations, and more. For more information about inventory, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622). The following describes how to enable the inventory feature for a bucket. COS allows you to generate inventories on schedule or on the fly as needed.

>!
> - You can configure multiple inventory jobs for a single bucket.
> - Inventory jobs do not directly read the object content during execution. Instead, they only scan the attribute information such as the object metadata.
> 

## Prerequisites

You have created a bucket. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions

### Adding a scheduled inventory

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**.
3. Click the name of the source bucket that you want to enable inventory for.
4. Click **Basic Configurations** > **Inventory**, and then click **Add Inventory**.
![](https://qcloudimg.tencent-cloud.cn/raw/9b8a2b1fc77bc2474f57e10dc5fffd7f.png)

5. On the **Add Inventory** page, configure the following parameters:
 1. Basic information
 
![](https://qcloudimg.tencent-cloud.cn/raw/9cdbf46cd2fc322b14dafb6a5cb9b4b2.png)

   - **Rule Status**: whether to enable this inventory rule. Valid values: **Enable**, **Disable**.
   - **Inventory Name**: name of the published inventory report
   - **Destination Bucket**: bucket where the inventory is stored. Defaults to the source bucket. The destination bucket must be in the same region as the source bucket.
   - **Report Prefix (Optional)**: prefix selected for the destination bucket. The prefix can be used to group the inventory files in a public location. The default value is used initially.
 2. Filter
![](https://qcloudimg.tencent-cloud.cn/raw/a8138f193f22bd28c824988e4d2d40ab.png)

    - **Scope of the file**: object scope to apply the inventory rule. **The whole bucket** is selected by default.
    - **Object Version**: whether to include all object versions or only the current version in the inventory. If not set, only the current version will be included.
    - **Filter Labels** (optional): lists objects with the same tag to the inventory. If this field is not set, no tag will be filtered.
    - **Filter Time (Optional)**: filters only objects modified after the specified time or within the specified period in the inventory. If not set, no time filter will be applied.
    - **Inventory Information**: object information to be included in the inventory report. Options include object size, storage class, ETag, cross-bucket replication status, multipart upload status, last updated time, and tag. If not specified, all will be selected.
>! `ETag` (entity tag) is the hash value of the object. It only reflects changes in the object content but not the object metadata. The value of `ETag` is not necessarily the MD5 checksum of the object. The value can be different if the uploaded object is encrypted.
>
 3. Output format
![](https://qcloudimg.tencent-cloud.cn/raw/b48c91e6bd090d500c7e34cd8eef92eb.png)

	- **Output Format**: The default value is **CSV**.
	- **Generate Lifecycle**: specifies whether to export the inventory **Everyday** (default) or **Everyweek**. For example, an inventory added at 15:00 today will be generated and delivered to the destination bucket before 6:00 tomorrow in most cases.
	- **Inventory Encryption**: whether to encrypt the inventory on the server. Options include:
		 - None: The inventory is not encrypted (default).
		 - SSE-COS: Encrypt the inventory report using server-side encryption with COS-managed key. For more information, please see [SSE-COS Encryption](https://intl.cloud.tencent.com/document/product/436/18145) in the COS Developer Guide.
	- **Access authorization**: This field needs to be enabled to proceed with the next step. By default, this field is disabled.
 4. Information confirmation
![](https://qcloudimg.tencent-cloud.cn/raw/f6fe780a4524fe149c258f2c6f17adaf.png)

Confirm the inventory configurations for the bucket. If there is anything you need to modify, click **Previous** and modify as needed.
5. Click **OK**. In this way, COS will publish inventory reports and deliver them to the destination bucket you set daily or weekly.
>? For more information about the format and content of the generated inventory reports, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).
>

### Generating an instant on the fly

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List** and then click the desired bucket (source bucket) for which you want to enable inventory.
3. Click **Basic Configurations** > **Inventory**. Click **Generate list on the fly** in the **Operation** column on the right of the desired inventory rule.
![](https://qcloudimg.tencent-cloud.cn/raw/56d01e3e37a28fa41f0e7a6349a9b438.png)
>? To generate an inventory on the fly, click **Generate list on the fly** in the **Operation** column.
> If you haven’t configured inventory, you can configure one and then generate an inventory on the fly.
