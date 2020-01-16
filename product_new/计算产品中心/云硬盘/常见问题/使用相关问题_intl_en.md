### What scenarios can cloud disks be used for?
- After purchasing CVMs, you realize the disk space is insufficient. You can [purchase](https://intl.cloud.tencent.com/document/product/362/5744) and [mount](https://intl.cloud.tencent.com/document/product/362/32401) elastic cloud disks to be used as data disks, satisfying storage requirements.
- When purchasing CVMs, you do not want to purchase additional data disks. When you have storage requirements, you can purchase an elastic cloud disk and mount it for use as a data disk.
- CVM A has 10GB of important data stored on an elastic cloud disk, and you need to share the data with CVM B. You can directly [unmount](https://intl.cloud.tencent.com/document/product/362/32400) the disk from CVM A, and then [mount](https://intl.cloud.tencent.com/document/product/362/32401) it to CVM B.
- When a single maximum size cloud disk cannot meet storage requirements, you can purchase multiple cloud disks with equal capacity and configure LVM logical volumes to provide a larger disk capacity.
- When I/O performance of a single disk cannot meet business requirements, you can purchase multiple cloud disks and configure Raid 0, Raid 10, etc., to enhance I/O performance.

For more information, see [Cloud disk application scenarios](https://intl.cloud.tencent.com/document/product/362/3065).

### How should I select cloud disk types?
Before you select a disk type, first determine the usage scenario.
- For scenarios where requests are relatively infrequent, such as system logs, enterprise work files, data warehouse, small-sized blogs, and BBS, we recommend you use HDD cloud disks to reduce costs.
- For general scenarios such as mid- and small-sized databases, Web/App applications, and transactional workloads, we recommend you use premium cloud storage for better cost efficiency.
- For scenarios with high workloads and relatively high performance requirements such as large-sized core databases, OLTP businesses, and NoSQL databases, we recommend you use SSD cloud disks for better performance.

### What should I pay attention to when using cloud disks?
- For independently purchased cloud disks, when configuring static file system information using `fstab`, UUID or label of the file system should be used as the file system ID, to prevent changes of the cloud disk’s kernel name in the CVM caused by multiple mountings/unmounting of several disks on the same CVM. 
- If the cloud disk expires before the CVM, it will be restricted, unmounted, or even repossessed within a certain period. To prevent business interruption, please pay attention to the expiration date of the cloud disk and renew it promptly.
- If unmounting the cloud disk from the CVM will not severely impact your core business, you can consider using the `nofail` option when configuring `fstab`, to prevent the system from reporting an error when it restarts after the cloud disk is unmounted from the CVM.
- We recommend that you execute the `san policy=OnlineAll` operation in `diskpart` first before using the cloud disk in Windows operating system.
- When unmounting a cloud disk from the Windows system, we recommend you first interrupt all read-write operations on the disk, and perform the `offline` operation.

### When using a custom image and a data disk snapshot, how do I implement automatic mounting when launching new instances?
For more information, see the “Automatic Mounting” section in [Mounting cloud disks](https://intl.cloud.tencent.com/document/product/362/32401).

### How do I purchase cloud disks?
You can create cloud disks in the console or through API. For more information, see [Creating cloud disks](https://intl.cloud.tencent.com/document/product/362/5744).

### Why can’t I find the CVM to which I want to mount the cloud disk?
Cloud disks cannot be mounted across availability zones. Please confirm that your CVM instance and cloud disks locate in the same availability zone in the same region. At the same time, ensure your CVM has not been released.

### After mounting a cloud disk, why can’t I see the new cloud disk capacity in the CVM?
Some Linux CVMs may not recognize the elastic cloud disk. You must first enable the disk hot swapping function in the CVM. For more information, see [Enabling the disk hot swapping function].

After manually mounting cloud disks, you must select and execute the subsequent operations to make cloud disks usable.
<table>
 <tr>
 <th>Creation Mode</th>
 <th>Cloud disk capacity</th>
 <th>Subsequent Operations</th>
 </tr>
 <tr>
 <td  rowspan="2">Create directly</td>
 <td>Cloud disk capacity< 2TB</td>
 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Initializing cloud disks (smaller than 2TB)</a></td>
 </tr>
 <tr>
  <td>Cloud disk capacity ≥ 2TB</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2TB)</a></td>
 </tr>
  <tr>
	<td  rowspan="3">Create from a snapshot</td>
	<td>Cloud disk capacity = snapshot capacity</td>
	<td>No subsequent operations needed, use directly after mounting.</td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">Snapshot capacity < cloud disk capacity ≤ 2TB <br/>or<br/>2TB < Snapshot capacity < cloud disk capacity</td>
<td><ul><li>Mounting to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601"> Expanding partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31602">Expanding partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 <tr>
 <td>Snapshot capacity ≤ 2TB < cloud disk capacity</td>
<td nowrap="nowrap"><ul><li>If MBR partition format is used in the snapshot: </li>Refer to <a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2TB)</a>Using GPT to re-partition:<b>This operation will delete the original data</b><li>If GPT partition format is used in the snapshot: <ul><li>Mounting to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601">Expanding partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31602">Expanding partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 </table>


### After mounting a cloud disk, how do I perform partitioning and formatting?
For more information, see [Initializing cloud disks (smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) or [Initializing cloud disks (larger than or equal to 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### Is access by multiple CVMs to one cloud disk supported?
This is not supported currently. You can mount up to 10 cloud disks to the same CVM, but multiple CVMs cannot concurrently share the same cloud disk. You can only share data by [unmounting](https://intl.cloud.tencent.com/document/product/362/32400) from CVM A and then [mounting](https://intl.cloud.tencent.com/document/product/362/32401) to CVM B.

### Several cloud disks of the same size and type are mounted on the same CVM. How do I distinguish them in the operating system?
- For Linux operating systems, you can view the corresponding relationship between the elastic cloud disk and the device name by executing the following command:
```
ls -l /dev/disk/by-id
```
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)

- For Windows operating systems, you can execute the following command to view:
```
wmic diskdrive get caption,deviceid,serialnumber
```
or
```
wmic path win32_physicalmedia get SerialNumber,Tag
```
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)

### Can I unmount the data disk that I purchased along with a CVM?
Since November 2017, data disks purchased along with CVMs support unmounting and remounting. To avoid lifecycle management difficulties when data disks are unmounted and remounted to another CVM with a different expiration date, we provide various options such as expiration date alignment and automatic renewal configuration. We recommend you carefully select the appropriate lifecycle management method, to avoid data loss caused by disk expiration.

### Will data be lost during disk unmounting?
Data in cloud disks is not changed by mounting or unmounting. To ensure data consistency, we strongly recommend: 
- In Linux operating systems, log in to the CVM instance and perform the `umount` operation on the disk. After the command is successfully executed, enter the console to perform the unmount operation on the disk.
- In Windows operating systems, suspend reading and writing operations on all file systems on the disk before unmounting. Otherwise, data that has not been read or written will be lost. 

### How do I unmount elastic cloud disks?
For more information, see [Unmounting cloud disks](https://intl.cloud.tencent.com/document/product/362/32400).

### What happens to the system after the cloud disk expires?
The following instructions are only applicable for elastic cloud disks that support unmounting. Non-elastic cloud disks that do not support unmounting have the same lifecycles as CVMs. For more information, see [CVM arrears description](https://intl.cloud.tencent.com/document/product/213/2181).
- Cloud disks with monthly subscription:
 - 7 days before the resources expire, the system will send you an expiration warning and a renewal reminder.
 - If your account balance is sufficient and auto renewal is enabled, cloud disk will automatically renew on the expiry date.
 - If your cloud disk is not renewed before it expires (including on the expiration date), the system will begin to limit its performance at the point in time of its expiration. When using the cloud disk, you will notice a significant decrease in performance.
 - If your cloud disk is not renewed within 7 \* 24 hours after it expires, the system will suspend its service processing (the cloud disk is unavailable, and can only store data), **force release** its relationship with the CVM (if any), and the cloud disk will be sent to the recycle bin. You can still retrieve the cloud disk from the recycle bin and renew it, but **the start time of the cloud disk that has been renewed and retrieved will be the previous period’s expiration date**.
 - If your cloud disk has not been renewed and retrieved within 7 \* 24 hours after it has been sent to the recycle bin, the system will start to release resources. Data in the expired cloud disk will be erased and **cannot be retrieved**.

- Pay-as-you-go cloud disks:
 - You can continue to use your Pay-as-You-Go cloud disk for 2 hours from the moment your account becomes negative. We will also continue to bill you for this period. When your account is in arrears for 2 hours, the service will automatically shut down. You cloud disk will not be available and can only store data. We will also stop billing you for service.
 - If your Tencent Cloud account is topped up to a positive balance  within 24 hours after automatic shutdown, the cloud disk will be restored and billing continues.
 - If your account remains negative for 26 hours after shutdown, the Pay-as-You-Go disk will be repossessed, and all data will be deleted and **cannot be recovered**. We will notify the Tencent Cloud account creator and all the collaborators via email, SMS and the Message Center when the cloud disk is repossessed.

Please contact customer service if you need further information. 

### Can I change cloud disk type after a successful purchase?
Currently, switching cloud disks between different types is not supported. You can create snapshot backups and use the snapshot to create cloud disks of your needed type.

### Can I adjust cloud disk capacity after a successful purchase?
Yes. Cloud disks support capacity adjustment. You can [expand the capacity of cloud disks](https://intl.cloud.tencent.com/document/product/362/31600), but you cannot reduce capacity.

### What are the conditions for extending the file system?
Only cloud disks support expansion. Local disks cannot be expanded. For more information, see [Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).
>- We strongly recommend that you create a snapshot before expansion to ensure data security.
> - If the maximum capacity of the cloud disk still does not meet your business needs, you can [build RAID 1 using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2932) or [build LVM logical volumes using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).
> - MBR partition format supports a maximum disk capacity of 2TB. If your disk is in MBR format and needs to be expanded to more than 2TB, we recommend you create and mount a data disk again, use GPT partition format and then copy the data to the new disk.

### How do I expand cloud disks?
For more information about expansion operations, see [Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).

### Do CVMs support CPU/memory expansion? 
When the system disk is a cloud disk, CVM supports CPU and memory adjustments.

### What should I do when the cloud disk is partitioned in MBR format and cannot be expanded any further?
MBR partition format supports a maximum disk capacity of 2TB. If your disk is in MBR format and needs to be expanded to more than 2TB, we recommend you create and mount a data disk again, use GPT partition format and then copy the data to the new disk.

### What should I do if the cloud disk has already been expanded to maximum capacity, but still cannot meet business requirements?
We recommend you [build RAID 1 using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2932) or [build LVM logical volumes](https://intl.cloud.tencent.com/document/product/362/2933).

### How do I build a RAID group using multiple elastic cloud disks?
For more information, see [Building RAID groups using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2932).

### How do I build LVM logical volumes using multiple elastic cloud disks?
For more information, see [Building LVM logical volumes using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).

### What happens to the data when a CVM is terminated?
- Lifecycle of a system disk completely follows that of a CVM. When the CVM is terminated, data stored in the system disk will also be terminated.
- Lifecycle of a data disk (that is, elastic cloud disk) is independent from that of a CVM. You can choose whether to retain the elastic cloud disk and its data outside of the CVM lifecycle.

Therefore, we recommend that you use elastic cloud disks to store data that needs to be saved for a relatively long duration.
### How can cloud disks be recovered after formatting?
After formatting, cloud disks cannot be recovered. We recommend you [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) before formatting.

### How do I delete cloud disks?
- Lifecycle of a system disk follows that of the CVM. It can only be deleted when the [CVM is terminated](https://intl.cloud.tencent.com/document/product/213/4930).
- Lifecycle of a data disk (that is, elastic cloud disk) is independent from that of the CVM. It can be deleted separately. For more information, see [Terminating cloud disks](https://intl.cloud.tencent.com/document/product/362/32399).

### Can system disks be partitioned?
System disks do not support partitioning.

