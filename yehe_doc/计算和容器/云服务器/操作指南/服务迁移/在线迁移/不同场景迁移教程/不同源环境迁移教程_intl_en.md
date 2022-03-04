## Overview
This document describes how to use online migration in the CVM console to migrate the system and applications on a source server from a self-built IDC or cloud platform to Tencent Cloud. It meets the business requirements for enterprise cloudification, cross-cloud migration, cross-account/region migration, and hybrid cloud deployment.


<dx-alert infotype="explain" title="">
- The source server can be a physical server, a virtual machine, or a cloud server on another cloud platform, such as AWS, Microsoft Azure, Google Cloud Platform, VMware, Alibaba Cloud, or Huawei Cloud.
- You can also use the migration tool for migration as instructed in [Migration via Tool](https://intl.cloud.tencent.com/document/product/213/35640).
</dx-alert>


## Prerequisites[](id:prerequisites)

- You have a Tencent Cloud account.
- If you want to use a sub-account to perform migration in the console, you need to log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) with the root account and associate the `QcloudCSMFullAccess` policy with the sub-account.
- Create and copy `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
[Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package.
- Stop applications on the source server to prevent existing applications from being affected by the migration.


## Directions

### Backing up data
- Source server: you can use the source server's snapshot feature or other methods to back up data.
- Destination CVM: you can [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.

### Getting migration tool  
[Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to obtain the compressed migration tool package.

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
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>。</li>
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
- For more information on the go2tencentcloud migration tool, see [Migration Tool Description](https://intl.cloud.tencent.com/document/product/213/44340).

</dx-alert>




## Starting Migration
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
2. (Optional) Exclude files or directories that do not need to be migrated on the source server. 
If there are files or directories on the Linux source server that do not need to be migrated, you can add them to the [rsync_excludes_linux.txt](https://intl.cloud.tencent.com/document/product/213/44340) file.
3. Import the migration source.
  1. This document takes a 64-bit Linux source server as an example. Go to the `go2tencentcloud` directory and run the following commands in sequence as the root user to run the tool.
```shell
chmod +x go2tencentcloud_x64
```
```shell
sudo ./go2tencentcloud_x64
```
   2. Enter the `SecretId` and `SecretKey` of the account API access key obtained in [Prerequisites](#prerequisites) and press **Enter** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/6e38d7e0487da4a2f6fd001e9953466a.png)
<dx-alert infotype="explain" title="">
You can also configure the account API access key in the `user.json` file before migration.
</dx-alert>
If the information in the following figure is displayed in the window of the migration tool, the migration source has been imported to the console successfully, and you can go to the console to view it:
<img src="https://qcloudimg.tencent-cloud.cn/raw/9261d9c0ce1789c1b7afa1accd6bf884.png"/>
You can log in to the <a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">CVM console</a> and enter the online migration page to view the imported migration source, whose status is **Online** as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
If "Import source server successfully" isn't displayed, the migration source failed to be imported, and you can view the log (which is the `logs/log` file in the migration tool directory by default) for troubleshooting. Then, run the migration tool to import the migration source again.
<dx-alert infotype="notice" title="">
After the migration source is imported successfully, don't close the migration tool in the instance until the migration task is completed; otherwise, the migration task can't be completed after the migration source becomes offline.
</dx-alert>
4. Go to the online migration page in the CVM console to create a migration task.
  1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/csm/online?rid=1), go to the online migration page, and click **Create Migration Task** on the right of the desired migration source.
  2. In the **Create Migration Task** pop-up window, configure the task as instructed in [Migration Task Configuration Description](https://intl.cloud.tencent.com/document/product/213/44338).
For example, to migrate a Linux source server to the Shanghai region of Tencent Cloud and generate the destination CVM image, you can configure the migration task as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)
5. Start the migration task.
<dx-alert infotype="explain" title="">
You can skip this step if your task is scheduled, which will automatically start running at the scheduled execution time.
</dx-alert>
After creating a migration task, you can click the <b>Migration Task</b> tab to view the task as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
You can click <b>Start/Retry</b> on the right of the task to start it, and the task status will become **Migrating** as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
6. Wait for the migrate task to end.
After the migration task status becomes **Successful**, the migration is completed successfully as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)
<dx-alert infotype="explain" title="">
The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to complete. The migration tool supports checkpoint restart for data transfer.
</dx-alert>



### Checking after migration

- **Failed migration**:
Check the error information in log files (under the migration tool directory by default), operation guides, or [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting methods. After fixing the problem, click **Start/Retry** in the **Operation** column of the migration task to start it again.
- **Successful migration**:
 - If the migration destination is a CVM instance, check whether the destination CVM can be started normally, whether data on the destination CVM is consistent with that on the source server, whether the network is normal, and whether other system services run normally.
 - If the migration destination is a CVM image, you can click the **CVM image ID** on the row of the migration task to enter the [CVM image page](https://console.cloud.tencent.com/cvm/image/index) and view the image information. You can use it to create CVM instances.

If you have any questions or the migration has an exception, see [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [contact us](https://intl.cloud.tencent.com/document/product/213/34837).
