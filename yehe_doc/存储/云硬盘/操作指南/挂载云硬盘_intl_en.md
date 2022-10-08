## Overview
You can attach elastic cloud disks to a CVM instance in the same availability zone as a data disk. Up to 20 data disks can be attached to a CVM instance.

This document describes how to attach cloud disks to a CVM instance in the console and by using an API.

<dx-alert infotype="explain" title="">
Some Linux CVMs may not recognize an elastic cloud disk. You must first enable the disk hot swapping feature in the CVM. For more information, see [Enabling the disk hot swapping feature](#modprobeacpiphp).
</dx-alert>


## Directions

### Attaching cloud disks in the CBS console
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. On the cloud disk list page, select and attach the cloud disks. Note that you can only attach cloud disks in **To be attached** status.
 - **Attach a single cloud disk**: Find the target cloud disk, and click **More** > **Attach** under the **Operation** column.
 - **Attach multiple cloud disks**: Select the cloud disks, and click **Attach** above the cloud disk list to attach them in a batch.
3. In the **Attach to instance** pop-up window, attach the disks to the instance.

Select the target instance, and complete the parameters **Attaching options**.
 - Unified expiry time with the instance (XXX)
 - Enable monthly auto-renewal of the cloud disks **(recommended)**
 - Attach directly
4. Click **Next**.
After attaching the cloud disk, you need to log in to the instance and initialize the disk.
5. Click **Attach now**.
If the status of the cloud disk changes to **Attached**, the attachment is successful.
6. Perform the subsequent operations corresponding to different cloud disk capacities.
<table>
  <tr>
	<th>Creation mode</th>
	<th>Cloud disk capacity</th>
	<th>Subsequent operations</th>
  </tr>
  <tr>
	<td rowspan="2">Manually created</td>
	<td>Cloud disk capacity < 2 TB</td>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/362/31597">Initializing cloud disks (<2 TB)</a>
	</td>
  </tr>
  <tr>
	<td>Cloud disk capacity ≥ 2 TB</td>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (≥2 TB)</a>
	</td>
  </tr>
  <tr>
	<td rowspan="3">Created from a snapshot</td>
	<td>Cloud disk capacity = Snapshot capacity</td>
	<td>
	  <ul>
		<li>Attach to Windows CVMs
		Log in to the instance, and go to <b>Server Manager</b> <b>Storage</b> <b>Disk Management</b> to make the disk online.</li>
		<li>Attach to Linux CVMs: Log in to the instance, and run 
		the command <code>mount <disk partition> <mount point></code>, such as 
		<code>mount /dev/vdb /mnt</code>, to make the disk usable.</li>
	  </ul>
	</td>
  </tr>
  <tr>
	<td nowrap="nowrap">Snapshot capacity < Cloud disk capacity ≤ 2 TB
	<br />or
	<br />2 TB < Snapshot capacity < Cloud disk capacity
	<td>
	  <ul>
		<li>Attach to Windows CVMs:
		<a href="https://intl.cloud.tencent.com/document/product/362/31601">[Extending Partitions and File Systems (Windows)]</a></li>
		<li>Attach to Linux CVMs:
		<a href="https://intl.cloud.tencent.com/document/product/362/39995">[Extending Partitions and File Systems (Linux)]</a></li>
	  </ul>
	</td>
  </tr>
  <tr>
	<td>Snapshot capacity ≤ 2 TB < Cloud disk capacity</td>
	<td nowrap="nowrap">
	  <ul>
		<li>If the snapshot uses a MBR partition,</li>
		<li style="list-style: none">see 
		<a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (≥2 TB)</a> to repartition the disk with GPT.
		<b>Note that this operation will delete the existing data</b></li>
		<li>If the snapshot uses a GPT partition,
		<ul>
		  <li>Attach to Windows CVMs:
		  <a href="https://intl.cloud.tencent.com/document/product/362/31601">[Extending Partitions and File Systems (Windows)]</a></li>
		  <li>Attach to Linux CVMs:
		  <a href="https://intl.cloud.tencent.com/document/product/362/39995">[Extending Partitions and File Systems (Linux)]</a></li>
		</ul></li>
	  </ul>
	</td>
  </tr>
</table>



### Using the API to attach cloud disks
You can use the `AttachDisks` API to attach cloud disks. For more information, see [AttachDisks](https://intl.cloud.tencent.com/document/product/362/16313).



## Related Operations
### Enabling the disk hot swapping feature[](id:modprobeacpiphp)

All existing images already support attaching and detaching elastic cloud disks. **To detach a cloud disk, you must first run the `umount` command in Linux CVM or perform offline operations in Windows CVM. Otherwise, the reattached elastic cloud disk may not be recognized.**


<dx-alert infotype="explain" title="">
Hot swapping is only recommended for CVMs with the following operating systems.
</dx-alert>

<table>
<tbody>
<tr><th width="50%">Operating system</th><th>Version</th>
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

1. [Log in to the Linux instance using Web Shell](https://intl.cloud.tencent.com/document/product/213/5436) as the root user.
2. Run the following command to add the driver.
```
modprobe acpiphp
```
<dx-alert infotype="explain" title="">
If you still need to load the `acpiphp` module after shutting down or re-starting the CVM, we recommend you run [Step 3](#step3) to set the `acpiphp` module to autoload.
</dx-alert>
3. [](id:step3)(Optional) If you need to load the `acpiphp` module automatically after shutting down or re-starting the CVM, run the following command according to the operating system.
<dx-tabs>
::: CentOS 5 Series
 1. Run the following command to create and open the `acpiphp.modules` file.
```
vi /etc/sysconfig/modules/acpiphp.modules
```
 2. Add the following content to the file, and save it.
```
 #!/bin/bash
 modprobe acpiphp >& /dev/null
```
3. Run the following command to grant execute permissions on the file.
```
chmod a+x /etc/sysconfig/modules/acpiphp.modules
```
:::
::: Debian 6 Series, Ubuntu 10.04 Series
 1. Run the following command to modify the file.
```
vi /etc/modules
```
 2. Add the following content to the file, and save it.
```
acpiphp
```

:::
::: openSUSE 12.3 Series
 1. Run the following command to modify the file.
```
vi /etc/sysconfig/kernel
```
 2. Add the following content to the file, and save it.
```
MODULES_LOADED_ON_BOOT="acpiphp"
```
:::
</dx-tabs>


### Attaching data disks automatically upon instance creation[](id:automatically)

If you specify a custom image and data disk snapshot while creating a CVM instance, the cloud disk created at the same time is automatically attached to the CVM and can be read and written without being initialized by partitioning, formatting and other operations. However, the specified custom images and data disk snapshots must meet the following requirements.


<dx-tabs>
::: Windows instances
If you use a custom image to create a Windows CVM instance, the cloud disk created from the corresponding data disk snapshot will be automatically attached. The custom image and the data disk snapshot must meet the following requirements:
- The data disk **must** be formatted to `ntfs` or `fat32` before you create a snapshot.
- The SAN policy in the custom image is `onlineAll`.

#### Checking configurations
Tencent Cloud provides pre-configured public images for Windows by default, but we still recommend that you perform the following steps to check configurations before creating a custom image. Run the following commands in order and check the returned results.
```
diskpart
```
```
san
```
See below:
<img src="https://main.qcloudimg.com/raw/edac7337395de380c0ec801646e0a627.png" width="60%">

:::
::: Linux instances
If you use a custom image to create a Linux CVM instance, the cloud disk created from the corresponding data disk snapshot will be automatically attached. The custom image and the data disk snapshot must meet the following requirements:
- The data disk **must** be formatted and attached to the source CVM.
- Add the following commands to the `/etc/rc.local` file to configure the mount point of the data disk before creating a system disk on the system disk.
```
mkdir -p <mount-point>
mount <device-id> <mount-point>
```
<dx-alert infotype="explain" title="">
- Replace `<mount-point>` with the mount point of the file system, such as `/mydata`.
- Replace `<device-id>` with the partition path of the file system. For example, enter `/dev/vdb` if the file system has no partition, and `/dev/vdb1` if the file system has partitions.
</dx-alert>

:::
</dx-tabs>

