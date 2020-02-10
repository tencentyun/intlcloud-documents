### What are some use cases for different cloud disks?
- After purchasing CVMs, you realize the disk space is insufficient. You can [purchase](https://intl.cloud.tencent.com/document/product/362/5744) and [mount](https://intl.cloud.tencent.com/document/product/362/32401) elastic cloud disks, which can be used as data disks and meet your storage requirements.
- When purchasing CVMs, you do not want to purchase additional data disks. When you have storage requirements, you can purchase an elastic cloud disk and mount it as a data disk.
- CVM A has 10 GB of important data stored on an elastic cloud disk, and you need to share the data with CVM B. You can directly [unmount](https://intl.cloud.tencent.com/document/product/362/32400) the disk from CVM A, and then [mount](https://intl.cloud.tencent.com/document/product/362/5745) it to CVM B.
- If a single maximum-sized cloud disk cannot meet your storage requirements, you can purchase multiple cloud disks with equal capacity and configure LVM logical volumes to provide a larger disk capacity.
- If the I/O performance of a single disk cannot meet business requirements, you can purchase multiple cloud disks and configure RAID 0, RAID 10, and so on to enhance the I/O performance.

For more information, see [Use Cases](https://intl.cloud.tencent.com/document/product/362/3065).

### How do I select cloud disk types?
Before you select a disk type, determine the usage scenario.
- For scenarios where requests are relatively infrequent, such as system logs, enterprise work files, data warehouses, small-sized blogs, and BBS, we recommend that you select HDD cloud disks to reduce costs.
- For general scenarios such as mid and small-sized databases, Web/App applications, and transactional workloads, we recommend that you select Premium Cloud Storage for higher cost efficiency.
- For scenarios with high workloads and relatively high performance requirements such as large-sized core databases, OLTP businesses, and NoSQL databases, we recommend that you select SSD cloud disks for better performance.

### What are the precautions for using cloud disks?
- For an independently purchased cloud disk, when you configure static file system information using `fstab`, the UUID or label of the file system should be used as the file system ID. This ensures that the cloud disk’s kernel name will not be modified when multiple cloud disks are mounted/unmounted on the same CVM.  
- If unmounting a cloud disk from your CVM will not severely impact your core business, you can consider using the `nofail` option when configuring `fstab`. This prevents the system from reporting an error when it restarts after the cloud disk is unmounted from the CVM.
- We recommend that you run `san policy=OnlineAll` in `diskpart` before using the cloud disk in Windows.
- When unmounting a cloud disk from Windows, we recommend that you first interrupt all read/write operations on the disk, and perform the `offline` operation.

### When using a custom image and a data disk snapshot, how do I implement automatic mounting when launching new instances?
See the "Automatic Mounting" section in [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

### How do I purchase cloud disks?
You can create cloud disks in the console or by calling an API. For more information, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744).

### Why can’t I find the CVM to which I want to mount a cloud disk?
Cloud disks cannot be mounted across availability zones. Please ensure that the CVM instance and cloud disk are in the same availability zone of the same region. Please also ensure that the CVM has not been released.

### Why can’t I see the new cloud disk capacity in the operating system of the CVM after mounting a cloud disk?
Some Linux CVMs may not recognize an elastic cloud disk. You must first enable the disk hot swapping function in the CVM. For more information, see [Enabling the Disk Hot Swapping Function](https://intl.cloud.tencent.com/document/product/362/32401#enabling-the-disk-hot-swapping-function).

After manually mounting a cloud disk, you must select and perform the subsequent operations to make the cloud disk usable.
<table>
 <tr>
 <th>Creation mode</th>
 <th>Cloud disk capacity</th>
 <th>Subsequent operations</th>
 </tr>
 <tr>
 <td  rowspan="2">Create directly</td>
 <td>Cloud disk capacity < 2 TB</td>
 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Initializing cloud disks (smaller than 2 TB)</a></td>
 </tr>
 <tr>
  <td>Cloud disk capacity ≥ 2 TB</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2 TB)</a></td>
 </tr>
  <tr>
	<td  rowspan="3">Create from a snapshot</td>
	<td>Cloud disk capacity = Snapshot capacity</td>
	<td>No subsequent operations are needed, and you can use the cloud disk directly after mounting it.</td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">Snapshot capacity < Cloud disk capacity ≤ 2 TB <br/>or<br/>2 TB < Snapshot capacity < Cloud disk capacity</td>
<td><ul><li>Mounting to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601"> Extending partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31602">Extending partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 <tr>
 <td>Snapshot capacity ≤ 2 TB < Cloud disk capacity</td>
<td nowrap="nowrap"><ul><li>If the MBR partition format is used in the snapshot: </li>see <a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2 TB)</a> Using GPT to re-partition: <b>this operation will delete the original data.</b><li>If the GPT partition format is used in the snapshot: <ul><li>Mounting to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601">Extending partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31602">Extending partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 </table>


### After mounting a cloud disk, how do I perform partitioning and formatting?
See [Initializing cloud disks (smaller than 2 TB)](https://intl.cloud.tencent.com/document/product/362/31597) or [Initializing cloud disks (larger than or equal to 2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### Can multiple CVMs access one cloud disk?
This is not supported currently. You can mount up to 20 cloud disks to the same CVM, but multiple CVMs cannot share the same cloud disk. You can only share data by [unmounting](https://intl.cloud.tencent.com/document/product/362/32400) from CVM A and then [mounting](https://intl.cloud.tencent.com/document/product/362/32401) to CVM B.

### When several cloud disks of the same size and type are mounted to the same CVM, how do I distinguish them in the operating system?
- In Linux, you can view the relationship between the elastic cloud disks and the device name by running the following command:
```
ls -l /dev/disk/by-id
```
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
- In Windows, you can view the relationship by running the following command:
```
wmic diskdrive get caption,deviceid,serialnumber
```
Or
```
wmic path win32_physicalmedia get SerialNumber,Tag
```
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)

### Can I unmount a data disk that I purchased along with a CVM?
From November 2017, the data disks purchased with a CVM can be unmounted and remounted.

### Will data be lost during cloud disk unmounting?
Data in cloud disks will not be modified during mounting or unmounting. To ensure data consistency, we strongly recommend that you follow the steps below: 
- In Linux, log in to the CVM instance and run the `umount` command on the cloud disk. After the command is successfully executed, go to the console to unmount the disk.
- In Windows, stop read and write operations on all file systems on the disk before unmounting. Otherwise, data that has not been read or written will be lost. 

### How do I unmount elastic cloud disks?
See [Unmounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32400).

### What happens to the system after my cloud disk expires?
The following instructions are only applicable for elastic cloud disks that support unmounting. Non-elastic cloud disks that do not support unmounting have the same lifecycles as CVMs. For more information, see [Arrears](https://intl.cloud.tencent.com/document/product/213/2181).

 - You can continue to use your pay-as-you-go cloud disk for 2 hours from the moment your account becomes negative. We will also continue to bill you for this period. When your account is in arrears for 2 hours, your cloud disk will automatically shut down. The cloud disk will be unavailable, but your data will be retained. We will also stop billing you for service.
 - If your Tencent Cloud account is topped up to a positive balance within 24 hours after automatic shutdown, the cloud disk will be restored and billing continues.
 - If your account remains negative for 26 hours after shutdown, your pay-as-you-go disk will be repossessed, and all data will be deleted and **cannot be recovered**. We will notify the Tencent Cloud account creator and all the collaborators via email, SMS, and the Message Center when the cloud disk is repossessed.

### Can I change the cloud disk type after a successful purchase?
Currently, switching types of cloud disks is not supported. You can create a snapshot for backup and then use the snapshot to create a cloud disk of your needed type.

### Can I adjust the cloud disk capacity after a successful purchase?
Yes. Cloud disks support capacity adjustment. Cloud disks can be [scaled up](https://intl.cloud.tencent.com/document/product/362/31600), but cannot be scaled down.

### What are the requirements for extending the file system?
Only cloud disks can be scaled up. Local disks cannot be scaled up. For more information, see [Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).
>
>- We strongly recommend that you create a snapshot before expansion to ensure data security.
> If the maximum capacity of a cloud disk cannot meet your business needs, you can try [Building Up RAID Groups](https://intl.cloud.tencent.com/document/product/362/2932) or [Building Up LVM Logic Volumes](https://intl.cloud.tencent.com/document/product/362/2933) by using multiple elastic cloud disks.
> - Disks in MBR format support a maximum capacity of 2 TB. If your disk is in MBR format and needs to be expand to more than 2 TB, we recommend that you create and mount a new data disk, select the GPT partition style, and copy the data from the MBR disk to the new disk.

### How do I expand cloud disks?
See [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600)

### Do CVMs support CPU/memory expansion? 
If the system disk is a cloud disk, the CVM supports CPU and memory adjustments.

### What should I do if the cloud disk is partitioned in MBR format and cannot be expanded?
Disks in MBR format support a maximum capacity of 2 TB. If your disk is in MBR format and needs to be expanded to more than 2 TB, we recommend that you create and mount a new data disk, select the GPT partition style, and copy the data from the MBR disk to the new disk.

### What should I do if the cloud disk has already been expanded to maximum capacity, but still cannot meet my business requirements?
You can try [Building Up RAID Groups](https://intl.cloud.tencent.com/document/product/362/2932) or [Building Up LVM Logic Volumes](https://intl.cloud.tencent.com/document/product/362/2933) by using multiple elastic cloud disks.

### How do I build a RAID group by using multiple elastic cloud disks?
See [Building Up RAID Groups](https://intl.cloud.tencent.com/document/product/362/2932).

### How do I build LVM logical volumes by using multiple elastic cloud disks?
See [Building Up LVM Logical Volumes](https://intl.cloud.tencent.com/document/product/362/2933).

### What happens to the data when a CVM is terminated?
- The lifecycle of a system disk completely follows that of a CVM. When the CVM is terminated, the data stored in the system disk will also be terminated.
- The lifecycle of a data disk (that is, an elastic cloud disk) is independent from that of a CVM. You can choose whether to retain the elastic cloud disk and its data outside of the CVM lifecycle.

Therefore, we recommend that you use elastic cloud disks to store data that needs to be saved for a long term.
### How can cloud disks be recovered after being formatted?
Cloud disks cannot be recovered after being formatted. We recommend that you [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) before formatting.

### How do I delete cloud disks?
- The lifecycle of a system disk follows that of the CVM. It can only be deleted when the [CVM instance is terminated](https://intl.cloud.tencent.com/document/product/213/4930).
- The lifecycle of a data disk (that is, an elastic cloud disk) is independent from that of the CVM. It can be deleted separately. For more information, see [Terminating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5752).

### Can my system disk be partitioned?
The system disk cannot be partitioned.
