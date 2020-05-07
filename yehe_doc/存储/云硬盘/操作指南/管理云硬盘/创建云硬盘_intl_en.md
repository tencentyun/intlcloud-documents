## Scenario
CBS allows you to create a cloud disk and connect it to any CVM in the same availability zone. The cloud disk is identified and used by the CVM through block storage device mapping. Once created, the cloud disk can reach its maximum performance without prefetch.
You can determine which type of CBS cloud disk to create based on your business needs. For more information about CBS cloud disk types, see [Cloud Disk Types](/doc/product/362/2353).

## Prerequisites
- Before you create a cloud disk, you need to [sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985), and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
### Creating a cloud disk using the console

1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. Select a region and click **Create**.
3. In the **Purchase Data Disk** dialog box, set the following parameters:
<table>
     <tr>
         <th width="12%">Parameter</th>  
         <th>Description</th>  
     </tr>
	 <tr>
         <td>AZ</td>
         <td>Required.</br>The available zone where your cloud disk resides. It cannot be modified after the cloud disk was created.</td>
     </tr> 
	 <tr>
         <td>Cloud Disk Type</td>
         <td>Required.</br>CBS offers 3 cloud disk types:<ul><li>HDD cloud disk</li><li>Premium cloud storage</li><li>SSD cloud disk</li></ul></td>
     </tr>
		 <tr>
			 <td>Quick Disk Creation<td>
			 <td>Optional. To create a cloud disk using a snapshot, you need to tick **Create a cloud disk with a snapshot** and select the snapshot you want to use.
				 <ul><li>You can adjust the capacity of a cloud disk created from a snapshot to be greater than the default value (snapshot size).</li>
         <li>You can change the type of a cloud disk created with a snapshot, which is the same as that of the snapshot source by default.</li></ul></td>
		 </tr>
	 <tr>
         <td>Capacity</td>
         <td>Required.</br>CBS provides the following cloud disk capacity and specifications:<ul><li>HDD cloud disk: 10GB-16000GB</li><li>Premium cloud storage: 10GB-16000GB</li><li>SSD cloud disk: 100GB-16000GB</li></ul>When you create a cloud disk with a snapshot, the disk capacity cannot be smaller than the snapshot size. If you do not specify this parameter, it defaults to the snapshot size value.</td>
     </tr>
	 <tr>
	 <tr>
         <td>Scheduled Snapshot</td>
         <td>Optional.<br>You can regularly manage your cloud disk snapshots by associating scheduled snapshot policies when creating cloud disks. Currently, Tencent Cloud provides a 50 GB free tier for each region in China. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/32415">Snapshot billing overview</a>.
         </td>
     </tr>
     <tr>
         <td>Disk Name</td>
         <td>Optional.</br>Allows up to 20 characters starting with an upper- or lower-case letter, or Chinese character, and can be a combination of upper- and lower-case letters, Chinese characters, numbers, and special characters `.`, `_`, `:`. This parameter can be modified after the cloud disk was created.<ul><li>Creating a single cloud disk: this parameter is the name of the cloud disk you create.</li><li>Creating multiple cloud disks: when you create multiple cloud disks at one time, this parameter is used as the prefix of your cloud disk name formatted as **disk name_number**, ranging from "disk name_0" up to "disk name_49".</li></ul></td>
     </tr>
	 <tr>
         <td>Project</td>
         <td>Required.</br>When you create a cloud disk, you can set the project to which the cloud disk belongs. Default value: **DEFAULT PROJECT**.</td>
     </tr>
	 <tr>
         <td>Tags</td>
         <td>Optional.</br>You can bind a tag to a cloud disk when creating it. Tags are used to identify cloud resources, helping you easily classify and search for them. For more information about tags, see <a href="https://intl.cloud.tencent.com/document/product/651?from_cn_redirect=1">Tag</a>.</td>
     </tr>
	 <tr>
         <td>Billing Mode</td>
         <td>Required.</br>CBS is billed based on a pay-as-you-go basis.</td>
     </tr>
	  <tr>
         <td>Quantity</td>
         <td>Optional.</br>Defaults to **1**, which means that only one cloud disk is created. Currently, up to 50 cloud disks can be created at one time.</td>
     </tr>
	 <tr>
         <td>Period</td>
         <td>The **Pay-as-you-go** billing mode does not involve this parameter.</td>
     </tr>
</table>

4. Click **OK**.

This action will complete the creation if you select **Pay-as-you-go** as **Billing Mode**.

  <ol>
  1. Once you confirm your configuration, determine whether to use voucher according to your actual needs, and then click **Confirm**.
  2. Complete the payment.
 <ol>
5. You can view the cloud disk(s) you created in the [Cloud Block Storage list](https://console.cloud.tencent.com/cvm/cbs) page. For a newly-added elastic cloud disk, its status is displayed as **To be mounted**. To mount it to a CVM in the same availability zone, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

### Creating a cloud disk from a snapshot
If you want to create a cloud disk that contains data upon creation, you can alternatively choose to [create cloud disks using snapshots](https://intl.cloud.tencent.com/document/product/362/5757).

### Creating a cloud disk using API
You can use the `CreateDisks` API to create a cloud disk. For more information, see [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).
