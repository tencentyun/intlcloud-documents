
This document describes how to use the online migration feature in the CVM console to migrate a server online.
<dx-alert infotype="explain" title="">
Currently, the online migration service in the console is in beta test. To try it out, [contact us](https://intl.cloud.tencent.com/document/product/213/34837) for application.
</dx-alert>

## Migration Process
The process of migration in the console is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0e290646e08b6af1b509ce324ea6e096.png)

## Prerequisites[](id:prerequisites)

- You have a Tencent Cloud account.
- If you want to use a sub-account to perform migration in the console, you need to log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) with the root account and associate the `QcloudCSMFullAccess` policy with the sub-account.
- Create and copy `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
[Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package.
- Stop applications on the source server to prevent existing applications from being affected by the migration.
- We recommend you back up your data in the following ways before migrating:
 - Source server: you can use the source server's snapshot feature or other methods to back up data.
 - Destination CVM: you can [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up the data of the destination CVM.

## Migration Directions


### Checking before migration

Before migration, you need to check the following configuration based on the actual conditions:
 - If the migration destination is a CVM instance, you need to check the source server and destination CVM.
 - If the migration destination is a CVM image, you need to check only the source server.

<table>
  <tr>
	<th>Linux source server</th>
	<td>
	  <ol style="margin: 0;">
		<li>Check and install Virtio. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>.</li> 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929"></a></li>
		<li>Run the <code>which rsync</code> command to check whether Rsync is installed, and if not, install it as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">How do I install Rsync?</a>.</li> 
		<li>Check whether SELinux is enabled, and if yes, disable it as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">How do I disable SELinux?</a>.</li>
		<li>After a migration request is made to the TencentCloud API, the API will use the current UNIX time to check the generated token. You need to make sure that the current system time is correct.</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">Destination CVM (optional)</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		Storage space: the cloud disks of the destination CVM (including system and data disks) should have sufficient capacity to save data migrated from the source server.</li>
		<li>Security group: port 443 and port 80 cannot be restricted in the security group.</li>
		<li>
		Bandwidth settings: we recommend you maximize bandwidths at the two ends to speed up the migration. During the process, the traffic consumed is approximately the amount of data migrated. Adjust the billing mode before the migration if necessary.</li>
		<li>
		OS consistency: if the operating systems of the source server and destination CVM are different, the created image may be inconsistent with the actual operating system. We recommend you use the same operating system for the source server and destination CVM. For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM as the destination.</li>
	  </ol>
	</td>
  </tr>
</table>



<dx-alert infotype="explain" title="">
- You can use tool commands such as `sudo ./go2tencentcloud_x64 --check` to automatically check the source server.
- By default, the go2tencentcloud migration tool automatically starts checking upon launch. To skip checks and perform forced migration, configure `Client.Extra.IgnoreCheck` to `true` in the `client.json` file.
</dx-alert>



### Registering migration source[](id:registrationSource)

1. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
    1. Run the following commands in sequence to decompress `go2tencentcloud.zip` and enter the directory.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. Run the following commands in sequence to decompress `go2tencentcloud_console.zip` and enter the directory:
```sh
unzip go2tencentcloud_console.zip
```
```sh
cd go2tencentcloud_console
```
<dx-alert infotype="explain" title="">
The files in the `go2tencentcloud` directory will not be migrated. Do not place the files to be migrated in this directory.
</dx-alert>
2. (Optional) Exclude files or directories that do not need to be migrated on the source server.
If there are files or directories on the Linux source server that do not need to be migrated, you can add them to the [rsync_excludes_linux.txt](https://intl.cloud.tencent.com/document/product/213/44340) file.
3. Import the migration source.
  1. This document takes a 64-bit Linux source server as an example. Go to the `go2tencentcloud` directory and run the following commands in sequence as the root user to run the tool.
```sh
chmod +x go2tencentcloud_x64
```
```sh
sudo ./go2tencentcloud_x64
```
   2. Enter the `SecretId` and `SecretKey` of the account API access key obtained in [Prerequisites](#prerequisites) and press **Enter** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png)
<dx-alert infotype="explain" title="">
You can also configure the account API access key in the `user.json` file before migration.
</dx-alert>
If the information in the following figure is displayed in the window of the migration tool, the migration source has been imported to the console successfully, and you can go to the console to view it:
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
<br>You can log in to the <a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">CVM console</a> and enter the online migration page to view the imported migration source, whose status is **Online** as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
   2. If "Import source server successfully" isn't displayed, the migration source failed to be imported, and you can view the log (which is the `logs/log` file in the migration tool directory by default) for troubleshooting. Then, run the migration tool to import the migration source again.
<dx-alert infotype="notice" title="">
After the migration source is imported successfully, don't close the migration tool in the instance until the migration task is completed; otherwise, the migration task can't be completed after the migration source becomes offline.
</dx-alert>



### Creating and starting migration task

1. Create a migration task
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/csm/online?rid=1), go to the online migration page, and click **Create migration task** on the right of the desired migration source. In the **Create migration task** pop-up window, configure the task  as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)
2. [](id:jobSettings)Configure the migration as follows:
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
<td>Target region</td>
<td>Yes</td>
  <td>Tencent Cloud region to which the source server is to be migrated. For more information on regions, see <a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and AZs</a>.</td>
</tr>
<tr>
<td>Task name</td>
<td>Yes</td>
<td>Migration task name.</td>
</tr>
<tr>
<td>Task description</td>
<td>No</td>
<td>Migration task description.</td>
</tr>
<tr>
<td>Target type</td>
<td>Yes</td>
<td>
  Set the destination type for the source server to be migrated to Tencent Cloud.
    <ul>
    <li><b>CVM image</b>: a destination CVM image will be generated for the migration source after the migration task is completed.
      <br>Image Name: name of the destination CVM image that will be generated for the migration source, which is <b>required</b>. If an image with the same name already exists in the destination region, the migration task will automatically add the task ID to the name.
    </li>
    <li><b>CVM instance</b>: select a CVM instance in the destination region as the migration destination.
      <br>Destination Instance: it is <b>required</b>. We recommend you use the same operating system for the source server and destination CVM. For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM as the destination.
    </li>
  </ul>
</td>
</tr>
<tr>
<td>Scheduled start time</td>
<td>No</td> 
  <td>Set the time when the migration task will be automatically started after creation. It can be as early as <b>10</b> minutes after the current time.</td>
</tr>
<tr>
<td>Transfer speed limit (KB/s)</td>
<td>No</td>  
<td>Cap of the data transfer bandwidth during migration in KB/s.</td>
</tr>
<tr>
<td>Checksum verification</td>
<td>No</td>  
<td>After it is enabled, data consistency check will be enhanced, but the transfer speed may be reduced.</td>
</tr>
</tbody></table>
2. Start the migration task.
<dx-alert infotype="explain" title="">
You can skip this step if your task is scheduled, which will automatically start running at the scheduled execution time.
</dx-alert>
After creating a migration task, you can click the <b>Migration task</b> tab to view the task as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
2. You can click <b>Start/Restart</b> on the right of the task to start it, and the task status will become **Migrating** as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
4. <dx-alert infotype="notice" title="">
- The migration in console feature can automatically migrate the system disk and all mounted data disks of the source server and generate destination disks with the same partition structure as the source disks.
- Currently, the migration in console feature supports only the public network. To migrate over the private network, you can use the migration tool. For more information, see [Private Network Migration](https://intl.cloud.tencent.com/document/product/213/44341).
- If the migration destination is a CVM instance, the destination CVM enters migration mode after the migration starts. Do not reinstall the system, shut down, terminate, or reset passwords of the destination CVM until the migration is completed and the destination CVM exits the migration mode.
- If the migration destination is a CVM image, a relay instance `do_not_delete_csm_instance` will be created under your account after the migration starts. Don't reinstall, shut down, or terminate the relay instance or reset its password. It will be automatically terminated by the system after the migration is completed.
</dx-alert>


### Waiting for migration task to end

After the migration task status becomes **Successful**, the migration is completed successfully as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)

<dx-alert infotype="explain" title="">
- The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to complete.
- After the migration task starts, you can click **Pause** on the row of the task to stop it.
- The migration tool supports checkpoint restart. After a task is paused, you can click **Start/restart** again to resume migration from where you paused.
- A migration task can be paused during data transfer. After you click **Pause** for it in the console, the migration tool will pause the data transfer in progress.
- If the migration process is time-consuming and you need to stop it, you can pause the migration task first and click **Delete** to delete it.
</dx-alert>



### Checking after migration[](id:checkAfter)

- **Failed migration**:
Check the error information in log files (under the migration tool directory by default), operation guides, or [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting methods. After fixing the problem, click **Start/restart** in the **Operation** column of the migration task to start it again.
- **Successful migration**:
 - If the migration destination is a CVM instance, check whether the destination CVM can be started normally, whether data on the destination CVM is consistent with that on the source server, whether the network is normal, and whether other system services run normally.
 - If the migration destination is a CVM image, you can click the **CVM image ID** on the row of the migration task to enter the [CVM image page](https://console.cloud.tencent.com/cvm/image/index) and view the image information. You can use it to create CVM instances.

If you have any questions or the migration has an exception, see [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [contact us](https://intl.cloud.tencent.com/document/product/213/34837).



