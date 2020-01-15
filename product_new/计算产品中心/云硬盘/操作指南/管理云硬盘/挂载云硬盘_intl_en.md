You can mount an elastic cloud disk (used as a data disk for the CVM) to any CVM in the same availability zone. Each CVM can have up to 20 data disks mounted to it. You can use the following methods to mount a cloud disk.
- When launching a new CVM, specify the corresponding custom image and data disk snapshot.
After automatic mounting, reads and writes on the data disk can be directly performed without disk initialization operations such as partitioning and formatting. 
- For an independently purchased cloud disk, the elastic cloud disk can be manually mounted to an existing CVM instance in the same availability zone through the console or API.
 - Directly created cloud disks
 After manual mounting, you need to perform initialization operations on the disk such as partitioning and formatting. For more information, see [Initializing cloud disks (smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) or [Initializing cloud disks (larger than or equal to 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).
 - Creating a cloud disk from a snapshot
    If the capacity of the cloud disk is equal to the capacity of the snapshot, reads and writes on the data disk can be directly performed without disk initialization operations such as partitioning and formatting.
	If the capacity of the cloud disk is larger than the snapshot capacity, you need to extend the file system or convert the partition format.

 > Some Linux CVMs may not recognize elastic cloud disks. You can first enable the disk hot swapping function on the CVM. For details, see [Enable disk hot swapping function](#modprobeacpiphp).

## Automatic Mounting
### Mounting data disks (Windows)
If you need to automatically mount a cloud disk created from a corresponding data disk snapshot when starting a Windows CVM instance, the specified custom image and data disk snapshot must meet the following requirements:
- The data disk **must** be formatted as `ntfs` or `fat32` before you create a snapshot.
- The SAN policy in the custom image is `onlineAll`.
 >Public images for Windows that are currently provided by Tencent Cloud have been configured by default, but we still recommend that you check the configuration before creating any custom images by following the steps below:
 ![](https://main.qcloudimg.com/raw/edac7337395de380c0ec801646e0a627.png)


### Mounting data disks (Linux)
If you need to automatically mount a cloud disk created from a corresponding data disk snapshot when starting a Linux CVM instance, the specified custom image and data disk snapshot must meet the following requirements:
- The data disk **must** be formatted before the snapshot is created. That is, the data disk has been successfully mounted to the original CVM.
- For the system disk to create a custom image, you need to add the following commands to the file `/etc/rc.local` to write the data disk mounting point to the file.
 ```
 mkdir -p <mount-point>
 mount <device-id> <mount-point>
 ```
 The parameter descriptions for these commands are as follows:
 - `<mount-point>` must be set to the mounting point of the file system, such as `/mydata`.
 - `<device-id>` must be set to the actual file partition location. For example, enter `/dev/vdb` when there is no partition in the file system, and `/dev/vdb1` when there is a partition in the file system.

## Mounting Manually

### Using the console to mount cloud disks
1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. On the cloud disk list page, you can mount cloud disks using the following methods:
 a. Click **More**>**Mount** in the row of the cloud disk with the status **To Be Mounted**.
 b. Select the cloud disks with the status **To Be Mounted**, and click **Mount** at the top of the cloud disk list to perform batch mounting.
3. In the pop-up box, click **OK**.
4. Refresh the cloud disk list.
 If the status of the cloud disk changes to **Mounted**, this indicates that mounting is successful.
5. Depending on the cloud disks, you need to choose to perform the corresponding subsequent operations to make the cloud disk available.
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
 <td nowrap="nowrap">Snapshot capacity < cloud disk capacity ≤ 2TB <br/>or<br/>2TB < snapshot capacity < cloud disk capacity</td>
<td><ul><li>Mounting to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601"> Expanding partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31602">Expanding partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 <tr>
 <td>Snapshot capacity ≤ 2TB < cloud disk capacity</td>
<td nowrap="nowrap"><ul><li>If MBR partition format is used in the snapshot: </li>Refer to <a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2TB)</a>Using GPT to re-partition:<b>This operation will delete the original data</b><li>If GPT partition format is used in the snapshot: <ul><li>Mounting to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601">Expanding partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31602">Expanding partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 </table>

### Using the API to mount cloud disks
You can use the AttachDisks API to mount a cloud disk. For more information, see [Mounting cloud disks](https://intl.cloud.tencent.com/document/product/362/16313).

<span id="modprobeacpiphp"></span>

### Enabling the disk hot swapping function
All images that are currently provided already support the mounting and unmounting operations of elastic cloud disks. **To unmount a cloud disk, you must first execute the `umount` (Linux) or offline (Windows) operations. Otherwise, the CVM may not recognize the elastic cloud disk next time it is mounted.**
However, if you have previously purchased a CVM with one of the following operating systems and plan to mount it with elastic cloud disks, we recommend that you first add the related driver to the CVM to get the hot swapping function:
<table>
<tbody>
<tr><th>CVM operating system types</th><th>Version</th>
<tr><td rowspan="4">CentOS</td><td>5.11 64-bit</td>
<tr><td>5.11 32-bit</td>
<tr><td>5.8 64-bit</td>
<tr><td>5.8 32-bit</td>
<tr><td >Debian</td><td>6.0.3 32-bit</td>
<tr><td rowspan="2">Ubuntu</td><td>10.04 64-bit</td>
<tr><td>10.04 32-bit</td>
<tr><td rowspan="2">openSUSE</td><td>12.3 64-bit</td>
<tr><td>12.3 32-bit</td>
</tbody>
</table>

1. As the root user, [Log In to the Linux CVM](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command to add the driver.
```
modprobe acpiphp
```
> If you need to load the `acpiphp` module when shutting down or re-starting the CVM, we recommend you execute [Step 3](#step3) to set the `acpiphp` module to load automatically when starting up.
<span id="step3"></span>
3. (Optional) According to the different operating systems, select the related operation method to set the `acpiphp` module to load automatically when starting up:
 - **CentOS 5 Series**
 a. Execute the following command to create and open an `acpiphp.modules`file.
```
vi /etc/sysconfig/modules/acpiphp.modules
```
b. Add the following content to the file, and save.
```
 #!/bin/bash
 modprobe acpiphp >& /dev/null
```
c. Execute the following command to add execution permissions.
```
chmod a+x /etc/sysconfig/modules/acpiphp.modules
```
 - **Debian 6 Series, Ubuntu 10.04 Series**
 a. Execute the following command to modify the file.
```
vi /etc/modules
```
b. Add the following content to the file, and save.
```
acpiphp
```
 - **openSUSE 12.3 Series**
 a. Execute the following command to modify the file.
```
vi /etc/sysconfig/kernel
```
b. Add the following content to the file, and save.
```
MODULES_LOADED_ON_BOOT="acpiphp"
```
