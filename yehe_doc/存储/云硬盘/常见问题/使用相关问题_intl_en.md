### What are some use cases for different cloud disks?
- After purchasing CVMs, you realize the disk space is insufficient. You can [purchase](https://intl.cloud.tencent.com/document/product/362/5744) and [mount](https://intl.cloud.tencent.com/document/product/362/32401) elastic cloud disks to be used as data disks, satisfying storage requirements.
- When purchasing CVMs, you do not want to purchase additional data disks. When you have storage requirements, you can purchase an elastic cloud disk and mount it for use as a data disk.
- CVM A has 10GB of important data stored on an elastic cloud disk, and you need to share the data with CVM B. You can directly [unmount](https://intl.cloud.tencent.com/document/product/362/32400) the disk from CVM A, and then [mount](https://intl.cloud.tencent.com/document/product/362/32401) it to CVM B.
- When a single maximum size cloud disk cannot meet storage requirements, you can purchase multiple cloud disks with equal capacity and configure LVM logical volumes to provide a larger disk capacity.
- When I/O performance of a single disk cannot meet business requirements, you can purchase multiple cloud disks and configure RAID 0, RIAD 10, etc., to enhance I/O performance.

For more information, see [Cloud disk application scenarios](https://intl.cloud.tencent.com/document/product/362/3065).

### How do I select cloud disk types?
Before you select a disk type, first determine the usage scenario.
- For scenarios where requests are relatively infrequent, such as system logs, enterprise work files, data warehouses, small-sized blogs, and BBS, we recommend that you select HDD cloud disks to reduce costs.
- For general scenarios such as mid and small-sized databases, Web/App applications, and transactional workloads, we recommend that you select Premium Cloud Storage for higher cost efficiency.
- For scenarios with high workloads and relatively high performance requirements such as large-sized core databases, OLTP businesses, and NoSQL databases, we recommend that you select SSD cloud disks for better performance.

### What are the precautions for using cloud disks?
- For independently purchased cloud disks, when configuring static file system information using `fstab`, UUID or label of the file system should be used as the file system ID, to prevent changes of the cloud disk’s kernel name in the CVM caused by multiple mountings/unmounting of several disks on the same CVM. 
- If the cloud disk expires before the CVM, it will be restricted, unmounted, or even repossessed within a certain period. To prevent business interruption, please pay attention to the expiration date of the cloud disk and renew it promptly.
- If unmounting the cloud disk from the CVM will not severely impact your core business, you can consider using the `nofail` option when configuring `fstab`, to prevent the system from reporting an error when it restarts after the cloud disk is unmounted from the CVM.
- We recommend that you run `san policy=OnlineAll` in `diskpart` before using the cloud disk in Windows.
- When unmounting a cloud disk from Windows, we recommend that you first interrupt all read/write operations on the disk, and perform the `offline` operation.

### When using a custom image and a data disk snapshot, how do I implement automatic mounting when launching new instances?
For more information, see the “Automatic Mounting” section in [Mounting cloud disks](https://intl.cloud.tencent.com/document/product/362/32401).

### How do I purchase cloud disks?
You can create cloud disks in the console or through API. For more information, see [Creating cloud disks](https://intl.cloud.tencent.com/document/product/362/5744).

### Where can I view cloud disk details?
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs/index).
2. At the top of the "Cloud Block Storage" list page, select the region of the disk you want to view.
3. Locate the disk in the list, and view its information.
You may click the disk ID to enter the details page for more information.


### What are the most common operations with cloud disks?
For more information, see [Operation Overview](https://intl.cloud.tencent.com/document/product/362/33140).


### Why can’t I find the CVM to which I want to mount the cloud disk?
Cloud disks cannot be mounted across availability zones. Please ensure that the CVM instance and cloud disk are in the same availability zone of the same region. Please also ensure that the CVM has not been released.

### After mounting a cloud disk, why can’t I see the new cloud disk capacity in the CVM?
Some Linux CVMs may not recognize the elastic cloud disk. You must first enable the disk hot swapping function in the CVM. For more information, see [Enabling the disk hot swapping function](https://intl.cloud.tencent.com/document/product/362/32401#modprobeacpiphp).

After manually mounting cloud disks, you must select and execute the subsequent operations to make cloud disks usable.
<table>
 <tr>
 <th>Creation mode</th>
 <th>Cloud disk capacity</th>
 <th>Subsequent operations</th>
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
	<td>Cloud disk capacity = Snapshot capacity</td>
	<td><ul class="params"><li>Mounting to a Windows CVM: After logging in to the instance, make the disk online through **Server Management**>**Storage**>**Disk Management**.</li>
		<li>Mounting to a Linux CVM: After logging in to the instance, run a <code>mount <disk partition> <mount target></code> command, such as <code>mount /dev/vdb /mnt</code>.</li>
		</ul>
	</li></td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">Snapshot capacity < cloud disk capacity ≤ 2TB <br/>or<br/>2TB < Snapshot capacity < cloud disk capacity</td>
<td><ul class="params"><li>Mounting to a Windows CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31601">Expanding partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31602">Expanding partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 <tr>
 <td>Snapshot capacity ≤ 2TB < cloud disk capacity</td>
<td nowrap="nowrap"><ul class="params"><li>If MBR partition format is used in the snapshot:</li>Refer to <a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2TB)</a>Using GPT to re-partition:<b>This operation will delete the original data</b><li>If GPT partition format is used in the snapshot:<ul><li>Mounting to a Windows CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31601">Expanding partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31602">Expanding partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 </table>

 </style>
	.params{margin-bottom:0px !important;}
</style>


### After mounting a cloud disk, how do I perform partitioning and formatting?
For more information, see [Initializing cloud disks (smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) or [Initializing cloud disks (larger than or equal to 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### What is the relationship between data writing and partition formatting?
A new data disk or data disk partition cannot be used before being formatted and recording the data structure. The purpose of formatting is to establish a file system on the data disk, which means data are written to the disk during the course. Depending on the file system, the formatting approach varies with different sizes of written files as shown below:
- For Windows:
   - Quick formatting: assigns the file system only to partitions and rewrites the directory table with little use of your disk capacity.
   - Normal formatting: includes quick formatting tasks. Besides, it scans the partitions sector by sector to identify and mark bad sectors, and fills empty blocks in the cloud disk. So basically, it writes data to the entire disk. At this point, the first snapshot shows a capacity that approximates that of the cloud disk.
- For Linux: After the cloud disk is formatted and before data are written to the instance, the capacity of the first snapshot is related to the format of the disk file system.

### After expanding my cloud disk, do I need to unmount my partitions in order to create new independent ones on Linux? 
Yes, and you can follow the directions below to do so:
1. Run the following command to unmount the data disk:
```
umount <mount target>
```
If the mount target is `/data`, then run:
```
umount /data
```
2. Unmount the file systems of all partitions on the cloud disk, and execute the subsequent operations. You can run the following command again to confirm that the file systems of all partitions on the disk have been unmounted.
```
mount | grep '<Disk path>'
```
If it returns null, all partition file systems on the cloud disk have been unmounted.


### Is access by multiple CVMs to one cloud disk supported?
This is not supported currently. You can mount up to 20 cloud disks to the same CVM, but multiple CVMs cannot concurrently share the same cloud disk. You can only share data by [unmounting](https://intl.cloud.tencent.com/document/product/362/32400) from CVM A and then [mounting](https://intl.cloud.tencent.com/document/product/362/32401) to CVM B.

### Several cloud disks of the same size and type are mounted on the same CVM. How do I distinguish them in the operating system?
- In Linux, you can view the relationship between the elastic cloud disks and the device name by running the following command:
```
ls -1 /dev/disk/by-id
```
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
- In Windows, you can view the relationship by running the following command:
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

### Why is the separate cloud disk I created released together with my instance?
When mounting a cloud disk, you can set whether to automatically release it together with your instance. To enable/disable this feature, you can use the [CBS Console] (https://console.cloud.tencent.com/cvm/cbs/index) or by [modifying disk attributes](https://intl.cloud.tencent.com/document/product/362/15659) via Cloud Disk APIs.


### What should I do if I lost my data after restarting my Linux instance?
Suppose that you find all data in a directory (such as /data) are lost after the restart, and the known cause is that you didn’t mount data disk partitions, then follow the step-by-step directions below:
1. Run `fdisk -l` to view the unmounted partitions.
2. Run `mount /dev/vdb /data` to mount partitions.
3. Run `df -h` to see if they are mounted successfully.
4. Complete your configuration by referencing [Automatic Mounting](https://intl.cloud.tencent.com/document/product/362/32401#.E6.8C.82.E8.BD.BD.E6.95.B0.E6.8D.AE.E7.9B.98.EF.BC.88linux.EF.BC.89), and the corresponding cloud disk will be automatically mounted when you start your Linux instance.

### Will data be lost during disk unmounting?
Data in cloud disks will not be modified during mounting or unmounting. To ensure data consistency, we strongly recommend that you follow the steps below: 
- In Linux, log in to the CVM instance and run the `umount` command on the cloud disk. After the command is successfully executed, go to the console to unmount the disk.
- In Windows, stop read and write operations on all file systems on the disk before unmounting. Otherwise, data that has not been read or written will be lost. 

### How do I unmount elastic cloud disks?
For more information, see [Unmounting cloud disks](https://intl.cloud.tencent.com/document/product/362/32400).

### What happens to the system after the cloud disk expires?
The following instructions are only applicable for elastic cloud disks that support unmounting. Non-elastic cloud disks that do not support unmounting have the same lifecycles as CVMs. For more information, see [CVM arrears description](https://intl.cloud.tencent.com/document/product/213/2181).
- Pay-as-you-go cloud disks:
 - You can continue to use your Pay-as-You-Go cloud disk for 2 hours from the moment your account becomes negative. We will also continue to bill you for this period. When your account is in arrears for 2 hours, the service will automatically shut down. You cloud disk will not be available and can only store data. We will also stop billing you for service.
 - If your Tencent Cloud account is topped up to a positive balance within 24 hours after automatic shutdown, the cloud disk will be restored and billing continues.
 - If your account remains negative for 26 hours after shutdown, the Pay-as-You-Go disk will be repossessed, and all data will be deleted and **cannot be recovered**. We will notify the Tencent Cloud account creator and all the collaborators via email, SMS and the Message Center when the cloud disk is repossessed.

If you need more detailed information, call 95716.

### Can I change cloud disk type after a successful purchase?
Currently, switching types of cloud disks is not supported. You can create a snapshot for backup and then use the snapshot to create a cloud disk of your needed type.

### Can I adjust cloud disk capacity after a successful purchase?
Yes. Cloud disks support capacity adjustment. You can [expand the capacity of cloud disks](https://intl.cloud.tencent.com/document/product/362/31600?from_cn_redirect=1), but you cannot reduce capacity.

### What are the conditions for extending the file system?
Only cloud disks support expansion. Local disks cannot be expanded. For more information, see [Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).
>
> - We strongly recommend that you create a snapshot before expansion to ensure data security.
> - If the maximum capacity of the cloud disk still does not meet your business needs, you can [build RAID 1 using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2932) or [build LVM logical volumes using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).
> - Disks in MBR format support a maximum capacity of 2 TB. If your disk is in MBR format and needs to be expand to more than 2 TB, we recommend that you create and mount a new data disk, select the GPT partition style, and copy the data from the MBR disk to the new disk.

### How do I expand cloud disks?
For more information about expansion operations, see [Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).

### Why does my capacity seem unchanged after I expanded my data disk?
When you expanded your capacity successfully through the console, only the storage capacity of your data disk is increased. You also need to log in to your CVM and expand the partitions and file systems. For more information, see:
 [Expanding partitions and file systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)
 [Expanding partitions and file systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)


### Do CVMs support CPU/memory expansion? 
If the system disk is a cloud disk, the CVM supports CPU and memory adjustments.

### What should I do if the cloud disk is partitioned in MBR format and cannot be expanded?
Disks in MBR format support a maximum capacity of 2 TB. If your disk is in MBR format and needs to be expand to more than 2 TB, we recommend that you create and mount a new data disk, select the GPT partition style, and copy the data from the MBR disk to the new disk.

### What should I do if the cloud disk has already been expanded to maximum capacity, but still cannot meet business requirements?
We recommend you [build RAID using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2932) or [build LVM logical volumes using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).

### How do I build a RAID group using multiple elastic cloud disks?
For more information, see [Building RAID groups using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2932).

### How do I build LVM logical volumes using multiple elastic cloud disks?
For more information, see [Building LVM logical volumes using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).

### What happens to the data when a CVM is terminated?
- The lifecycle of a system disk completely follows that of a CVM. When the CVM is terminated, the data stored in the system disk will also be terminated.
- The lifecycle of a data disk (that is, an elastic cloud disk) is independent from that of a CVM. You can choose whether to retain the elastic cloud disk and its data outside of the CVM lifecycle.

Therefore, we recommend that you use elastic cloud disks to store data that needs to be saved for a long term.
### How can cloud disks be recovered after formatting?
After formatting, cloud disks cannot be recovered. We recommend you [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) before formatting.

### How do I delete cloud disks?
- The lifecycle of a system disk follows that of the CVM. It can only be deleted when the [CVM instance is terminated](https://intl.cloud.tencent.com/document/product/213/4930).
- Lifecycle of a data disk (that is, elastic cloud disk) is independent from that of the CVM. It can be deleted separately. For more information, see [Terminating cloud disks](https://intl.cloud.tencent.com/document/product/362/32399).

### Can my system disk be partitioned?
The system disk cannot be partitioned.
