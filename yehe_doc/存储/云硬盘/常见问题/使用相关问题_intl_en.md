### In what scenarios are cloud disks used?
- After you purchased a CVM, and later find its disk space was insufficient, you can [purchase](https://intl.cloud.tencent.com/document/product/362/5744) and [mount](https://intl.cloud.tencent.com/document/product/362/32401) elastic cloud disks to be used as data disks, satisfying storage requirements.
- After you purchased a CVM without additional data disks, you can purchase and mount elastic cloud disks to be used as data disks when you have the storage requirements.
- CVM A has 10 GB of important data stored on an elastic cloud disk, and you need to share the data with CVM B. You can directly [unmount](https://intl.cloud.tencent.com/document/product/362/32400) the disk from CVM A, and then [mount](https://intl.cloud.tencent.com/document/product/362/32401) it to CVM B.
- If a single maximum-sized cloud disk cannot meet your storage requirements, you can purchase multiple cloud disks with equal capacity and configure LVM logical volumes to provide a larger disk capacity.
- When I/O performance of a single disk cannot meet business requirements, you can purchase multiple cloud disks and configure RAID 0, RIAD 10, etc., to enhance I/O performance.

For more information, see [Use Cases](https://intl.cloud.tencent.com/document/product/362/3065).

### How do I select a cloud disk?
Before you select a disk type, determine the use cases.
- For general use cases including Web/APP applications, logical processing, and small and medium sites, we recommend that you select Premium Cloud Storage for a higher cost efficiency.
- For use cases including medium databases and image processing, we recommend that you select SSD for a better performance.
- For use cases with high requirements for workloads and performance, including large databases, video business, NoSQL, and Elasticsearch, we recommend that you select Enhanced SSD for an optimal performance and minimum storage latency.


### What should I notice when using a cloud disk?
- For an independently purchased cloud disk, when configuring the `fstab` static file system information, use the UUID or label of the file system as the file system ID, so that the device name remains unchanged on the CVM when any cloud disk is unmounted and then remounted. 
- If the cloud disk expires before the CVM, it will be restricted, unmounted, or even repossessed within a certain period. To prevent business interruption, please pay attention to the expiration date of the cloud disk and renew it promptly.
- If unmounting a cloud disk from your CVM will not severely impact your core business, you can consider using the `nofail` option when configuring `fstab`. This prevents the CVM from reporting an error when it restarts after the cloud disk is unmounted.
- We recommend that you run `san policy=OnlineAll` in `diskpart` before using the cloud disk in Windows.
- When unmounting a cloud disk from Windows, we recommend that you first interrupt all read/write operations on the disk, and perform the `offline` operation.

### If a custom image and a data disk snapshot is used, how do I automatically mount the data disk when starting a new instance?
For more information, see the “Automatic Mounting” section in [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

### How do I purchase a cloud disk?
You can create cloud disks via the console or an API. For more information, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744).

### How do I view cloud disk details?
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs/index).
2. At the top of the **Cloud Block Storage** page, select the region where the disk you want to view resides.
3. Locate the disk in the list, and view its information, as shown below:
You may click the ID/Name of the disk to enter its details page for more information.

### How do I view the cloud disk usage on the console?

The Cloud Monitor feature is automatically enabled once a CVM instance is created. You can view the usage of an initialized cloud disk that is mounted to CVMs by following the steps below:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index) and access the **Instances** page.
2. Select the ID/Name of the target instance to access the details page.
3. Select the **Monitoring** tab to view the instance disk usage, as shown below:

### What are the most common cloud disk operations?
For more information, see [Operation Overview](https://intl.cloud.tencent.com/document/product/362/33140).


### Why can’t I locate the CVM to which I want to mount a cloud disk?
Cloud disks cannot be mounted across availability zones. Make sure that the CVM instance has not been released and ensure that it is in the same region and availability zone as the cloud disk is in.

### Why am I unable to view the new cloud disk capacity that I mounted to a CVM instance?
Some Linux CVMs may not recognize an elastic cloud disk. You must first enable the disk hot swapping function in the CVM. For more information, see [Enabling the disk hot swapping function](https://intl.cloud.tencent.com/document/product/362/32401#modprobeacpiphp).

After manually mounting a cloud disk, you must select and perform the subsequent operations to make it usable.
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
	<td><ul class="params"><li>Mounting to a Windows CVM: after logging in to the instance, make the disk online through **Server Management** > **Storage** > **Disk Management**.</li>
		<li>Mounting to a Linux CVM: after logging in to the instance, run the <code>mount <disk partition> <mount point></code> command, such as <code>mount /dev/vdb /mnt</code>.</li>
		</ul>
	</li></td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">Snapshot capacity < Cloud disk capacity ≤ 2 TB <br/>or<br/>2 TB < Snapshot capacity < Cloud disk capacity</td>
<td><ul class="params"><li>Mounting to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601">extending partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31602">extending partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 <tr>
 <td>Snapshot capacity ≤ 2 TB < Cloud disk capacity</td>
<td nowrap="nowrap"><ul class="params"><li>If the snapshot uses the MBR partition format:</li>see <a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing Cloud Disks (Larger than 2TB)</a> to use the GPT partition instead.<b>This operation will delete the original data.</b><li>If the snapshot uses the GPT partition format:<ul><li>Mounting to a Windows CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31601">extending partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31602">extending partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 </table>

 <style>
	.params{margin-bottom:0px !important;}
</style>


### How do I partition and format a cloud disks mounted?
For more information, see [Initializing Cloud Disks (Smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) or [Initializing Cloud Disks (Larger than 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### What is the relationship between data writing and partition formatting?
A new data disk or data disk partition cannot be used until being formatted and recording the data structure. Formatting the disk is to establish a file system on and writes data to the data disk. The write-in data size varies by the file systems:
- For Windows:
   - Quick formatting: assigns the file system only to partitions and rewrites the directory table with little use of your disk capacity.
   - Normal formatting: in addition to the quick formatting tasks, it scans the partitions sector by sector to identify and mark bad sectors, and fills empty blocks in the cloud disk. In this case, it writes data to the entire disk. The capacity of the first snapshot approximates to that of the cloud disk.
- For Linux: after the cloud disk is formatted and before data are written to the instance, the capacity of the first snapshot depends on the format of the disk file system.

### After expanding my cloud disk, do I need to unmount existing partitions when creating a new independent partition on Linux? 
Yes. To do this, please follow the steps below:
1. Run the following command to unmount the data disk.
```
umount <Mount point>
```
If the mount point is `/data`, then run the following command:
```
umount /data
```
2. Unmount the file systems from all partitions on the cloud disk, and perform the subsequent operations. You can run the following command again to confirm that the unmounting operation is successful.
```
mount | grep '<Disk path>'
```
If it returns null, all file systems have been unmounted from partitions on the cloud disk.


### Can one cloud disk be accessed by CVMs?
No. You can mount up to 20 cloud disks to the same CVM, but you cannot mount the same cloud disk to multiple CVMs. You can only share data by [unmounting the data disk](https://intl.cloud.tencent.com/document/product/362/32400) from CVM A and then [mounting](https://intl.cloud.tencent.com/document/product/362/32401) it to CVM B.

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

### Can I change a CVM system disk from a local disk to a cloud disk?
Yes. To do this, follow the steps below:
>!Refer to [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) and [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942) to back up data before performing operations to ensure data security.
>

1. Log in to the [CVM console](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fcvm) and access the **Instances** page.
2. Locate the instance of which you want to change the disk, select **More** > **Instance Status** > **Shutdown** under the **Operation** column to shut down the selected instance.
3. After the instance is shut down, select **More** > **Resource Adjustment** > **Change Disk Media Type**.
4. In the pop-up window, select a target cloud disk type, check **I have read and agreed to Rules for Changing Disk Media Type**, and click **Change Now**.
5. Double-check the information, make a payment if applicable, and wait for the process to complete.
For more information about how to change the disk media type, see [Change Disk Media Type](https://intl.cloud.tencent.com/document/product/213/32365).


### Can I unmount the data disk that I purchased along with a CVM?
Since November 2017, data disks purchased with CVMs support unmounting from and remounting to CVMs. To avoid lifecycle management difficulties when data disks are unmounted from and remounted to another CVM with a different expiry time, we provide various options such as collective expiry time and auto-renewal configuration. We recommend you carefully select the appropriate lifecycle management method, to avoid data loss caused by disk expiration.

### Why is the separate cloud disk I created released together with my instance?
When mounting a cloud disk, you can decide if it should be released with the instance automatically. This can be configured via the [CBS console](https://console.cloud.tencent.com/cvm/cbs/index) or [ModifyDiskAttributes](https://intl.cloud.tencent.com/document/product/362/15659) API.


### What should I do if I lost my data after restarting my Linux instance?
If you lost all data in a directory (such as /data) after the restart, and you know the reason is that you didn’t mount data disk partitions, follow the steps below:
1. Run the `fdisk -l` command to view the unmounted partitions.
2. Run the `mount /dev/vdb /data` command to mount partitions.
3. Run the `df -h` command to see if they are mounted successfully.
4. Complete your [automatic mounting](https://intl.cloud.tencent.com/document/product/362/32401#.E6.8C.82.E8.BD.BD.E6.95.B0.E6.8D.AE.E7.9B.98.EF.BC.88linux.EF.BC.89) configurations. Then cloud disk will be automatically mounted when you start the Linux instance.

### When I unmount a cloud disk, will its data be lost?
Data in cloud disks will not be modified during mounting or unmounting. To ensure data consistency, we strongly recommend that you follow the steps below: 
- In Linux, log in to the CVM instance and run the `umount` command on the cloud disk. After the command is executed, log in to the CVM console to unmount the cloud disk.
- In Windows, stop all read and write operations on all file systems of the cloud disk before unmounting. Otherwise, the data that has not finished being read or written will be lost. 

### How do I unmount an elastic cloud disk?
For more information, see [Unmounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32400).

### What happens to the system after my cloud disk expires?
The following instructions are only applicable for elastic cloud disks that support unmounting. A non-elastic cloud disk that does not support unmounting has the same lifecycle as CVMs. For more information, see [Arrears](https://intl.cloud.tencent.com/document/product/213/2181).
- Pay-as-you-go cloud disks:
    - You can continue to use the pay-as-you-go cloud disk for 2 hours from the moment your account balance becomes negative. You will be billed for this period. After 2 hours, its services will be suspended (cloud disk is unavailable and can only store data). You will still be billed according to the billing standard (even if the account balance is negative) until data is completely erased.
    - If your Tencent Cloud account is topped up to a positive balance within 15 days after the cloud disk has its services suspended, the disk can be restored.
    - If the balance is less than 0 for 15 days after the cloud disk has its services suspended, the pay-as-you-go disk will be repossessed. All data will be erased and **cannot be recovered**. When your cloud disk is repossessed, Tencent Cloud account creator and all collaborators will be notified via email, SMS, and the console Message Center.

### Can I change the cloud disk type after a successful purchase?
No. However, you can create a snapshot for data backup and then use the snapshot to create a cloud disk of your needed type.

### Can I adjust cloud disk capacity after a successful purchase?
Yes. Cloud disks support capacity adjustment. You can [expand the capacity of cloud disks](https://intl.cloud.tencent.com/document/product/362/31600), but you cannot reduce the capacity.

### Do I have to shut down the CVM instance before an expansion operation? 
No. Please note that you need to assign its expanded capacity to an existing partition, or format it into an independent new partition. Depending on the operating system of the CVM, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

### What are the requirements for extending the file system?
Only cloud disks support expansion. Local disks cannot be expanded. For more information, see [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).
>!
> - We strongly recommend that you create a snapshot before expansion to ensure data security.
> - If the maximum capacity of the cloud disk still cannot meet your business needs, please try [building up RAID groups](https://intl.cloud.tencent.com/document/product/362/2932) or [building LVM logical volumes with multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).
> - MBR partition supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you create and mount a new data disk and use the GPT partition format to copy data.

### How do I expand a cloud disk?
For more information about expansion operations, see [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).

### Why does the capacity seem unchanged after I expanded my data disk?
The expansion on the console only increases the storage capacity of the data disk. You also need to log in to your CVM instance and extend the partitions and file systems. For more information, see:
 - [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)
 - [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)


### Do CVMs support CPU/memory expansion? 
If the system disk of the CVM is a cloud disk, you can adjust its CPU and memory.

### What should I do if the cloud disk is partitioned in MBR format and cannot be expanded?
MBR partition supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you create and mount a new data disk and use the GPT partition format to copy data.

### What should I do if a cloud disk has already been expanded to its maximum capacity, but still cannot meet my business requirements?
We recommend you [build up RAID groups](https://intl.cloud.tencent.com/document/product/362/2932) or [build LVM logical volumes with multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).

### How do I build up a RAID group by using multiple elastic cloud disks?
For more information, see [Building Up RAID Groups](https://intl.cloud.tencent.com/document/product/362/2932).

### How do I build LVM logical volumes by using multiple elastic cloud disks?
For more information, see [Building LVM Logic Volumes with Multiple Elastic Cloud Disks](https://intl.cloud.tencent.com/document/product/362/2933).

### How do I export the data from a cloud disk?
You can use FTP to upload and download data. For more information, see [Building the FTP Service (Windows)](https://intl.cloud.tencent.com/document/product/213/10414) and [Building the FTP Service (Linux)](https://intl.cloud.tencent.com/document/product/213/10912).

### What happens to the data when a CVM is terminated?
- The lifecycle of a system disk is the same as that of the CVM. When the CVM is terminated, the data stored in the system disk will also be terminated.
- The lifecycle of a data disk (that is, an elastic cloud disk) is independent from that of a CVM. You can decide if an elastic cloud disk and its data will be retained after a CVM expires.

Therefore, we recommend that you use elastic cloud disks to store data that needs to be saved for a long term.
### How can cloud disks be recovered after being formatted?
Cloud disks cannot be recovered after being formatted. We recommend that you [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) before formatting.

### How do I delete a cloud disk?
- The lifecycle of a system disk is the same as the CVM. It can only be deleted when the [CVM instance is terminated](https://intl.cloud.tencent.com/document/product/213/4930).
- The lifecycle of a data disk (that is, an elastic cloud disk) is independent from that of the CVM. It can be deleted separately. For more information, see [Terminating cloud disks](https://intl.cloud.tencent.com/document/product/362/32399).

### Can my system disk be partitioned?
No.


### How do I update the mounting information at the mount point?
LinuxOS supports the `systemd mount` command which will generate a mounting configuration file, and the existing .mount file still remains, the mounting to the same directory `/run/systemd/generator/` therefore will be affected.
#### Issue
Assume you have mounted the data disk vdb to the directory `/opt/apps` (run the `mount -a` command on the fstab file based on disk uuid). Now, you want to mount a new data disk vdc to the same directory and replace the old one. If you directly mount vdc to the directory, its data cannot be read.
#### Solution
1. Delete the configuration of the corresponding mount point (for example, run the `rm /run/systemd/generator/opt-apps.mount` command).
2. Run the `reload` command (for example, use `systemctl daemon-reload`).
3. Mount the data disk (for example, run the `mount /dev/vdc /opt/apps` command).


