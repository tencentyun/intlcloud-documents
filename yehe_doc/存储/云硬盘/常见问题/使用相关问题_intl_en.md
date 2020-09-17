### In what scenarios are cloud disks used?
- After you purchased a CVM, and later find its disk space was insufficient, you can [purchase](https://intl.cloud.tencent.com/document/product/362/5744) and [mount](https://intl.cloud.tencent.com/document/product/362/32401) elastic cloud disks to be used as data disks, satisfying storage requirements.
- After you purchased a CVM without additional data disks, you can purchase and mount elastic cloud disks to be used as data disks when you have the storage requirements.
- CVM A has 10 GB of important data stored on an elastic cloud disk, and you need to share the data with CVM B. You can directly [unmount](https://intl.cloud.tencent.com/document/product/362/32400) the disk from CVM A, and then [mount](https://intl.cloud.tencent.com/document/product/362/32401) it to CVM B.
- When a single maximum size cloud disk cannot meet storage requirements, you can purchase multiple cloud disks with equal capacity and configure LVM logical volumes to provide a larger disk capacity.
- When I/O performance of a single disk cannot meet business requirements, you can purchase multiple cloud disks and configure RAID 0, RAID 10, etc., to enhance I/O performance.

For more information, see [Use Cases](https://intl.cloud.tencent.com/document/product/362/3065).

### How do I select a cloud disk?
Before you select a disk type, determine the use case:
- For general use cases including Web/APP applications, logical processing, and small and medium sites, we recommend that you select Premium Cloud Storage for a higher cost efficiency.
- For use cases including medium databases, and image processing, we recommend that you select SSD for a better performance.
- For use cases with high requirements for workloads and performance, including large databases, video business, NoSQL, and ElasticSearch, we recommend that you select Enhanced SSD for the optimal performance and minimum storage latency.

### What should I notice when using a cloud disk?
- For an independently purchased cloud disk, when configuring static file system information using `fstab`, use the UUID or label of the file system as the file system ID, so that the device name remains unchanged on the CVM when any cloud disk is unmounted and then remounted. 
- If the cloud disk expires before the CVM, it will be restricted, unmounted, or even repossessed within a certain period. To prevent business interruption, please pay attention to the expiration date of the cloud disk and renew it promptly.
- If unmounting the cloud disk from the CVM will not severely impact your core business, you can consider using the `nofail` option to configure`fstab`, so there will be no error when you restart the CVM after unmounting the cloud disk.
- We recommend that you run `san policy=OnlineAll` in `diskpart` before using the cloud disk in Windows.
- When unmounting a cloud disk from Windows, we recommend that you first interrupt all read/write operations on the disk, and perform the `offline` operation.

### How do I use a custom image and a data disk snapshot to automatically mount the data disk when launching new instances?
For more information, see the automatic mounting section in [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

### How do I purchase a cloud disk?
You can create cloud disks via the Console or API. For more information, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744).

### Where can I view cloud disk details?
1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs/index).
2. At the top of the **Cloud Block Storage** list page, select the region where the disk you want to view resides.
3. Locate the cloud disk in the list, and view its information, as shown below:
You may click the ID/Name of the disk to enter its details page for more information.

### How do I commonly operate on a cloud disk?
For more information, see [Operation Overview](https://intl.cloud.tencent.com/document/product/362/33140).


### Why can’t I locate the CVM to which I want to mount a cloud disk?
Cloud disks cannot be mounted across availability zones. Please ensure that the CVM instance and cloud disk are in the same availability zone of the same region. Please also ensure that the CVM has not been released.

### Why can’t I see the capacity of the new cloud disk on the CVM after mounting it to the CVM?
Some Linux CVMs may not recognize the elastic cloud disk. You must first enable the disk hot swapping function in the CVM. For more information, see [Enabling the disk hot swapping function](https://intl.cloud.tencent.com/document/product/362/32401#modprobeacpiphp).

After manually mounting a cloud disk, you must select and perform the subsequent operations to make it usable.
<table>
 <tr>
 <th>Creation mode</th>
 <th>Cloud disk capacity</th>
 <th>Subsequent operations</th>
 </tr>
 <tr>
 <td  rowspan="2">Create directly</td>
 <td>Cloud disk capacity < 2TB</td>
 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Initializing cloud disks (smaller than 2TB)</a></td>
 </tr>
 <tr>
  <td>Cloud disk capacity ≥ 2TB</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2TB)</a></td>
 </tr>
  <tr>
	<td  rowspan="3">Create from a snapshot</td>
	<td>Cloud disk capacity = Snapshot capacity</td>
	<td><ul class="params"><li>Mounting to a Windows CVM: After logging in to the instance, select **Server Management** -> **Storage** -> **Disk Management** to make the disk online.</li>
		<li>Mounting to a Linux CVM: After logging in to the instance, run the <code>mount <Disk partition> <Mount point></code> command, such as <code>mount /dev/vdb /mnt</code>.</li>
		</ul>
	</li></td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">Snapshot capacity < cloud disk capacity ≤ 2TB <br/>or<br/>2TB < snapshot capacity < cloud disk capacity</td>
<td><ul class="params"><li>Mounting to a Windows CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31601">Extending partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31602">Extending partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 <tr>
 <td>Snapshot capacity ≤ 2TB < cloud disk capacity</td>
<td nowrap="nowrap"><ul class="params"><li>If MBR partition format is used in the snapshot:</li>See<a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2TB)</a>Using GPT to re-partition:<b>This operation will erase the original data</b><li>If GPT partition format is used in the snapshot:<ul><li>Mounting to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601">Extending partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31602">Extending partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 </table>

 <style>
	.params{margin-bottom:0px !important;}
</style>


### How do I partition and format a cloud disk mounted?
For more information, see [Initializing Cloud Disks (Smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) or [Initializing Cloud Disks (Larger than 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### What is the relationship between data writing and partition formatting?
A new data disk or data disk partition cannot be used until being formatted and recording the data structure. Formatting the disk is to establish a file system on and writes data in the data disk. The write-in data size varies by the file systems:
- For Windows:
   - Quick formatting: assigns the file system only to partitions and rewrites the directory table with little use of your disk capacity.
   - Normal formatting: in addition to the quick formatting tasks, it scans the partitions sector by sector to identify and mark bad sectors, and fills empty blocks in the cloud disk. In this case, it writes data to the entire disk. The capacity of the first snapshot approximates to that of the cloud disk.
- For Linux: After the cloud disk is formatted and before data are written to the instance, the capacity of the first snapshot depends on the format of the disk file system.

### After expanding my cloud disk, do I need to unmount my partitions to create an independent one on the Linux CVM? 
Yes. To do this, follow the directions below:
1. Run the following command to unmount the data disk:
```
umount <Mount point>
```
If the mount point is `/data`, then run the following command:
```
umount /data
```
2. Unmount the file systems from all partitions on the cloud disk, and execute the subsequent operations. You can run the following command again to confirm that the unmounting is successful.
```
mount | grep '<Disk path>'
```
If it returns null, all file systems have been unmounted from partitions on the cloud disk.


### Can one cloud disk be accessed by CVMs?
No. You can mount up to 20 cloud disks to the same CVM, but you cannot mount the same cloud disk to multiple CVMs. You can only share data by [unmounting the cloud disk](https://intl.cloud.tencent.com/document/product/362/32400) from CVM A and then [mounting](https://intl.cloud.tencent.com/document/product/362/32401) it to CVM B.

### Several cloud disks of the same size and type are mounted on the same CVM. How do I distinguish them in the operating system?
- In Linux, you can view the relationship between the elastic cloud disks and the device name by running the following command:
```
ls -l /dev/disk/by-id
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

### Why is the separate cloud disk I created released along with my instance?
When mounting a cloud disk, you can configure whether it will be automatically released along with your instance. You can enable or disable this feature via the [CBS Console] (https://console.cloud.tencent.com/cvm/cbs/index) or the [ModifyDiskAttributes](https://intl.cloud.tencent.com/document/product/362/15659) API.


### What should I do if I lost my data after restarting a Linux instance?
If you lost all data in a directory (such as `/data`) after the restart, and you know the reason is that you didn’t mount data disk partitions, follow the step-by-step directions below:
1. Run `fdisk -l` to view the unmounted partitions.
2. Run `mount /dev/vdb /data` to mount partitions.
3. Run `df -h` to see if they are mounted successfully.
4. Complete your [automatic mounting](https://intl.cloud.tencent.com/document/product/362/32401#.E6.8C.82.E8.BD.BD.E6.95.B0.E6.8D.AE.E7.9B.98.EF.BC.88linux.EF.BC.89) configurations. The cloud disk will be automatically mounted when you launch the Linux instance.

### Will data be lost during disk unmounting?
No. Data in cloud disks will not be modified during mounting or unmounting. To ensure data consistency, we strongly recommend that you follow the steps below: 
- In Linux, log in to the CVM instance, run the `umount` command on the cloud disk, and then access the Console to unmount the disk.
- In Windows, stop all read and write operations on all file systems of the disk before unmounting it. Otherwise, the data that has not finished being read or written will be lost. 

### How do I unmount an elastic cloud disk?
For more information, see [Unmounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32400).

### What happens to the system after the cloud disk expires?
The following instructions are only applicable for elastic cloud disks that support unmounting. Non-elastic cloud disks that do not support unmounting have the same lifecycles as CVMs. For more information, see [Arrears](https://intl.cloud.tencent.com/document/product/213/2181).

Pay-as-you-go cloud disks:

 - You can continue to use the pay-as-you-go cloud disk for 2 hours from the moment your account becomes negative. You will be billed for this period. After 2 hours, the service will automatically shut down (cloud disk is unavailable and only data is retained) and billing continues until the data is completely erased, even though your account remains a negative balance.
 - If your Tencent Cloud account is topped up to a positive balance within 15 days after shutdown, the cloud disk will be restored.
 - If your account remains negative for 15 days after shutdown, your pay-as-you-go disk will be repossessed, and all data will be erased and **cannot be retrieved**. We will notify the Tencent Cloud account creator and all the collaborators via email, SMS, and the Message Center when the cloud disk is repossessed.


### Can I change the type of the cloud disk I have purchased?
No. To do this, you need to create a snapshot for backup and then use the snapshot to create a cloud disk of your needed type.

### Can I adjust the capacity of the cloud disk I have purchased?
Yes. Cloud disks support capacity adjustment. You can [expand the capacity] ](https://intl.cloud.tencent.com/document/product/362/31600), but cannot reduce the capacity of cloud disks.

### What are the requirements for extending the file system?
Only cloud disks support expansion. Local disks cannot be expanded. For more information, see [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).
>
>- We strongly recommend that you create a snapshot before expansion to ensure data security.
> - If the maximum capacity of the cloud disk still cannot meet your business needs, you can try [building up RAID groups using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2932) or [building LVM logical volumes using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).
> - Disks in MBR format support a maximum capacity of 2 TB. If your disk is in MBR format and you need to expand its capacity to more than 2 TB, we recommend that you create and mount a new data disk, and copy the data to the new disk using GPT partition format.

### How do I expand cloud disks?
For more information about expansion operations, see [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).

### Why does the capacity seem unchanged after I expanded my data disk?
When you expanded your capacity successfully through the Console, only the storage capacity of your data disk is increased. You also need to log in to your CVM and extend the partitions and file systems. For more information, see:
 [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)
 [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)


### Do CVMs support CPU/memory expansion? 
If the system disk of the CVM is a cloud disk, you can adjust its CPU and memory.

### What should I do if the cloud disk is partitioned in MBR format and cannot be expanded?
Disks in MBR format support a maximum capacity of 2 TB. If your disk is in MBR format and you need to expand its capacity to more than 2 TB, we recommend that you create and mount a new data disk, and copy the data to the new disk using GPT partition format.

### What should I do if the cloud disk has already been expanded to the maximum capacity, but still cannot meet business requirements?
We recommend you [build up RAID groups using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2932) or [build LVM logical volumes using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).

### How do I build up a RAID group using multiple elastic cloud disks?
For more information, see [Building up RAID Groups Using Multiple Elastic Cloud Disks](https://intl.cloud.tencent.com/document/product/362/2932).

### How do I build LVM logical volumes using multiple elastic cloud disks?
For more information, see [Building LVM Logical Volumes Using Multiple Elastic Cloud Disks](https://intl.cloud.tencent.com/document/product/362/2933).

### What happens to the data when a CVM is terminated?
- The lifecycle of a system disk is the same as that of a CVM. When the CVM is terminated, the data stored in the system disk will also be terminated.
- The lifecycle of a data disk (that is, an elastic cloud disk) is independent from that of a CVM. You can choose whether to survive the elastic cloud disk and its data upon the expiration of CVM.

Therefore, we recommend that you use elastic cloud disks to store data that needs to be saved for a long term.
### How can a cloud disk be restored after formatting?
After formatting, cloud disks cannot be restored. We recommend you [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) before formatting.

### How do I delete a cloud disk?
- The lifecycle of a system disk is the same as that of the CVM. It can only be deleted when the [CVM instance is terminated](https://intl.cloud.tencent.com/document/product/213/4930).
- The lifecycle of a data disk (that is, an elastic cloud disk) is independent from that of the CVM, which can be deleted separately. For more information, see [Terminating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32399).

### Can my system disk be partitioned?
No.
