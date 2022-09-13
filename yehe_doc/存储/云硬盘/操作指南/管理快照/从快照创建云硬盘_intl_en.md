## Overview
Making snapshot is an important method for data sharing and migration. Cloud disks created using a snapshot own all data in the snapshot. You can use a snapshot to create a cloud disk whose capacity is greater than or equal to that of the snapshot.
- When you use a snapshot to create a data disk with the same capacity as that of the snapshot, the data disk does not need to be initialized. To read and write into it, you only need to [mount](https://intl.cloud.tencent.com/document/product/362/32401) it and choose **Server Management** -> **Storage** -> **Disk Management** to associate it with a CVM.
- When you use a snapshot to create a data disk whose capacity is greater than that of the snapshot, the system only expand the storage block and does not extend the file system or convert the partition format. After you [mount](https://intl.cloud.tencent.com/document/product/362/32401) the new data disk, it can only use the file system and data of the source snapshot and cannot use the new disk space. You need to manually extend the file system and convert the partition format.
  For example, if you want to a 3 TB data disk by using a data disk snapshot that uses the MBR partition format and has a capacity of 1 TB, you need to format the data disk in GPT partition style because the maximum disk space supported in MBR partition style is 2 TB. Please note that this operation will **delete original data**.

This document describes how to use a snapshot to create a cloud disk on the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page. When [creating a cloud disk](https://intl.cloud.tencent.com/document/product/362/5744), you can configure the **Snapshots** parameter to specify a snapshot for creating the cloud disk.


## Directions
### Creating a cloud disk with a snapshot in the console
1. Log in to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. In the row of the target snapshot, click **More** and select **Create Cloud Disk**.
3. In the **Purchase Data Disk** dialog box, configure the following parameters:
<table>
     <tr>
         <th width="12%">Parameter</th>  
         <th>Description</th>  
     </tr>
	<tr>
         <td>Availability Zone</td>
         <td>Required.</br>The availability zone where the created cloud disk resides. It cannot be modified after the cloud disk is created.</td>
     </tr>
     <tr>
         <td>Cloud Disk Type</td>
         <td>Required.</br>The values include:<ul><li>Premium Cloud Disk</li><li>SSD </li></ul></td>
     </tr>
     <tr>
         <td>Capacity</td>
         <td>Required.</br>CBS provides the following cloud disk capacity and specifications:<ul><li>Premium Cloud Disk: 50 to 16,000 GB</li><li>SSD: 100 to 16,000 GB</li></ul>When you create a cloud disk using a snapshot, the disk capacity cannot be smaller than that of the snapshot. If you do not specify this parameter, the disk capacity is equal to that of the snapshot by default.</td>
     </tr>
	<tr>
         <td>Snapshots</td>
				 <td>Optional. To use a snapshot to create a cloud disk, select **Create a Cloud Disk with a Snapshot** and select the required snapshot. <ul><li>The disk capacity is the same as that of the snapshot by default. You can adjust the capacity to be greater than that of the snapshot.</li><li>The disk type is the same as that of the snapshot by default. You can change the cloud disk type.</li></ul></td>
     </tr>
     <tr>
         <td>Disk Name</td>
         <td>Optional.</br>A maximum of 20 characters are supported. It must start with a letter, and can be a combination of letters, digits, and special characters (`.`, `_`, `:`, and `-`). This parameter can be modified after the cloud disk is created.<ul><li>If you create only one cloud disk, the disk name is the name of the cloud disk you create.</li><li>If you create multiple cloud disks at one time, the disk name entered will be used as he prefix of the final disk name, in the format of **disk name_number**, for example, "disk name_0" to "disk name_49".</li></ul></td>
     </tr>
	 <tr>
         <td>Project</td>
         <td>Required.</br>When creating a cloud disk, you can configure the project to which the cloud disk belongs. The default value is **DEFAULT PROJECT**.</td>
     </tr>
	 <tr>
         <td>Tag</td>
         <td>Optional.</br>When creating a cloud disk, you can bind a tag to it. Tags are used to identify cloud resources, helping you easily categorize and search for cloud resources. For more information, see <a href="https://intl.cloud.tencent.com/document/product/651">Tag</a>.</td>
     </tr>
	 <tr>
         <td>Billing Mode</td>
         <td>Required.<li>The value is **Pay as you go**.</li></ul></td>
     </tr>
	 <tr>
	 	 <tr>
         <td>Scheduled Snapshot</td>
         <td>Optional.</br>When creating a cloud disk, you can select **Scheduled Snapshot** to create snapshots for the cloud disk periodically based on the created scheduled snapshot policy. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/35238">Scheduled Snapshot</a>.
     </tr>
	 <tr>
         <td>Quantity</td>
         <td>Optional.</br>The default value is **1**, which indicates that only one cloud disk is created. Currently, up to 50 cloud disks can be created at one time.</td>
     </tr>
	 <tr>
         <td>Period</td>
         <td></li><li>If **Billing Mode** is set to **Pay as you go**, this parameter is not involved.</li></ul></td>
     </tr>
		 		 <tr>
         <td>Automatic Renewal</td>
         <td> <li>If **Billing Mode** is set to **Pay as you go**, this parameter is not involved.</li></ul></td>
	 </tr>
</table>
4. Click **OK**.
 - If **Billing Mode** is **Pay as you go**, the creation is completed.
  <ol>
  1. After you confirm your configuration, select whether to use a voucher based on actual needs, and then click **OK**.
  2. Complete the payment.
 </ol>
5. You can view the cloud disk(s) you created in the [Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs) list page. New elastic cloud disks are in the **To be mounted** state. For more information on how to mount an elastic cloud disk to a CVM in the same availability zone, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

### Using an API to create a cloud disk from snapshot
You can use the `CreateDisks` API to create a cloud disk. For more information, see [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).
