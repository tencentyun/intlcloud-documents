## Overview
CBS allows you to create a cloud disk and attach it to any CVM in the same availability zone. The cloud disk is identified and used by the CVM through block storage device mapping. Once created, the cloud disk can reach its maximum performance without prefetch.
You can create different types of CBS cloud disks based on business needs. For more information about CBS disk types, see [CBS Types](https://intl.cloud.tencent.com/document/product/362/31636).

## Prerequisites
- Before creating a cloud disk, you need to [sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
### Creating a cloud disk through the Console

1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. Select a region and click **+ New**.
3. In the **Purchase Data Disk** dialog box, configure the following parameters:
<table>
     <tr>
         <th width="12%">Parameter</th>  
         <th>Description</th>  
     </tr>
	 <tr>
         <td>Availability Zone</td>
         <td>Required.</br>The availability zone where your cloud disk resides. It cannot be modified after the cloud disk was created.</td>
     </tr> 
	 <tr>
         <td>Cloud Disk Type</td>
         <td>Required.</br>CBS offers 2 cloud disk types:<ul><li>Premium cloud storage</li><li>SSD</li><li>Enhanced SSD</li></ul></td>
     </tr>
		 <tr>
			 <td>Quick Disk Creation</td>
			 <td>Optional. To create a cloud disk using a snapshot, you need to tick **Create a cloud disk with a snapshot** and select the snapshot you want to use.
				 <ul><li>The capacity of a cloud disk created using a snapshot is equal to that of the snapshot by default. You can adjust the disk capacity.</li>
         <li>When you create a cloud disk using s snapshot, the disk type is the same as that of the snapshot’s source disk. You can adjust the disk type.</li></ul></td>
		 </tr>
	 <tr>
         <td>Capacity</td>
         <td>Required.</br>CBS provides the following cloud disk capacity and specifications:<ul><li>Premium Cloud Storage: 10 GB - 16000 GB</li><li>SSD: 100 GB - 16000 GB</li><li>Enhanced SSD: 100 GB-16,000 GB</li></ul>When you create a cloud disk using a snapshot, the disk capacity cannot be smaller than that of the snapshot. If you do not specify this parameter, the disk capacity is equal to that of the snapshot by default.</td>
     </tr>
	 <tr>
	 <tr>
         <td>Scheduled Snapshot</td>
         <td>Optional.<br>You can associate scheduled snapshot policies when creating a cloud disk to regularly manage your cloud disk snapshots. Currently, Tencent Cloud provides a 50 GB free tier for each region in mainland China. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>.
         </td>
     </tr>
     <tr>
         <td>Disk Name</td>
         <td>Optional.</br>A maximum of 20 characters start with a letter or Chinese character, and can be a combination of upper- and lower-case letters, Chinese characters, numbers, and special characters `.`, `_`, `:`. This parameter can be modified after the cloud disk was created.<ul><li>Creating a single cloud disk: disk name is the name of the cloud disk you create.</li><li>Batch creating cloud disks: when you create multiple cloud disks at one time, disk name is the prefix of your cloud disk names, which are **disk name_number** ranging from "disk name_0" to "disk name_49".</li></ul></td>
     </tr>
	 <tr>
         <td>Project</td>
         <td>Required.</br>When creating a cloud disk, you can configure the project to which the cloud disk belongs. Default value: **DEFAULT PROJECT**.</td>
     </tr>
	 <tr>
         <td>Tag</td>
         <td>Optional.</br>When creating a cloud disk, you can bind a tag to it. Tag is used for identification, helping you easily categorize and search for cloud resources. For more information about tags, see <a href="https://intl.cloud.tencent.com/document/product/651">Tag</a>.</td>
     </tr>
	 <tr>
         <td>Billing Mode</td>
         <td>Required.</br>CBS is pay-as-you-go.</td>
     </tr>
	  <tr>
         <td>Quantity</td>
         <td>Optional.</br>Default value is **1**, meaning only one cloud disk is created. Currently, up to 50 cloud disks can be created at one time.</td>
     </tr>
	 <tr>
         <td>Period</td>
         <td>The **Pay-as-you-go** billing mode does not involve this parameter.</td>
     </tr>
</table>
4. Click **OK**.
 - If **Billing Mode** is **Pay-as-you-go**, the creation is completed.
  <ol>
  1. Once you confirm your configuration, select whether to use the voucher based on actual needs, and then click **Confirm**.
  2. Complete the payment.
 </ol>
5. You can view the cloud disk(s) you created in the [Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs) list page. The newly added elastic cloud disk has a **To be mounted** status. To mount it to a CVM in the same availability zone, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

### Creating a cloud disk using a snapshot
If you want to create a cloud disk that contains all data upon creation, you can [create cloud disks using snapshots](https://intl.cloud.tencent.com/document/product/362/5757).

### Creating a cloud disk using API
You can use the `CreateDisks` API to create a cloud disk. For more information, see [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).
