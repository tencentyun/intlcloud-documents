## Overview
Making snapshot is an important method for data sharing and migration. Cloud disks created using a snapshot own all data in the snapshot. You can use a snapshot to create a cloud disk whose capacity is greater than or equal to that of the snapshot.
- When you use a snapshot to create a data disk of the same size as the snapshot, the new data disk doesn't need to be initialized. You can directly [attach](/doc/product/362/5745) it, right-click <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-5px 0px "> > **Disk Management**, and set it to **Online** to bring it online in the CVM instance, after which it can be normally read and written.
- When you use a snapshot to create a data disk whose capacity is greater than that of the snapshot, the system only expand the storage block and does not extend the file system or convert the partition format. After you [mount](https://intl.cloud.tencent.com/document/product/362/32401) the new data disk, it can only use the file system and data of the source snapshot and cannot use the new disk space. You need to manually extend the file system and convert the partition format.
  For example, if you want to a 3 TB data disk by using a data disk snapshot that uses the MBR partition format and has a capacity of 1 TB, you need to format the data disk in GPT partition style because the maximum disk space supported in MBR partition style is 2 TB. 	Note that this operation will **delete original data**.

This document describes how to use a snapshot to create a cloud disk on the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page. When [creating a cloud disk](https://intl.cloud.tencent.com/document/product/362/5744), you can configure the **Snapshots** parameter to specify a snapshot for creating the cloud disk.


## Directions

### Creating a cloud disk with a snapshot in the console
1. Log in to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. On the row of the target snapshot, select **More** > **Create Cloud Disk**.
3. In the **Purchase Data Disk** pop-up window, configure the following parameters:
<table>
     <tr>
         <th width="14%">Parameter</th>  
         <th>Configuration</th>  
     </tr>
	<tr>
         <td>AZ</td>
         <td>Required.</br>The availability zone where the created cloud disk resides. It cannot be modified after the cloud disk is created.</td>
     </tr>
     <tr>
         <td>Cloud Disk Type</td>
         <td>Required.</br>For more information on cloud disk types, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>.</td>
     </tr>
     <tr>
         <td>Capacity</td>
         <td>Required.</br>For more information on the cloud disk capacity and specifications, see <a href="https://intl.cloud.tencent.com/document/product/362/31636#performance">Performance metrics</a>. When you create a cloud disk with a snapshot, the disk capacity cannot be smaller than that of the snapshot. If you don't specify the capacity of the cloud disk, the capacity is equal to that of the snapshot by default.</td>
     </tr>
	<tr>
         <td>Snapshots</td>
				 <td>Optional. To use a snapshot to create a cloud disk, select **Create a Cloud Disk with a Snapshot** and select the required snapshot. <ul><li>The disk capacity is the same as that of the snapshot by default. You can adjust the capacity to be greater than that of the snapshot.</li><li>The disk type is the same as that of the snapshot by default. You can change the cloud disk type.</li></ul></td>
     </tr>
     <tr>
         <td>Disk Name</td>
         <td>Optional.</br>A maximum of 20 characters are supported. It must start with a letter and can be a combination of letters, digits, and special symbols (`.`, `_`, `:`, and `-`). This parameter can be modified after the cloud disk is created.<ul><li>If you create only one cloud disk, the disk name is the name of the cloud disk you create.</li><li>If you create multiple cloud disks at one time, the disk name entered will be used as he prefix of the final disk name, in the format of **disk name_number**, for example, "disk name_0" to "disk name_49".</li></ul></td>
     </tr>
	 <tr>
         <td>Projects</td>
         <td>Required.<br>When creating a cloud disk, you can configure the project to which the cloud disk belongs. The default value is <b>Default Project</b>.</td>
     </tr>
	 <tr>
         <td>Label</td>
         <td>Optional.<br>When creating a cloud disk, you can bind a tag to it. A tag is used for identification, helping you categorize and search cloud resources. For more information on tags, see <a href="https://www.tencentcloud.com/document/product/651">Tag</a>.</td>
     </tr>
	 <tr>
         <td>Billing mode</td>
				 <td>Required.</br>The cloud disk supports the following billing modes:<ul><li>Monthly subscription. If this mode is selected, you must set the **Purchase Period**.</li><li>Pay-as-you-go.</li></ul></td>
     </tr>
	 <tr>
	 	 <tr>
         <td>Scheduled Snapshot</td>
         <td>Optional.<br>When creating a cloud disk, you can select **Scheduled Snapshot** to create snapshots for the cloud disk periodically based on the created scheduled snapshot policy. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/35238">Scheduled Snapshot</a>.
     </tr>
	 <tr>
         <td>Quantity</td>
         <td>Optional.<br>The default value is <b>1</b>, meaning only one cloud disk is created. Currently, up to 50 cloud disks can be created at a time.</td>
     </tr>
	 <tr>
         <td>Validity Period</td>
				 <td><ul><li>If the **Billing mode** is <b>Monthly Subscription</b>, this parameter is required. Value range: One month to five years.</li><li>If the **Billing Mode** is <b>Pay-as-you-go</b>, this parameter is not involved.</li></ul></td>
     </tr>
     <tr>
         <td>Automatic Renewal</td>
         <td><ul>
				 <li>If the **Billing Mode** is <b>Monthly Subscription</b>, this parameter is optional. If you select **Auto-renewal**, auto-renewal will be performed on the device monthly upon expiration if your account has a sufficient balance. 
					</li>
				 <li>If the **Billing Mode** is <b>Pay-as-you-go</b>, this parameter is not involved.</li></ul></td>
     </tr>
</table>
4. Click **OK**.
   - If the **Billing Mode** is **Pay-as-you-go**, the creation is completed.
   - If the **Billing Mode** is **Monthly Subscription**, the **Information Verification** page will be popped up.
    1. After you confirm the specifications, select whether to use a voucher as needed and click **Submit Order**.
    2. Complete the payment.
5. You can view the cloud disk you created in the [Cloud Disk List](https://console.cloud.tencent.com/cvm/cbs). The new elastic cloud disk is in the **To be attached** status. To attach it to a CVM instance in the same AZ, see [Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

### Using an API to create a cloud disk from snapshot
You can use the `CreateDisks` API to create a cloud disk. For more information, see [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).


