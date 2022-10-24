## Overview

Snapshots are an important way of data sharing and migration. File systems created using a snapshot own all data in the snapshot. You can use a snapshot to create a file system (to ensure data security, only new file systems can be created from snapshots).

This document describes how to use a snapshot to create a file system on the snapshot list page. When [creating a file system](https://console.cloud.tencent.com/cfs/fs/create?rid=1), you can configure the **Snapshots** parameter to specify a snapshot for creating the file system.


## Directions

1. Log in to the CFS console and go to the [Snapshot List](https://console.cloud.tencent.com/cfs/snapshot/list?rid=4) page.
2. Click **Use** in the row of the target snapshot.
3. On the file system creation page, select the file system type, click **Next: Set Up Details**, and set the following parameters.
>? The following describes the parameters for creating a file system of Standard type as an example.
>
  <table>
     <tr>
       <th nowrap="nowrap">Field</th>
       <th>Description</th>
     </tr>
     <tr>
       <td>Billing Mode</td>
       <td>Select the desired billing mode. Two billing modes are supported: pay-as-you-go and prepaid.</br><b>Note: </b>Only some products support the prepaid mode.</td>
     </tr>
   	<tr>
       <td>File System Name</td>
       <td>Customize the name of the file system to create.</td>
     </tr>
     <tr>
       <td>Region</td>
       <td>Select the region where the file system is to be created.</td>
     </tr>
     <tr>
       <td nowrap="nowrap">Availability Zone</td>
       <td>Select the availability zone where the file system is to be created.</td>
     </tr>
     <tr>
       <td nowrap="nowrap">Protocol</td>
       <td>Select a protocol type, NFS or SMB, for the file system. NFS is more suitable for Linux and Unix clients. CIFS/SMB is more suitable for Windows clients. The Turbo series can only be used by private clients and does not allow the selection of file system protocols.</td>
     </tr> 
     <tr>
       <td nowrap="nowrap">Data Source</td>
       <td>Optional. To create a file system using a snapshot, you need to select **Use a snapshot** and select the snapshot you want to use. If you create a file system using a snapshot, the initial data amount on the file system is the same as the snapshot size.</td>
     </tr>
     <tr>
       <td>Permission Group</td>
       <td>Each file system must be bound to a permission group. The permission group specifies an allowlist that can access the file system and lists the read and write permissions.
       </td>
     </tr>
     <tr>
       <td>Scheduled Snapshot</td>
       <td>Optional. When creating a file system, you can select **Scheduled Snapshot** to create snapshots for the file system periodically based on the created scheduled snapshot policy. For more information, see <a href="https://intl.cloud.tencent.com/document/product/582/44915">Scheduled Snapshots</a>.
       </td>
     </tr>
   	 <tr>
       <td>Storage Capacity</td>
       <td>Required only for the Turbo series. The Turbo series is an exclusive cluster and has restrictions on the minimum cluster scale and expansion step. For Standard Turbo, the minimum initial cluster scale is 40 TiB, and the expansion step is 20 TiB. For High-Performance Turbo, the minimum initial cluster scale is 20 TiB, and the expansion step is 10 TiB.
     </tr>
   	 <tr>
       <td>CCN</td>
       <td>Required only for the Turbo series. Select an existing CCN or create a new one. For more information, see <a href="https://www.tencentcloud.com/products/ccn">Cloud Connect Network</a>. 
     </tr>
   	<tr>
       <td>IP Range</td>
       <td>Required only for the Turbo series. This parameter allows you to reserve an IP range for Turbo related components. Ensure that the selected IP range does not conflict with the IP ranges of other instances on the cloud that need to communicate with Turbo. To ensure the number of IP addresses in the IP range, the mask must have 16 to 24 bits, for example, 10.0.0.0/24.
       </td>
   	 </tr>
   	<tr>
       <td>Tag</td>
       <td>
   		<ul  style="margin: 0;">
         <li>If you already have a tag, you can add it to the new file system here.</li>
   			<li>If you do not have a tag, log in to the <a href="https://console.cloud.tencent.com/tag/taglist">Tag console</a> to create a desired tag, and then bind it to the file system. You can also add a tag to the file system after the file system is created.</li></ul>
       </td>
     </tr>
   </table>
4. Click **Create Now**. You can see the newly created file system on the file system list.


