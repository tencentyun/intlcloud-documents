## Overview
CBS allows you to create a cloud disk and attach it to any CVM in the same availability zone. The cloud disk is identified and used by the CVM through block storage device mapping. Once created, the cloud disk can reach its maximum performance without prefetch.
You can create different types of cloud disks as needed as detailed in [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636).

## Prerequisite
- Before creating a cloud disk, you need to [sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
<dx-tabs>
::: Creating a cloud disk through the console
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Select a region and click **Create**.
3. In the **Purchase Data Disk** dialog box, configure the following parameters:

<table>
     <tr>
         <th width="15%">Parameter</th>  
         <th>Configuration</th>  
     </tr>
	 <tr>
         <td>AZ</td>
         <td>Required.</br>The availability zone where the created cloud disk resides. It cannot be modified after the cloud disk is created.</td>
     </tr> 
	 <tr>
         <td>Cloud Disk Type</td>
         <td>Required.</br>Cloud disk types include:<ul><li>Premium Cloud Storage</li><li>Balanced SSD</li><li>SSD</li><li>Enhanced SSD</li><li>ulTra SSD. This type can only be purchased together with the Storage Optimized CVM instance.</li></ul></td>
     </tr>
		 <tr>
			 <td>Quick Disk Creation</td>
			 <td>Optional. To create a cloud disk using a snapshot, you need to tick <b>Create a cloud disk with a snapshot</b> and select the snapshot you want to use.
				 <ul><li>The capacity of a cloud disk created using a snapshot is equal to that of the snapshot by default. You can adjust the disk capacity.</li>
         <li>When you create a cloud disk using a snapshot, the disk type is the same as that of the snapshot's source disk. You can change the disk type.</li></ul></td>
		 </tr>
	 <tr>
         <td>Capacity</td>
         <td>Required.</br>The cloud disk capacity and specifications are as follows:<ul><li>Premium Cloud Storage: 10 to 32,000 GB</li><li>Balanced SSD: 20 to 32,000 GB</li><li>SSD: 20 to 32,000 GB</li><li>Enhanced SSD: 20 to 32,000 GB</li></ul>When you create a cloud disk with a snapshot, the disk capacity cannot be smaller than that of the snapshot. If you don't specify the capacity of the cloud disk, the capacity is equal to that of the snapshot by default.</td>
     </tr>
	 <tr>
	 <tr>
         <td>Scheduled Snapshot</td>
         <td>Optional.<br>You can associate scheduled snapshot policies when creating a cloud disk to regularly manage your cloud disk snapshots. Currently, Tencent Cloud provides a 50 GB free tier for each region in the Chinese mainland. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>.
         </td>
     </tr>
     <tr>
         <td>Disk Name</td>
         <td>Optional.</br>A maximum of 128 characters are supported. It must start with a letter and can be a combination of letters, digits, and special symbols (<code>.</code>, <code>_</code>, <code>:</code>, <code>-</code>). This parameter can be modified after the cloud disk is created.<ul><li>Creating a single cloud disk: The disk name entered is the name of the cloud disk you create.</li><li>Batch creating cloud disks: The disk name entered is the prefix of your cloud disk names, in the format of <b>disk name_number</b>.</li></ul></td>
     </tr>
	 <tr>
         <td>Projects</td>
         <td>Required.</br>When creating a cloud disk, you can configure the project to which the cloud disk belongs. The default value is <b>DEFAULT PROJECT</b>.</td>
     </tr>
	 <tr>
         <td>Label</td>
         <td>Optional.</br>When creating a cloud disk, you can bind a tag to it. A tag is used for identification, helping you categorize and search cloud resources. For more information on tags, see <a href="hhttps://intl.cloud.tencent.com/zh/document/product/651">Tag</a>.</td>
     </tr>
	 <tr>
         <td>Billing mode</td>
         <td>Required</br>CBS is pay-as-you-go.</td>
     </tr>
	  <tr>
         <td>Quantity</td>
         <td>Optional.</br>The default value is <b>1</b>, meaning only one cloud disk is created. Currently, up to 50 cloud disks can be created at one time.</td>
     </tr>
	 <tr>
         <td>Validity Period</td>
         <td><ul><li>The <b>pay-as-you-go</b> billing mode does not involve this parameter.</li></ul></td>
     </tr>
</table>


4. Click **OK**.
 If **Billing Mode** is **Pay-as-you-go**, the creation is completed.


 5. You can view the cloud disk(s) you created in the [Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs) list page. The new elastic cloud disk is in the **To be attached** status. To attach it to a CVM instance in the same availability zone, see [Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

:::
::: Creating a cloud disk using a snapshot
If you want to create a cloud disk that contains all data upon creation, you can [create cloud disks using snapshots](https://intl.cloud.tencent.com/document/product/362/5757).
:::
::: Creating a cloud disk using the API
You can use the `CreateDisks` API to create a cloud disk. For more information, see [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).
:::
</dx-tabs>



