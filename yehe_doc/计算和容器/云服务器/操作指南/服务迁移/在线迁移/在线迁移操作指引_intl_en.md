This document describes how to use the online migration feature in the CVM console to migrate a server online.


## Migration Process
The online migration procedure is shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0e290646e08b6af1b509ce324ea6e096.png)

[](id:prerequisites)
## Considerations

- Register on Tencent Cloud International.
- If you want to migrate using a sub-account, ask the root account owner to assign the sub-account with the `QcloudCSMFullAccess` and `QcloudCVMFullAccess` permissions in [CAM console](https://console.cloud.tencent.com/cam/policy).
- Create a key and obtain the `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
- [Download](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) the compressed migration tool package.
- Stop all applications on the source server to prevent them from being affected by the migration.
- Back up your data in the following ways before migrating:
  - Source server: You can use the source server snapshot feature or other methods to back up data.
  - Destination CVM: You can create a snapshot as instructed in [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.

## Migration Directions


### Checking before the migration

Before migration, you need to check the following configuration based on the actual conditions:
 - If the migration destination is a CVM instance, you need to check the source server and destination CVM.
 - If the migration destination is a CVM image, you need to check only the source server.

<table>
  <tr>
	<th>Linux source server</th>
	<td>
	  <ol style="margin: 0;">
		<li>Check and install Virtio. For more information, see  
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>.</li>
		<li>Run  
		the <code>which rsync</code> command to check whether Rsync is installed, and if not, install it as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">How do I install Rsync?</a>.</li>
		<li>Check whether SELinux is enabled, and if yes, disable it as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">How do I disable SELinux?</a>.</li>
		<li>After a migration request is made to the Tencent Cloud API, the API will use the current UNIX time to check the generated
		token. You need to make sure that the current system time is correct.</li>
	  </ol>
	</td>
 </tr>
  <tr>
	<th>Windows source server</th>
	<td>
	  <ol style="margin: 0;">
		<li>Check and install Virtio. For more information, see  
		<a href="https://intl.cloud.tencent.com/document/product/213/17815">Checking or installing the Virtio driver</a>.</li>
		<li>(Optional) Check and install Cloudbase-Init. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/32364">Installing Cloudbase-Init on Windows</a>. You can install it on the source server before the migration, or install it on the destination instance after the migration.<br>If you install it before the migration, network configuration and activation are performed automatically after the migration.<br>If you do not install it before the migration, you need to <a href="https://intl.cloud.tencent.com/document/product/213/32496">Log into Windows Instance via VNC</a>, and modify the network configuration manually.</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">Destination CVM (optional)</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		Storage space: The cloud disks (including the system disk and data disk) of the destination CVM must offer sufficient storage space for saving data from the source server.</li>
		<li>Security group: Port 443 and port 80 cannot be restricted in the security group.</li>
		<li>
		Bandwidth setting: It is recommended that you maximize bandwidths at the 2 ends to speed up the migration. During the process, the traffic consumed is approximately the amount of data migrated. Adjust the billing mode before the migration if necessary.</li>
	  </ol>
	</td>
  </tr>
</table>


<dx-alert infotype="explain" title="">
- You can use tool commands such as `sudo ./go2tencentcloud_x64 --check` to automatically check the source server.
- By default, the go2tencentcloud migration tool automatically performs checks upon launch. To skip checks and perform forced migration, configure `Client.Extra.IgnoreCheck` to `true` in the client.json file.
</dx-alert>


[](id:registrationSource)
### Registering migration source
#### Importing migration source with migration tool
<dx-tabs>
::: Linux CVM instances
1. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
   i. Run the following commands in sequence to decompress `go2tencentcloud.zip` and enter the directory.
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
   ii. Run the following commands in sequence to decompress `go2tencentcloud-linux.zip` and enter the directory.
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
The files in the `go2tencentcloud` directory will not be migrated. Do not place the files to be migrated in this directory.
</dx-alert>
2. (Optional) Exclude files and directories on the source server that do not need to be migrated.
If there are files or directories on the Linux source server that do not need to be migrated, you can add them to the [rsync_excludes_linux.txt] file, as described in Compatibility and Tool Configuration Description (https://intl.cloud.tencent.com/document/product/213/44340).
3. Import the migration source.
   i. For example, on a 64-bit Linux source server, execute the following command in sequence as the root user to run the tool.
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
   ii. Enter the `SecretId` and `SecretKey` of the account API access key obtained in [Prerequisites](#prerequisites) and press **Enter** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png)
If the information in the following figure is displayed in the window of the migration tool, the migration source has been imported to the console successfully, and you can go to the console to view it:
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
:::

::: Windows CVM instances
1. Download or upload `go2tencentcloud.zip` to the source server, decompress the file to `go2tencentcloud` folder. Extract `go2tencentcloud-windows.zip` and decompress it. The directory obtained is as shown in the following figure:
![](https://qcloudimg.tencent-cloud.cn/raw/3f2c9881d9c5323a14d096d0811814cd.png)    
2. Run `go2tencentcloud_x64.exe` with one of the following methods.
	- Method 1: Right-click `go2tencentcloud_x64.exe` and run it as admin. Enter `SecretId` and `SecretKey` in the pop-up window.
	- Method 2: Start cmd or PowerShell command line as admin: cd /d "absolute path of the directory of go2tencentcloud_x64.exe", and run `go2tencentcloud_x64.exe`.
3. Enter Tencent Cloud API key (`SecretId` and `SecretKey`) in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/b7af60919e710d7d148e791124fce1a0.png) ![](https://qcloudimg.tencent-cloud.cn/raw/8494a126134389796be195ccd268e03a.png)       

4. If the information in the following figure is displayed in the window of the migration tool, the migration source has been imported to the console successfully, and you can go to the console to view it:
![](https://qcloudimg.tencent-cloud.cn/raw/5ecd29f96415d0cb090fe165909272be.png)
:::
</dx-tabs>

#### Viewing migration source in the console
You can log in to the <a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">CVM console</a> and enter the online migration page to view the imported migration source, whose status is **Online** as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
If "Import source server successfully" isn't displayed, the migration source failed to be imported, and you can view the log (which is the `logs/log` file in the migration tool directory by default) for troubleshooting. Then, run the migration tool to import the migration source again.

>! After the migration source is imported successfully, don't close the migration tool in the instance until the migration task is completed; otherwise, the migration task can't be completed after the migration source becomes offline.


### Creating and starting a migration task

1. Create a migration task
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/csm/online?rid=1), go to the online migration page, and click **Create Migration Task** on the right of the desired migration source. In the **Create Migration Task** pop-up window, configure the task as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)
[](id:jobSettings)Configure the migration as follows:
 - **Basic Options**:
<table>
<thead>
<tr>
<th width="18%">Configuration Item</th>
<th width="10%">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Destination Region</td>
<td>Yes</td>
  <td>The Tencent Cloud region to which the source server is to be migrated. For information on regions, see<a href="https://intl.cloud.tencent.com/document/product/582/35772">Regions and AZs</a>.</td>
</tr>
<tr>
<td>Task name</td>
<td>Yes</td>
<td>The migration task name.</td>
</tr>
<tr>
<td>Task Description</td>
<td>No</td>
<td>Migration task description.</td>
</tr>
<tr>
<td>Destination Type</td>
<td>Yes</td>
<td>
  Set the destination type for the source server to be migrated to Tencent Cloud.
    <ul>
    <li><b>CVM Image</b>: A destination CVM image will be generated for the migration source after the migration task ends.
      <br>Image name: Name of the destination CVM image that will be generated for the migration source. If an image with the same name already exists in the destination region, the migration task will automatically add the task ID to the name.
    </li>
    <li><b>CVM Instance</b>: Select a CVM instance in the destination region as the migration destination.
      <br>Destination instance: We recommend you use the same operating system for the source server and destination CVM. For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM as the destination.
    </li>
  </ul>
</td>
</tr>
<tr>
<td>Scheduled Execution Time</td>
<td>No</td> 
  <td>Set the time when the migration task will be automatically started after creation. It can be as early as <b>10</b> minutes after the current time.</td>
</tr>
</tbody></table>
 - **Advanced Options (optional)**:
<table>
<thead>
<tr>
<th width="18%">Configuration Item</th>
<th width="10%">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Network Mode</td>
<td>No</td>
<td>
  Set the network type for transferring data in migration.
    <ul>
    <li><b>Transfer via public network</b>: Transfer data to the destination CVM or relay instance via the public network.
    </li>
    <li><b>Transfer via private network</b>: Transfer data to the destination CVM or relay instance via the private network. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/44341">Private Network Migration</a>.
      <br>VPC: Create the relay instance in a VPC when migrating to a CVM image.
      <br>Subnet: Create the relay instance in a subnet when migrating to a CVM image.
    </li>
  </ul>
</td>
</tr>	
<tr>
<td>Transfer Restriction (KB/s)</td>
<td>No</td>  
<td>The bandwidth for data transfer during the migration ranges from 0 to 25600 KB/s. The transfer rate is unlimited by default. This item is not available for migration on Windows.</td>
</tr>
<tr>
<td>Checksum Verification</td>
<td>No</td>  
<td>When it is enabled, data consistency check is enhanced, but the transfer speed may be reduced. This item is not available for migration on Windows.</td>
</tr>
</tbody></table>
2. Start the migration task
<dx-alert infotype="explain" title="">
You can skip this step if your task is scheduled, which will automatically start running at the scheduled execution time.
</dx-alert>
After creating a migration task, you can click the <b>Migration Task</b> tab to view the task as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
You can click <b>Start/Retry</b> on the right of the task to start it, click <b>OK</b> in the pop-up window, and the task status will become **Migrating** as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
<dx-alert infotype="notice" title="">
- If the migration destination is a CVM, the destination CVM enters migration mode after the migration starts. Do not reinstall the system, shut down, terminate, or reset passwords of the destination CVM until the migration ends and the destination CVM exits the migration mode.
- If the migration destination is a CVM image, a relay instance `do_not_delete_csm_instance` will be created under your account after the migration starts. Don't reinstall, shut down, or terminate the relay instance or reset its password. It will be automatically terminated by the system after the migration ends.
</dx-alert>


### Waiting for migration task to end

After the migration task status becomes **Successful**, the migration is completed successfully as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)

<dx-alert infotype="explain" title="">
- The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to end.
- After the migration task starts, you can click **Pause** on the row of the task to stop it.
- The migration tool supports checkpoint restart. After a task is paused, you can click **Start/Retry** again to resume migration from where you paused.
- A migration task can be paused during data transfer. After you click **Pause** for it in the console, the migration tool will pause the data transfer in progress.
- If the migration process is time-consuming and you need to stop it, you can pause the migration task first and click **Delete** to delete it.
</dx-alert>

### Checking after migration[](id:checkAfter)

- **Failed migration**:
- Check the error information in log files (under the migration tool directory by default), operation guides, or FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting methods. After troubleshooting, click **Start/Retry** under the operation column to restart the migration task.
- **Successful migration**:
 - Migrating to a CVM: Check whether the destination CVM starts up normally, whether data on the CVM is consistent with that on the source server, and whether the network and other system services are normal.
 - Migrating to a CVM image: Click the **CVM image ID** on the row of the migration task to enter the [CVM image page](https://console.cloud.tencent.com/cvm/image/index) and view the image information. You can use this image to create CVM instances.

If you have any questions or the migration has an exception, see FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [Contact Us](https://intl.cloud.tencent.com/document/product/213/34837).



