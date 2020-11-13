## Overview

The COS batch operation feature allows you to perform large-scale batch operations on objects in a bucket. Currently, you can perform the following batch operations:

- Replicating objects
- Restoring archived objects

You can generate an inventory file for the objects on which to perform a batch operation using either COS inventory (you need to first [enable inventory feature](https://intl.cloud.tencent.com/document/product/436/30624)), or the CSV format you specify. COS will then perform this batch operation based on the inventory file. For more information on batch operations, see [Overview](https://intl.cloud.tencent.com/document/product/436/32958).

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Batch Operation** on the left sidebar to enter the batch operation management page.
2. Click **Create Job** to create a batch operation job and configure the following:
 - **Job Region**: select a region for the job. It must be the same as the bucket region where the objects in your inventory file reside; otherwise the job will fail.
 >?Currently, COS batch operation is only available in public cloud regions in Chinese mainland.
 - **Inventory Format**: select a format for the objects to be inventoried from the following two options:
<table>
   <tr>
      <th>Inventory Format</th>
      <th>Field</th>
      <th>Description</th>
   </tr>
   <tr>
      <td nowrap="nowrap">COS inventory report</td>
      <td>-</td>
      <td>Please select this format if you want to generate the inventory file by using COS inventory.</td>
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
 -**Inventory Bucket**: select the bucket where the inventory file is stored.
 -**Inventory File Path**: specify the path of COS inventory report or CSV file in the format: `directory/manifest.json` or `directory/manifest.csv`, respectively. For example, if you have an inventory stored in the `examplebucket-1250000000` root directory, the inventory path will be `manifest.json`. 
![](https://main.qcloudimg.com/raw/5544edff70879dbee24dc2e3fef0c36e.png)
3. If an inventory ETag automatically appears, you have selected the correct inventory file. Then, click **Next** to enter the “Operation Configuration” page, select either of the following two job types, and configure accordingly:
  - **Batch Data Copy**:
    - Destination Bucket: select the bucket to store the object copies.
    - Storage Class: specify the storage class for object copies. Valid values: STANDARD, STANDARD_IA, ARCHIVE.
    - Server-Side Encryption: specify whether to encrypt the object copies. Valid values: None, SSE-COS.
    - Access Permissions: configure access permissions for the object copies. Valid values: Inherit destination bucket permissions, Private Read/Write, Public Read/Private Write.
    - Object Metadata: configure metadata for the object copies. Valid values: Copy all metadata, Replace all metadata.
  - **Restored archived objects in batches**：
    - Restoration Mode: you can select either standard or bulk mode. For more information on restoration modes, see [Restoring an Archived Object](https://intl.cloud.tencent.com/document/product/436/30961).
    - Validity: specify the number of days after which the object copies will expire and be automatically deleted. This value ranges from 1 to 365.
      ![](https://main.qcloudimg.com/raw/4a51de0288564cb70ac5249523637e3e.png)
4. Click **Next** to enter the "Other Configuration" page where you should configure the following:
 - **Job Description (Optional)**: description of the job. This field is optional.
 - **Job Priority**: a job of a higher priority will be performed first. The value must be a positive integer. A larger value indicates a higher priority.
 - **Job Report**: select whether to generate a job report.
 - **CAM Role**: you can create a CAM role or select an existing role to grant operation permissions to COS.
![](https://main.qcloudimg.com/raw/3a45c1180a241468084fcff59f1018e8.png)
> !For COS to perform batch operations, you need to use a CAM role to grant permissions. For more information on CAM roles, please see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420).
5. Click **Next** to check all the information you have configured. If you need to make a change, click **Modify** or **Previous** accordingly. After confirming that everything is correct, click **Created**.
![](https://main.qcloudimg.com/raw/2f84d4dafa2586e6ca9aacae5d5b7d47.png)
6. Once completed, find the new job in the job list, and click **Pending** > **Confirm** under **Status**. To cancel the job, click **Cancel Job** under **Operation**.
![](https://main.qcloudimg.com/raw/45577c34529204109a436bce596e428c.png)


