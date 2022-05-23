## Overview

The batch operation feature of COS can perform large-scale batch operations on objects in a bucket, currently including:

- Replicating objects
- Restoring archived objects

You can generate an inventory file for the target objects using either COS inventory (you need to first [enable inventory feature](https://intl.cloud.tencent.com/document/product/436/30624)) or the specified format. COS will then perform a batch operation based on the inventory file. For more information on batch operations, see [Overview](https://intl.cloud.tencent.com/document/product/436/32958).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Batch Operation** to enter the batch operation management page.
3. Click **Create Job** to create a batch operation job.

The configuration items are as described below:
 - **Job Region**: Select a region for the job. It must be the same as the bucket region of the objects in your inventory file; otherwise, the job will fail.
>? Currently, COS batch operation is only available in public cloud regions in the Chinese mainland.
>
 - **Inventory Format**: Select a format for the objects to be inventoried from the following two options:
<table>
   <tr>
      <th>Inventory Format</th>
      <th>Field</th>
      <th>Configuration Description</th>
   </tr>
   <tr>
      <td nowrap="nowrap">COS inventory report</td>
      <td>-</td>
      <td>Select this format if you want to generate the inventory file by using COS inventory.</td>
   </tr>
   <tr>
      <td rowspan="3">CSV</td>
      <td>Bucket</td>
      <td>Bucket name</td>
   </tr>
   <tr>
      <td>Key</td>
      <td>Name of an object in a bucket. If you use this format, the object name is URL-encoded and must be decoded before use.</td>
   </tr>
   <tr>
      <td>VersionId</td>
      <td>Object version ID. If versioning is enabled for a bucket, COS will assign a version ID to each object added to the bucket. If you do not want to inventory the latest version of an object, you can specify a particular version ID.</td>
   </tr>
</table>
 -**Inventory Bucket**: Select the bucket where the inventory file is stored.
 -**Inventory File Path**: Specify the path of the COS inventory file or CSV file in JSON or CSV format respectively. For example, if you have an inventory stored in the `examplebucket-1250000000` root directory, the inventory path will be `manifest.json`. 
4. Click **Next** and select the job type.

The configuration items are as described below:
  - **Batch data copy**:
    - Destination Bucket: Select the bucket to store the object copies.
    - Prefix Operation: You can choose to add, replace, or delete the prefix of the object copies.
    - Storage Class: Specify the storage class for object copies. Valid values: STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE.
    - Server-Side Encryption: Specify whether to encrypt the object copies. Valid values: None, SSE-COS.
    - Access Permission: Set access permissions for the object copies. Valid values: Copy all permissions, Replace all permissions, Add permissions.
    - Object Metadata: Configure metadata for the object copies. Valid values: Copy all metadata, Replace all metadata, Add metadata.
    - Object Tag: Configure tags for the object copies. Valid values: Copy all tags, Replace all tags, Add tags.
  - **Restore archived objects in batches**:
    - Restoration Mode: You can select either standard or bulk mode. For more information on restoration modes, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
    - Validity: Specify the number of days after which the object copies will expire and be automatically deleted. This value ranges from 1 to 365.
5. Click **Next** and configure the following options.

 - **Job Description (Optional)**: Description of the job. This field is optional.
 - **Job Priority**: A job of a higher priority will be performed first. The value must be a positive integer. A larger value indicates a higher priority.
 - **Job Report**: Select whether to generate a job report.
 - **CAM Role**: You can create a CAM role or select an existing role to grant operation permissions to COS.
>! For COS to perform batch operations, you need to use a CAM role to grant permissions. For more information on CAM roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420).
>
6. Click **Next**, check the batch operation job configuration you set, and select **If you select this option, the job will be directly started after creation. Make sure that the above configuration information is correct.** as needed.
To modify the information, click **Modify** or **Previous**.

7. After confirming that everything is correct, click **Create** or **Create and Start**.
Then, find the new job in the job list. To cancel the job, click **Cancel Job** on the right.



