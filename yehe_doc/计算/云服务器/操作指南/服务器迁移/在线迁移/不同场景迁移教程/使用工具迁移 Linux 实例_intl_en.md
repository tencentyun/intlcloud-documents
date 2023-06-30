This document introduces how to use the migration tool go2tencentcloud to migrate the Linux-based CVM online.

## Preparations

- You already have a Tencent Cloud account and a destination CVM.
- Stop applications on the source server to prevent existing applications from being affected by the migration.
- [Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package.
- You can create a key and obtain the `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
- Check that both source servers and destination CVM meet the migration requirements. For example, the cloud disks of the destination CVM should have sufficient capacity to save data migrated from source servers.
- We recommend you back up your data in the following ways before migrating:
 - Source server: You can use the source server snapshot feature or other methods to back up data.
 - Destination CVM: You can create a snapshot as instructed in [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.

## Migration Toolkit

### Files in the compressed package

After `go2tencentcloud.zip` is decompressed, it contains the following files:
<table>
	<tr><th width="30%">File Name</th><th>Description</th></tr>
	<tr><td>go2tencentcloud-linux.zip</td><td>The migration zip for Linux system.</td></tr>
	<tr><td>readme.txt</td><td>Directory overview file.</td></tr>
	<tr><td>release_notes.txt</td><td>Migration tool change log.</td></tr>
</table>

After `go2tencentcloud-linux.zip` is decompressed, it contains the following files:
<table>
	<tr><th width="30%">File Name</th><th>Description</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>Executable program of the migration tool for the 64-bit Linux operating system</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>Executable program of the migration tool for the 32-bit Linux operating system</td></tr>
	<tr><td>user.json</td><td>User information in the migration.</td></tr>
	<tr><td>client.json</td><td>Configuration file of the migration tool.</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync configuration file, which excludes files and directories that do not need to be migrated in the Linux system.</td></tr>
</table>

<dx-alert infotype="notice" title="">
The configuration files cannot be deleted. You must store them under the same folder as the go2tencentcloud executable program. 
</dx-alert>

### Parameters in the user.json file[](id:userJsonState)

The user.json configuration file is described as below:

<table>
  <tr>
	<th>Parameter Name</th>
	<th>Type</th>
	<th>Required</th>
	<th>Description</th>
  </tr>
  <tr>
	<td>SecretId</td>
	<td>String</td>
	<td>Yes</td>
	<td>SecretId for your account to access APIs. For more information, see  
	<a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td>
  </tr>
  <tr>
	<td>SecretKey</td>
	<td>String</td>
	<td>Yes</td>
	<td>SecretKey for your account to access APIs. For more information, see  
	<a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td>
  </tr>
  <tr>
	<td>Region</td>
	<td>String</td>
	<td>Yes</td>
	<td>Region of the destination CVM. Only the region is required, not the AZ. For more information about the values, see  
	<a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and AZs</a>.</td>
  </tr>
  <tr>
	<td>InstanceId</td>
	<td>String</td>
	<td>Yes</td>
	<td>Instance ID of the destination CVM, which is in the format of 
	<code>ins-xxxxxxxx</code>.</td>
  </tr>
  <tr>
	<td>DataDisks</td>
	<td>Array</td>
	<td>No</td>
	<td>List of data disks to be migrated from the source server. Each element indicates a data disk. A maximum of 20 data disks are supported.</td>
  </tr>
  <tr>
	<td>DataDisks.Index</td>
	<td>Integer</td>
	<td>No</td>
	<td>The serial number of data disk ranges from 1 to 20. If the value is <code>1</code>, it indicates that the data disk is the first one to be migrated and attached to the destination CVM; if the value is <code >2</code>, it indicates that the data disk is the second one to be migrated and attached to the destination CVM, and so on.</td>
  </tr>
  <tr>
	<td>DataDisks.Size</td>
	<td>Integer</td>
	<td>No</td>
	<td>Size of the source data disk in GB. The value range is [10,16000].</td>
  </tr>
  <tr>
	<td>DataDisks.MountPoint</td>
	<td>String</td>
	<td>No</td>
	<td>Mount point of the source data disk, such as 
	<code>&quot;/mnt/disk1&quot;</code>.</td>
  </tr>
</table>

You can refer to the following examples to modify the configuration file based on the actual business scenarios.
 - Example 1: To migrate a Linux source server to a CVM located in Guangzhou, configure the `user.json` file as follows:
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
} 
```
 - Example 2: A Linux source server has one data disk, of which the mount point is `/mnt/disk1`, and the size is `10` GB. To migrate this server to a CVM (with at least one data disk attached) located in the Guangzhou region, configure the `user.json` file as follows:
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		}
	]
}
```
 - Example 3: A Linux source server has two data disks. The mount point for disk 1 is `/mnt/disk1`, and the size is `10` GB. The mount point for disk 2 is `/mnt/disk2`, and the size is `20` GB. To migrate this server to a CVM (with at least two data disks attached) located in Guangzhou, with disk 1 and disk 2 of the source server to be migrated to the first and second data disks of the destination CVM respectively, configure the `user.json` file as follows:
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		},
		{
			"Index": 2,
			"Size": 20,
			"MountPoint": "/mnt/disk2"
		}
	]
}  
```

### Parameters in the client.json file[](id:clientJsonState)

The client.json configuration file is described as below:

<table>
  <tr>
	<th>Parameter Name</th>
	<th>Type</th>
	<th>Required<br></th>
	<th>Description</th>
  </tr>
  <tr>
	<td>Client.ToolMode</td>
	<td>bool</td>
	<td>No</td>
	<td>Tool migration mode identifier, the value of which defaults to <code>false</code>. If migration via tool is needed, modify the value to <code>true</code> or add the <code>--no-console</code> parameter when running the tool. </td>
  </tr>
  <tr>
	<td>Client.Net.Mode</td>
	<td>Integer</td>
	<td>Yes</td>
	<td>Migration mode, the value of which defaults to <code>0</code>, indicating the public network migration. Valid values: <code>0</code> (<a href="https://intl.cloud.tencent.com/document/product/213/44340">Public network migration mode</a>), <code>1</code> (<a href="https://intl.cloud.tencent.com/document/product/213/44340">Private network migration mode: Scenario 1</a>), <code>2</code> (<a href="https://intl.cloud.tencent.com/document/product/213/44340">Private network migration mode: Scenario 2</a>), <code>3</code> (<a href="https://intl.cloud.tencent.com/document/product/213/44340">Private network migration mode: Scenario 3</a>).</td>
  </tr>
  <tr>
	<td>Client.Extra.IgnoreCheck</td>
	<td>Bool</td>
	<td>No</td>
	<td>The default value is <code>false</code>. By default, the migration tool automatically checks the source server environment when the tool starts running. To skip the check, set this parameter to <code>true</code>.</td>
  </tr>
  <tr>
	<td>Client.Rsync.BandwidthLimit</td>
	<td>String</td>
	<td>No</td>
	<td>Bandwidth limit in KBytes/s, which is empty by default, i.e., no limit during transfer.</td>
  </tr>
  <tr>
	<td>Client.Rsync.Checksum</td>
	<td>Bool</td>
	<td>No</td>
	<td>Transfer verification. Setting this parameter to <code>true</code> can enhance the transfer consistency verification, but it will increase the CPU load of the source server 
	and slow down the transfer speed. The default value is <code>false</code>, which means no verification by default. </td>
  </tr>
</table>

If neither the source server or destination CVM can access the public network directly, you can establish a connection between them through [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216) and then migrate via the private network mode. Determine the appropriate migration mode according to the network environment of your source server and destination CVM.

### rsync\_excludes\_linux.txt file description[](id:_linuxTxtState)

This file is used to exclude files on the Linux source server or configuration files under specified directories that do not need to be migrated. By default, the rsync\_excludes\_linux.txt file already excludes the following directories and files. **Do not delete or modify the existing configurations.**
```shellsession
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
To exclude other directories or files, append them to the rsync\_excludes\_linux.txt file. For example, to exclude all content on the data disk attached to `/mnt/disk1`, configure the rsync\_excludes\_linux.txt file as follows:
```shellsession
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
/mnt/disk1/*
```

### Parameters of the migration tool

<table>
<thead>
<tr>
<th width="18%">Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>--help</code></td>
<td>Prints help information.</td>
</tr>
<tr>
<td><code>--no-console</code></td>
<td>Only migrates via tool (not migration in console).</td>
</tr>
<tr>
<td><code>--check</code></td>
<td>Checks the source server</td>
</tr>
<tr>
<td><code>--log-file</code></td>
<td>Configures the log file name, which is <code>log</code> by default.</td>
</tr>
<tr>
<td><code>--log-level</code></td>
<td>Configures the logging level. Valid values: <code>1</code>(ERROR level), <code>2</code> (INFO level) and <code>3</code>(DEBUG level). Default value: <code>2</code>.</td>
</tr>
<tr>
<td><code>--clean</code></td>
<td>Forces the destination CVM to exit the migration mode and cleans up the site. For example, if the console prompts "Please execute '--clean' option manually.", you need to use this parameter to force the destination CVM to exit the migration mode.</td>
</tr>
<tr>
<td><code>--version</code></td>
<td>Prints the version number.</td>
</tr>
</tbody>
</table>


## Migration Directions

### Data Backup
- Source server: You can use the source server snapshot feature or other methods to back up data.
- Destination CVM: You can create a snapshot as instructed in [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.


### Checking Before the Migration
Before migration, you need to check the source server and destination CVM separately as detailed below:
<table>
  <tr>
	<th style="width: 15%;">Destination CVM</th>
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
</table>

<dx-alert infotype="explain" title="">
- You can use tool commands such as `./go2tencentcloud_x64 --no-console --check` to automatically check the source server.
- By default, the go2tencentcloud migration tool automatically performs checks upon launch. To skip checks and perform forced migration, configure `Client.Extra.IgnoreCheck` to `true` in the client.json file.
</dx-alert>


### Starting migration

If you use go2tencentcloud supporting checkpoint restart provided by Tencent Cloud for migration, the migration process includes the following three stages. You can intuitively view the migration progress when the tool is running.

- **Stage 1**: The destination CVM enters the migration mode, and is ready for migration.
- **Stage 2**: The destination CVM is in the migration mode, and receives data migrated.
- **Stage 3**: The destination CVM exits the migration mode, and the migration completes.

Each stage will generate some subtasks to perform related operations, and some time-consuming subtasks may have maximum timeout periods by default. The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to complete.
<dx-alert infotype="notice" title="">
The destination CVM enters migration mode after the migration starts. Do not reinstall the system, shut down, terminate, or reset passwords of the destination CVM until the migration is completed and the destination CVM exits the migration mode. 
</dx-alert>

<dx-tabs>

:::  Public network

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
2. In the `user.json` file, configure the destination CVM for the migration.
Configure the required parameters based on the [description of parameters in the user.json file](#userJsonState).
3. In the `client.json` file, configure the migration mode and other parameters.
Configure `Client.ToolMode` in the `client.json` file to `true`, that is, select the migration via tool. If necessary, configure other parameters based on the description of [Parameters in the client.json file](#clientJsonState).
4. (Optional) Exclude files and directories on the source server that do not need to be migrated.
Add files or directories that do not need to be migrated from the Linux source server to [rsync_excludes_linux.txt file](#_linuxTxtState).
5. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as the root user to run the tool.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
If you have not modified `Client.ToolMode` in the client.json to `true`, you need to add the parameter `--no-console` when running the tool, as shown below:
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
After the tool runs, wait patiently for the migration to end. Generally, the console output of a successful public network migration is shown below:
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

:::
:::  Private network (Scenario 1)

1. Establish a connection between the source server and the destination CVM.
- Establish a connection between the source server and the destination CVM by using [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), or [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
2. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
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
3. In the `user.json` file, configure the destination CVM for the migration.
Configure the required parameters based on the description of [Parameters in the user.json file](#userJsonState).
4. In the `client.json` file, configure the migration mode and other parameters.
   - Set the `Client.ToolMode` value in the `client.json` file to `true`, that is, select the migration via tool.
   - Set the `Client.Net.Mode` in the `client.json` file to `1`, that is, select the [Private network migration mode: Scenario 1](https://intl.cloud.tencent.com/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F ) to migrate. If necessary, configure other parameters based on the description of [Parameters in the client.json file](#clientJsonState).
5. (Optional) Exclude files and directories on the source server that do not need to be migrated.
Add files or directories that do not need to be migrated from the Linux source server to [rsync_excludes_linux.txt file](#_linuxTxtState).
6. [](id:Scenario1_step06)Run the tool on a server (such as the gateway) that can access the public network.
For example, on a server that can access the public network, execute the following command to run the tool for migration stage 1.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
If you have not modified `Client.ToolMode` in the client.json to `true`, you need to add the parameter `--no-console` when running the tool, as shown below:
```shell
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
If `Stage 1 is finished and please run next stage at source machine.` is prompted, stage 1 has been completed, as shown below:
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
7. [](id:Scenario1_step07)Run the tool on the source server to be migrated.
After [step 6](#Scenario1_step06) (stage 1) is completed, copy the entire tool directory in stage 1 to the source server, and then run the tool for migration stage 2.
Execute the following command to run the tool for migration stage 2.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
If you have not modified `Client.ToolMode` in the client.json to `true`, you need to add the parameter `--no-console` when running the tool, as shown below:
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
If `Stage 2 is finished and please run next stage at gateway machine.` is prompted, stage 2 has been completed, as shown below:
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
8. Run the tool on a server (such as the gateway) that can access the public network.
After [step 7](#Scenario1_step07) (stage 2) is completed, copy the entire tool directory in stage 2 to the source server in stage 1, and then run the tool for migration stage 3.
Execute the following command to run the tool for migration stage 3.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
If you have not modified `Client.ToolMode` in the client.json to `true`, you need to add the parameter `--no-console` when running the tool, as shown below:
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
If `Migrate successfully` is prompted, the entire migration task has been completed, as shown below:
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)




:::
:::  Private network (Scenario 2)

1. Establish a connection between the source server and the destination CVM.
- Establish a connection between the source server and the destination CVM by using [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), or [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
2. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
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
3. In the `user.json` file, configure the destination CVM for the migration.
Configure the required parameters based on the [description of parameters in the user.json file](#userJsonState).
4. In the `client.json` file, configure the migration mode and other parameters.
    - Set the `Client.ToolMode` value in the `client.json` file to `true`, that is, select the migration via tool.
    - Set the `Client.Net.Mode` in the `client.json` file to `2`, that is, select the [Private network migration mode: Scenario 2](https://intl.cloud.tencent.com/ document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F ) to migrate. If necessary, configure other parameters based on the description of [Parameters in the client.json file](#clientJsonState).
5. (Optional) Exclude files and directories on the source server that do not need to be migrated.
Add files or directories that do not need to be migrated from the Linux source server to [rsync_excludes_linux.txt file](#_linuxTxtState).
6. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as the root user to run the tool.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
If you have not modified `Client.ToolMode` in the client.json to `true`, you need to add the parameter `--no-console` when running the tool, as shown below:
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
After the tool runs, wait patiently for the migration to end. Generally, the console output of a successful migration is shown below: ![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png).




:::
:::  Private network (Scenario 3)
1. Establish a connection between the source server and the destination CVM.
- Establish a connection between the source server and the destination CVM by using [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), or [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
2. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
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
3. In the `user.json` file, configure the destination CVM for the migration.
Configure the required parameters based on the description of [Parameters in the user.json file](#userJsonState).
4. In the `client.json` file, configure the migration mode and other parameters.
    - Set the `Client.ToolMode` value in the `client.json` file to `true`, that is, select the migration via tool.
    - Set the `Client.Net.Mode` in the `client.json` file to `3`, that is, select the [Private network migration mode: Scenario 3](https://intl.cloud.tencent.com/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F ) to migrate.
    - Set the `Client.Net.Proxy.Ip` and `Client.Net.Proxy.Port` in the `client.json` file to the IP address and port of the network proxy. If your network proxy needs to be verified, enter the username and password of the network proxy in `Client.Net.Proxy.User` and `Client.Net.Proxy.Password`. If not necessary, leave the two items empty. 
		If necessary, configure other parameters based on the description of [Parameters in the client.json file](#clientJsonState).
5. (Optional) Exclude files and directories on the source server that do not need to be migrated.
Add files or directories that do not need to be migrated from the Linux source server to [rsync_excludes_linux.txt file](#_linuxTxtState).
6. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as the root user to run the tool.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
If you have not modified `Client.ToolMode` in the client.json to `true`, you need to add the parameter `--no-console` when running the tool, as shown below:
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
After the tool runs, wait patiently for the migration to end. Generally, the console output of a successful migration is shown below:
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)

:::

</dx-tabs>


### Checking after the Migration

- If the migration fails, check the error information in log files (under the migration tool directory by default), operation guides, or FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting methods.
- If the migration is successful, check whether the target CVM starts up normally, whether data on the target CVM is consistent with that on the source server, and whether the network and other system services are normal.

If you have any questions or the migration has an exception, see FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [Contact Us](https://intl.cloud.tencent.com/document/product/213/34837).
