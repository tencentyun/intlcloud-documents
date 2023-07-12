## Overview

You can enable inventory for your bucket in the [COS console](https://console.cloud.tencent.com/cos5). The inventory feature allows you to regularly (daily/weekly) publish inventory reports about the object attributes, configurations, and more. For more information about inventory, see [Inventory Overview](https://www.tencentcloud.com/document/product/436/30622). The following describes how to enable the inventory feature for a bucket. COS allows you to generate inventories on schedule or on the fly as needed.

>!
> - You can configure multiple inventory jobs for a single bucket.
> - Inventory jobs do not directly read the object content during execution. Instead, they only scan the attribute information such as the object metadata.
> 

## Prerequisites

You have created a bucket. For more information, see [Creating a Bucket](https://www.tencentcloud.com/document/product/436/13309).

## Directions

### Adding a scheduled inventory

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**.
3. Click the name of the source bucket that you want to enable inventory for.
4. Select **Basic Configurations** > **Inventory** on the left and click **Add Inventory**.
5. On the **Configuration** page, you can configure the following items:
 1. Basic information
    - **Rule Status**: Whether to enable this inventory rule. Valid values: **Enable**, **Disable**.
    - **Inventory Name**: Name of the inventory.
    - **Destination Bucket**: Bucket where the inventory is stored. Defaults to the source bucket. The destination bucket must be in the same region as the source bucket.
    - **Report Prefix (Optional)**: Prefix selected for the destination bucket. The prefix can be used to group the inventory files in a public location. The default value is used initially.
 2. Filter
    - **Scope of the file**: Object scope to apply the inventory rule. **The whole bucket** is selected by default.
	- **Object Version**: Whether to include all object versions or only the current version in the inventory. If not set, only the current version will be included.
	- **Filter Labels** (optional): Lists objects with the same tag to the inventory. If this field is not set, no tag will be filtered.
	- **Filter Time (Optional)**: Filters only objects modified after the specified time or within the specified period in the inventory. If not set, no time filter will be applied.
	- **Inventory Information**: Object information to be included in the inventory report. Options include object size, storage class, ETag, cross-bucket replication status, multipart upload status, last updated time, tag, and CRC-64. If not specified, all options will be selected.
>?
>- `ETag` (entity tag) is the hash value of the object. It only reflects changes in the object content but not the object metadata. The value of `ETag` is not necessarily the MD5 checksum of the object. The value can be different if the uploaded object is encrypted.
>- The generated inventory contains the `Appid`, `Bucket`, `Key`, and `LastModifiedTime` fields by default.
>- If versioning is enabled for the bucket, the generated inventory will also contain the `VersionId`, `IsLatest`, and `IsDeleteMarker` fields.
>
 3. Output format
	- **Output Format**: The output inventory file is a CSV file compressed with GZIP.
	- **Generate Lifecycle**: Specifies whether to generate the inventory **Everyday** (default) or **Everyweek**. For example, an inventory added at 15:00 today will be generated and delivered to the destination bucket before 6:00 tomorrow in most cases. If you select to generate inventories by week, an inventory will be generated every 7 days. For example, if you enable inventory on September 1, then an inventory will be generated on September 2, 9, 16, and so on.
	- **Inventory Encryption**: whether to encrypt the inventory on the server. Options include:
		 - None: The inventory is not encrypted (default).
		 - SSE-COS: Encrypt the inventory report using server-side encryption with COS-managed key. For more information, see [SSE-COS Encryption](https://www.tencentcloud.com/document/product/436/18145) in the COS Developer Guide.
	- **Access authorization**: This field needs to be enabled to proceed with the next step. By default, this field is disabled.
 4. Information confirmation
Confirm the bucket inventory configurations. If you need to change anything, click **Previous** and modify as needed.
6. Click **OK**. COS will generate inventory reports daily or weekly and deliver them to the destination bucket you set.
>? For more information about the format and content of the generated inventory reports, see [Inventory Overview](https://www.tencentcloud.com/document/product/436/30622).
>

### Generating an instant inventory

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List** and then click the bucket (source bucket) that you want to enable inventory for.
3. Click **Basic Configurations** > **Inventory** on the left, select an inventory rule, and click **Generate Instant Inventory** on the right to generate an instant inventory.
>? 
>- To generate an instant inventory, click **Generate Instant Inventory** in the **Operation** column.
>- If you haven't configured inventory, you can configure one and then generate an instant inventory.
>


