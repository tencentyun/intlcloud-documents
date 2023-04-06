This document describes how to migrate a server to Tencent Cloud.

## Migration Workflow
The online migration procedure is shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0e290646e08b6af1b509ce324ea6e096.png)
[](id:prerequisites)

## Preparation
- Go to [Manage API Key](https://console.cloud.tencent.com/cam/capi) to create a key and obtain the `SecretId` and `SecretKey`.
- Stop applications on the server and back up your data.
 - Source server: Backup the server on local.
 - Destination CVM: Create a snapshot of the instance (See [Creating Snapshots](https://www.tencentcloud.com/document/product/362/5755))
- If you are using a sub-account, ask the root account to assign you the `QcloudCSMFullAccess` and `QcloudCVMFullAccess` permissions in the [CAM console](https://console.cloud.tencent.com/cam/policy).

## Migration Directions
### Step 1: Check before the migration

 
 - Migrate to a CVM instance: Check the source server and destination CVM.
 - Migrate to a CVM image: Check the source server.

<table>
  <tr>
	<th>Linux source server</th>
	<td>
	  <ol style="margin: 0;">
		<li>Check and install Virtio. For more information, see  
		<a href="https://www.tencentcloud.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>.</li>
		<li>Run  
		<code>which rsync</code> to check whether Rsync is installed. If not, install it as instructed in <a href="https://www.tencentcloud.com/document/product/213/32395#installRsync">How do I install Rsync?</a>.</li>
		<li>Check whether SELinux is enabled, If yes, disable it as instructed in <a href="https://www.tencentcloud.com/document/product/213/32395#closeSELinux">How do I disable SELinux?</a>.</li>
		<li>Make sure that the system time of your server is correct. After the migration task starts, Tencent Cloud API generates a token using the current UNIX 
		for verification.</li>
	  </ol>
	</td>
 </tr>
  <tr>
	<th>Windows source server</th>
	<td>
	  <ol style="margin: 0;">
		<li>Check and install Virtio. For more information, see  
		<a href="https://www.tencentcloud.com/document/product/213/17815">Checking or installing the Virtio driver</a>.</li>
		<li>(Optional) Check and install Cloudbase-Init (See <a href="https://www.tencentcloud.com/document/product/213/32364">Installing Cloudbase-Init on Windows</a>). It’s recommended to install it on the source server before the migration. <br>In this case, the network configuration and OS license activation are performed automatically after the migration. <br>Otherwise you need to <a href="https://www.tencentcloud.com/document/product/213/32496">log in to the instance via VNC</a>, and modify the network configuration manually on the destination server after migration.</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">Destination CVM (optional)</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		Storage space: The cloud disks (including the system disk and data disk) of the destination CVM must have sufficient space for the source server.</li>
		<li>Security group: Port 80, port 443 and port 3389 are opened.</li>
		<li>
		Bandwidth: Set the bandwidth cap on both the two ends to the highest possible value. During the process, the traffic consumed is approximately the amount of data migrated. Adjust the billing mode beforehand if necessary.</li>
<li>
		Network: If the source or destination server only supports IPv6 but not IPv4, see <a href="https://www.tencentcloud.com/document/product/213/44340"> Parameters in the client.json file</a>.</li>
	  </ol>
	</td>
  </tr>
</table>


<dx-alert infotype="explain" title="">
- Check the source server by executing `sudo ./go2tencentcloud_x64 --check`.
- By default, go2tencentcloud automatically performs checks upon launch. To skip checks, open the `client.json` file, set `Client.Extra.IgnoreCheck` to `true` 
</dx-alert>

[](id:registrationSource)
### Step 2: Register the migration source
#### Register source server
<dx-tabs>
::: Linux source server
1. Download the migration tool on the source server.
  - Run the following commands in sequence to [download](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) and decompress the migration tool `go2tencentcloud.zip` and go to the corresponding directory.
```shellsession
wget https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip
```
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
- Run the following commands in sequence to decompress `go2tencentcloud-linux.zip` and go to the directory.

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
Add files and directories that don’t need to be migrate to the [rsync_excludes_linux.txt](https://www.tencentcloud.com/document/product/213/44340) file.
3. Register the source
  - Assume that we need to register a 64-bit Linux source server. Execute the following commands in sequence as the root user.
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
  - Enter the `SecretId` and `SecretKey` of the account API access key obtained in the [Prerequisites](#prerequisites) step and press **Enter**.
![](https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png)
If you see the following message, the source server is registered successfully. You can now see the server in the CVM console.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
:::

::: Windows source server
1. [Download](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) and upload `go2tencentcloud.zip` to the source server. Decompress the file to the `go2tencentcloud` folder. Extract `go2tencentcloud-windows.zip` and decompress it. 
![](https://qcloudimg.tencent-cloud.cn/raw/3f2c9881d9c5323a14d096d0811814cd.png)    
2. Run `go2tencentcloud_x64.exe`
	- Method 1: Right-click `go2tencentcloud_x64.exe` and run it as admin. Enter `SecretId` and `SecretKey` in the pop-up window.
	- Method 2: Start cmd or PowerShell command line as admin: cd /d "absolute path of the directory of go2tencentcloud_x64.exe", and run `go2tencentcloud_x64.exe`.
3. Enter Tencent Cloud API key (`SecretId` and `SecretKey`) in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/b7af60919e710d7d148e791124fce1a0.png) ![](https://qcloudimg.tencent-cloud.cn/raw/8494a126134389796be195ccd268e03a.png)       

4. If the following message appears, the source server information is registered. You can now check the source server in the CVM console. 
![](https://qcloudimg.tencent-cloud.cn/raw/5ecd29f96415d0cb090fe165909272be.png)
:::
</dx-tabs>
<dx-alert infotype="explain" title="">
If "Import source server successfully" does not appear, check the logs in the `logs/log` file under the migration tool directory for troubleshooting. 
</dx-alert>

#### Check the registered server in the console
Log in to the <a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">CVM console</a>, go to **Online migration** to check the registered server. Its status should be **Online**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>

>! Registering the source server is the first step of migration. Keep the migration tool alive till the whole migration progress ends.


### Step 3: Create and start a migration task

1. Create a migration task
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/csm/online?rid=1), go to the online migration page, locate the source server and click **Create Migration Task**. In the **Create Migration Task** pop-up window, configure the task.
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)
[](id:jobSettings)Configuration description:
 - **Basic options**:
<table>
<thead>
<tr>
<th width="18%">Item</th>
<th width="10%">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Destination region</td>
<td>Yes</td>
  <td>The Tencent Cloud region to which the source server is to be migrated. For information on regions, see<a href="https://www.tencentcloud.com/document/product/582/35772">Regions and AZs</a>.</td>
</tr>
<tr>
<td>Task name</td>
<td>Yes</td>
<td>The migration task name.</td>
</tr>
<tr>
<td>Task description</td>
<td>No</td>
<td>Migration task description.</td>
</tr>
<tr>
<td>Destination type</td>
<td>Yes</td>
<td>
  Set the destination type for the source server to be migrated to Tencent Cloud.
    <ul>
    <li><b>CVM image</b>: Create a CVM image for the source server
      <br>Image name: Name of the destination CVM image that will be generated for the migration source. If the name already exists, the migration task ID is appended to the name.
    </li>
    <li><b>CVM instance</b>: Select a CVM instance in the destination region as the migration destination.
      <br>Destination instance: We recommend you use the same operating system for the source server and destination CVM. For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM as the destination.
    </li>
  </ul>
</td>
</tr>
<tr>
<tr>
<td>Network mode</td>
<td>Yes</td>
<td>
  The network used for transferring data.
    <ul>
    <li><b>Public network</b>: Transfer over the public network.
    </li>
    <li><b>Private network</b>: Transfer over the private network. For details, see <a href="https://www.tencentcloud.com/document/product/213/44341">Migrating via Private Network</a>.
      <br>VPC: Create the relay instance in a VPC when migrating to a CVM image.
      <br>Subnet: Create the relay instance in a subnet when migrating to a CVM image.
    </li>
  </ul>
</td>
</tr>	
<tr>
<td rowspan='2'>Migration method</td>
<td rowspan='2'>Yes</td>
<td>
  For Linux instances:
    <ul>
    <li><b>File-level migration</b>: Higher compatibility and relatively slower transfer speed.
    </li>
    <li><b>Block-level migration</b>: Faster transfer speed and relatively lower compatibility.
    </li>
  </ul>
</td>
</tr>	
<tr>
<td>
<b>Windows block-level migration</b>: Block-level migration, with faster transfer speed and relatively lower compatibility. 
  </ul>
</td>
</tr>	
<tr>
<td>Configure incremental sync</td>
<td>No</td>
<td>You can customize the incremental sync duration to continuously sync the data.
	<ul>
		<li><b>Not enable</b>: The migration tool scans for and migrate the increments. Generally, it is implemented for once.</li>
		<li><b>Enable</b>: You can select the incremental sync duration. The migration tool will continuously sync the data to Tencent Cloud. You can also manually stop the incremental sync in the task list.</li>
	</ul>
</td>
</tr>
<td>Scheduled execution time</td>
<td>No</td> 
<td>Set the time when the migration task will be automatically started after creation. It can be as early as <b>10</b> minutes after the current time.</td>
</tr>
</tbody></table>
 - **Advanced options (optional)**:
<table>
<thead>
<tr>
<th width="18%">Item</th>
<th width="10%">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Data rate (KB/s)</td>
<td>No</td>  
<td>The upper limit of data rate during the migration (0 to 25600 KB/s). It’s set to 0 by default. This item is not available for migration to Windows.</td>
</tr>
<tr>
<td>Checksum verification</td>
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

### Step 4: Wait for the migration task to complete

After the migration task status becomes **Successful**, the migration is completed successfully as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)

<dx-alert infotype="explain" title="">
- The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to end.
- After the migration task starts, you can click **Pause** on the row of the task to stop it.
- The migration tool supports checkpoint restart. After a task is paused, you can click **Start/Retry** again to resume migration from where you paused.
- A migration task can be paused during data transfer. After you click **Pause** for it in the console, the migration tool will pause the data transfer in progress.
- If the migration process is time-consuming and you need to stop it, you can pause the migration task first and click **Delete** to delete it.
</dx-alert>

### Step 5: Check after the migration[](id:checkAfter)

- **Failed migration**:
Check the error information in log files (under the migration tool directory by default), operation guides, or FAQs about [Service Migration](https://www.tencentcloud.com/document/product/213/32395) for troubleshooting. After troubleshooting, click **Start/Retry** under the operation column to restart the migration task.
- **Successful migration**:
 - Migrating to a CVM: The destination CVM starts up normally. Data on the CVM is consistent with that on the source server. The network and other system services are normal.
 - Migrating to a CVM image: Click the **CVM image ID** on the row of the migration task to enter the [CVM image page](https://console.cloud.tencent.com/cvm/image/index) and view the image information. You can use this image to create CVM instances.

If you have any questions or the migration has an exception, see FAQs about [Service Migration](https://www.tencentcloud.com/document/product/213/32395) or [Contact Us](https://www.tencentcloud.com/document/product/213/34837).
