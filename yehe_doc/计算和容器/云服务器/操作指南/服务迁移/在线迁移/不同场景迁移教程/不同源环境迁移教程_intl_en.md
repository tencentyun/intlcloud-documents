## Overview
This document describes how to migrate systems and applications on source servers from your IDCs or other cloud platforms to Tencent Cloud through the online migration in the CVM console. The online migration meets the business requirements for enterprise cloudification, cross-cloud migration, cross-account or cross-region migration, and hybrid cloud deployment.

<dx-alert infotype="explain" title="">
The source server can be a physical server, a virtual machine, or a cloud server on another cloud platform, such as AWS, Google Cloud Platform, VMware, Alibaba Cloud, or Huawei Cloud.
</dx-alert>

## Prerequisites[](id:prerequisites)

- You have a Tencent Cloud account.
- If you want to use a sub-account to perform migration in the console, you need to log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) with the root account and associate the `QcloudCSMFullAccess` policy with the sub-account.
- You can create a key and obtain the `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
- [Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package.
- Stop applications on the source server to prevent existing applications from being affected by the migration.


## Directions

### Data Backup
- Source server: You can use the source server snapshot feature or other methods to back up data.
- Destination CVM: you can [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.

### Getting migration tool  
[Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to obtain the compressed migration tool package.

### Checking Before the Migration
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
	<th style="width: 15%;">Destination CVM (optional)</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		Storage space: The cloud disks (including the system disk and data disk) of the target CVM must offer sufficient storage space for saving data from the source server.</li>
		<li>Security group: Port 443 and port 80 cannot be restricted in the security group.</li>
		<li>
		Bandwidth setting: It is recommended that you maximize bandwidths at the 2 ends to speed up the migration. During the process, the traffic consumed is approximately the amount of data migrated. Adjust the billing mode before the migration if necessary.</li>
		<li>
		OS consistency: If the OSs of the source server and destination CVM are inconsistent, the created image may be inconsistent with the actual OS. We recommend that the OS of the destination CVM be the same as that of the source server. For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM as the destination.
		</li>
	  </ol>
	</td>
  </tr>
</table>


<dx-alert infotype="explain" title="">
 - You can use tool commands such as `sudo ./go2tencentcloud_x64 --check` to automatically check the source server.
 - By default, the go2tencentcloud migration tool automatically performs checks upon launch. To skip checks and perform forced migration, configure `Client.Extra.IgnoreCheck` to `true` in the client.json file.
- For more information on the go2tencentcloud migration tool, see [Compatibility and Tool Configuration Description](https://intl.cloud.tencent.com/document/product/213/44340).

</dx-alert>




## Starting Migration
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

If there are files or directories in the Linux source server that do not need to be migrated, you can add them to the [rsync_excludes_linux.txt file](https://intl.cloud.tencent.com/zh/document/product/213/44340#rsync_excludes_linux.txt-.E6.96.87.E4.BB.B6.E8.AF.B4.E6.98.8E.3Ca-id.3D.22_linuxtxtstate.22.3E.3C.2Fa.3E).
3. Import the migration source.
 i. For example, on a 64-bit Linux source server, execute the following commands in sequence as the root user to run the tool.
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
 ii. Enter the `SecretId` and `SecretKey` of the account API access key obtained in [Prerequisites](#prerequisites) and press **Enter** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/6e38d7e0487da4a2f6fd001e9953466a.png)
<dx-alert infotype="explain" title="">
You can also configure the account API access key in the `user.json` file before migration.
</dx-alert>
If the information in the following figure is displayed in the window of the migration tool, the migration source has been imported to the console successfully, and you can go to the console to view it:
<img src="https://qcloudimg.tencent-cloud.cn/raw/9261d9c0ce1789c1b7afa1accd6bf884.png"/>
You can log in to the <a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">CVM console</a> and enter the online migration page to view the imported migration source, whose status is <b>Online</b> as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
If "Import source server successfully" isn't displayed, the migration source failed to be imported, and you can view the log (which is the logs/log file in the migration tool directory by default) for troubleshooting. Then, run the migration tool to import the migration source again.
<dx-alert infotype="notice" title="">
After the migration source is imported successfully, don't close the migration tool in the instance until the migration task is completed; otherwise, the migration task can't be completed after the migration source becomes offline.
</dx-alert>

4. Go to the online migration page in the CVM console to create a migration task.
  i. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/csm/online?rid=1), go to the online migration page, and click **Create Migration Task** on the right of the desired migration source.
  ii. In the "Create migration task" pop-up window, configure the parameters as instructed in [Creating and starting migration task](https://intl.cloud.tencent.com/zh/document/product/213/44338#.E5.88.9B.E5.BB.BA.E5.B9.B6.E5.90.AF.E5.8A.A8.E8.BF.81.E7.A7.BB.E4.BB.BB.E5.8A.A1).
For example, to migrate a Linux source server to the Shanghai region of Tencent Cloud and generate the destination CVM image, you can configure the migration task as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)

5. Start the migration task
<dx-alert infotype="explain" title="">
You can skip this step if your task is scheduled, which will automatically start running at the scheduled execution time.
</dx-alert>
After creating a migration task, you can click the <b>Migration Task</b> tab to view the task as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
You can click <b>Start/Restart</b> on the right of the task to start it, click <b>OK</b> in the pop-up window, and the task status will become <b>Migrating</b> as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
6. Wait for the migration task to end
After the migration task status becomes **Successful**, the migration is completed successfully as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)
<dx-alert infotype="explain" title="">
The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to end. The migration tool supports checkpoint restart for data transfer.
</dx-alert>



### Checking after the Migration

- **Failed migration**:
Check the error information in log files (under the migration tool directory by default), operation guides, or FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting. After troubleshooting, click **Start/Restart** under the operation column to restart the migration task.
- **Successful migration**:
 - If the migration destination is a CVM, check whether the destination CVM starts up normally, whether data on the CVM is consistent with that on the source server, and whether the network and other system services are normal.
 - If the migration destination is a CVM image, you can click the **CVM image ID** on the row of the migration task to enter the [CVM image page](https://console.cloud.tencent.com/cvm/image/index) and view the image information. You can use it to create CVM instances.

If you have any questions or the migration has an exception, see FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [Contact Us](https://intl.cloud.tencent.com/document/product/213/34837).
