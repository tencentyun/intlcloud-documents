You can use an elastic cloud disk as the data disk and mount it to any CVM in the same availability zone. Each CVM can have up to 20 data disks mounted to it. You can use the following methods to mount a cloud disk.
- When launching a new CVM, specify the corresponding custom image and data disk snapshot.
After automatic mounting, reads and writes on the data disk can be directly performed without disk initialization operations such as partitioning and formatting.
- When purchasing an elastic cloud disk, manually mount it to an existing CVM instance in the same availability zone via the console or an API.
 - Creating a cloud disk directly
 After manual mounting, you need to initialize the cloud disk by formatting and partitioning it. For more information, see [Initializing Cloud Disks (Smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) or [Initializing Cloud Disks (Larger than 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).
 - Creating a cloud disk from a snapshot
    If the cloud disk capacity is equal to the snapshot size, you can directly read and write on the cloud disk without disk initialization operations such as partitioning and formatting.
	If the cloud disk capacity is larger than the snapshot size, you need to extend the file system or convert the partition format.

 >?Some Linux CVMs may not recognize an elastic cloud disk. You must first enable the disk hot swapping feature in the CVM. For more information, see [Enabling the disk hot swapping feature](#modprobeacpiphp).

## Automatic Mounting
### Mounting data disks (Windows)
If you use a custom image to create a Windows CVM instance, the cloud disk created from the corresponding data disk snapshot will be automatically mounted. The custom image and the data disk snapshot must meet the following requirements:
- The data disk **must** be formatted to `ntfs` or `fat32` before you create a snapshot.
- The SAN policy in the custom image is `onlineAll`.
 >?Tencent Cloud provides pre-configured public images for Windows by default, but we still recommend that you perform the following steps to check configurations before creating a custom image.
![](https://main.qcloudimg.com/raw/edac7337395de380c0ec801646e0a627.png)


### Mounting data disks (Linux)
If you use a custom image to create a Linux CVM instance, the cloud disk created from the corresponding data disk snapshot will be automatically mounted. The custom image and the data disk snapshot must meet the following requirements:
- The data disk **must** be formatted and successfully mounted to the source CVM before the snapshot is created.
- Add the following commands to the `/etc/rc.local` file to configure the mount point of the data disk before creating a system disk on the system disk.
 ```
 mkdir -p <mount-point>
 mount <device-id> <mount-point>
 ```
>?
> - Replace `<mount-point>` with the mount point of the file system, such as `/mydata`.
> - Replace `<device-id>` with the partition path of the file system. For example, enter `/dev/vdb` if the file system has no partition, and `/dev/vdb1` if the file system has partitions.

## Mounting Manually

### Using the console to mount cloud disks
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. On the cloud disk list page, you can use the following methods to mount cloud disks.
 a. Select a cloud disk **to be mounted**, and click **More** > **Mount** under the **Operation** column.
 b. Select multiple cloud disks **to be mounted**, and click **Mount** at the top of the cloud disk list.
3. In the pop-up box, select the target CVM instance and click **OK**.
4. Refresh the cloud disk list.
 If the statuses of these cloud disks change to **Mounted**, this indicates that mounting is successful.
5. Perform subsequent operations as shown below to make the cloud disk usable.
 <table>
 <tr>
 <th>Creation mode</th>
 <th>Cloud disk capacity</th>
 <th>Subsequent operations</th>
 </tr>
 <tr>
 <td  rowspan="2">Create directly</td>
 <td>Cloud disk capacity < 2TB</td>
 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Initializing cloud disks (< 2 TB)</a></td>
 </tr>
 <tr>
  <td>Cloud disk capacity ≥ 2 TB</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (≥ 2 TB)</a></td>
 </tr>
  <tr>
	<td  rowspan="3">Create from a snapshot</td>
	<td>Cloud disk capacity = Snapshot capacity</td>
	<td><ul><li>Mounting to a Windows CVM: after logging in to the instance, make the disk online through **Server Management** > **Storage** > **Disk Management**.</li>
		<li>Mounting to a Linux CVM: after logging in to the instance, run the <code>mount <disk partition> <mount point></code> command, such as <code>mount /dev/vdb /mnt</code>.</li>
		</ul>
	</li></td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">Snapshot capacity < cloud disk capacity ≤ 2 TB <br/>or<br/>2 TB < snapshot capacity < cloud disk capacity</td>
<td><ul><li>Mounting to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601">extending partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31602">extending partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 <tr>
 <td>Snapshot capacity ≤ 2 TB < cloud disk capacity</td>
<td nowrap="nowrap"><ul><li>If the snapshot uses the MBR partition format:</li>see <a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing Cloud Disks (Larger than 2TB)</a> to use the GPT partition instead.<b>This operation will delete the original data.</b><li>If the snapshot uses the GPT partition format:<ul><li>Mounting to a Windows CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31601">extending partitions and file systems (Windows)</a></li><li>Mounting to a Linux CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31602">extending partitions and file systems (Linux)</a></li></ul></td>
 </tr> 
 </table>

### Using the API to mount cloud disks
You can use the `AttachDisks` API to mount a cloud disk. For more information, see [AttachDisks](https://intl.cloud.tencent.com/document/product/362/16313).

[](id:modprobeacpiphp)
### Enabling the disk hot swapping feature
All existing images already support mounting and unmounting elastic cloud disks. **To unmount a cloud disk, you must first run the `umount` command in Linux CVM or perform offline operations in Windows CVM. Otherwise, the remounted elastic cloud disk may not be recognized.**
However, if you want to mount an elastic cloud disk to a CVM with the following operating systems, we recommend that you first add drivers and enable the hot swapping feature in the CVM.
<table>
<tbody>
<tr><th>CVM operating system</th><th>Version</th>
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

1. [Log In to the Linux CVM](https://intl.cloud.tencent.com/document/product/213/5436) as the root user.
2. Run the following command to add the driver.
```
modprobe acpiphp
```
>?If you still need to load the `acpiphp` module after shutting down or re-starting the CVM, we recommend you run [Step 3](#step3) to set the `acpiphp` module to autoload.
<span id="step3"></span> 
3. (Optional) Run the following command according to the operating system to set the `acpiphp` module to autoload:
 - **CentOS 5 Series**
 a. Run the following command to create and open the `acpiphp.modules` file.
```
vi /etc/sysconfig/modules/acpiphp.modules
```
b. Add the following content to the file, and save.
```
 #!/bin/bash
 modprobe acpiphp >& /dev/null
```
c. Run the following command to grant execute permissions on the file.
```
chmod a+x /etc/sysconfig/modules/acpiphp.modules
```
 - **Debian 6 Series, Ubuntu 10.04 Series**
 a. Run the following command to modify the file.
```
vi /etc/modules
```
b. Add the following content to the file, and save.
```
acpiphp
```
 - **openSUSE 12.3 Series**
 a. Run the following command to modify the file.
```
vi /etc/sysconfig/kernel
```
b. Add the following content to the file, and save.
```
MODULES_LOADED_ON_BOOT="acpiphp"
```
