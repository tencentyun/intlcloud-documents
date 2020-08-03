## Overview
Online migration refers to migrating or synchronizing systems and applications on the source server or virtual machine from your IDCs or other cloud platforms to Tencent Cloud without system downtime.
Tencent Cloud provides the migration tool [go2tencentcloud](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip). After you run the migration tool on the source server, it can be migrated to the destination Cloud Virtual Machine (CVM) on Tencent Cloud. The migration tool migrates the source server directly onto the cloud and eliminates the need for you to prepare, upload, or import images. It meets business requirements for enterprise cloudification, cross-cloud migration, cross-account or cross-region migration, and hybrid cloud deployment.

## Migration Tool

### Supported migration modes

<span id="DefaultMode"></span>
#### Default Mode
If both your source server and destination CVM can access the public network, you can use the default migration mode.
In the current default mode, the source server calls Tencent Cloud APIs through the Internet to initiate a migration request, and transfers data to the destination CVM to complete the migration.
![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)

#### Private network migration mode
If your source server or destination CVM is in a private network or Virtual Private Cloud (VPC) instance, the source server cannot directly establish a connection with the destination CVM through the Internet. In this case, you can use the private network migration mode of the tool. You need to establish a connection between the source server and the destination CVM using [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connection](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216).

- <span id="Scenario1">Scenario 1</span>: if your source server or destination CVM cannot access the public network, use a server (such as the gateway) that can access the public network to call Tencent Cloud APIs through the Internet to initiate a migration request. Then, transfer data to the destination CVM through the connection to complete the migration. This scenario requires neither the source server nor the destination CVM to be able to access the public network.
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- <span id="Scenario2">Scenario 2</span>: if your source server can access the public network, use the source server to call Tencent Cloud APIs through the Internet to initiate a migration request. Then, transfer data to the destination CVM through the connection to complete the migration. This scenario requires the source server, but not the destination CVM, to be able to access the public network.
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- <span id="Scenario3">Scenario 3</span>: if your source server can access the public network through a proxy, use the source server to call Tencent Cloud APIs through the network proxy to initiate a migration request. Then, transfer data to the destination CVM through the connection to complete the migration. This scenario requires both the source server and the destination CVM to be able to access the public network.
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)

### Supported operating systems
Operating systems supported by the online migration tool include but are not limited to the following (32-bit or 64-bit):
<table>
	<tr><th>Linux</th><th>Windows</th></tr>
	<tr><td>CentOS 5/6/7</td><td rowspan=7>-</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18</td></tr>
	<tr><td>Debian 7/8/9</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

### Compressed package files

<table>
	<tr><th>File Name</th><th>Description</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>Executable program of the migration tool for the 64-bit Linux operating system</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>Executable program of the migration tool for the 32-bit Linux operating system</td></tr>
	<tr><td>user.json</td><td>Configuration file of the source server and destination CVM during migration. You need to modify the configurations based on <a href="#userJsonState">description of user.json file parameters</a>.</td></tr>
	<tr><td>client.json</td><td>Configuration file of the migration tool. You need to modify the configurations based on <a href="#clientJsonState">description of client.json file parameters</a>.</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync configuration file, which excludes files and directories that do not need to be migrated in the Linux system</td></tr>
</table>

> The configuration files cannot be deleted and must be stored under the same directory level as the go2tencentcloud executable program. 
>

- <span id="userJsonState">Description of user.json file parameters:</span>
<table>
	<tr><th>Parameter</th><th>Type</th><th>Required</th><th>Description</th></tr>
	<tr><td>SecretId</td><td>String</td><td>Yes</td><td>Secret ID for your account to access APIs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>Yes</td><td>Secret key for your account to access APIs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td></tr>
	<tr><td>Region</td><td>String</td><td>Yes</td><td>Region of the destination CVM. You need to specify the region, but not the availability zone. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and Availability Zones</a>.</td></tr>
	<tr><td>InstanceId</td><td>String</td><td>Yes</td><td>Instance ID of the destination CVM. The ID format is <code>ins-xxxxxxxx</code>.</td></tr>
	<tr><td>DataDisks</td><td>Array</td><td>No</td><td>List of data disks to be migrated from the source server. Each entry represents one data disk, and up to 20 data disks are supported.</td></tr>
	<tr><td>DataDisks.Index</td><td>Integer</td><td>Yes</td><td>Serial number of the data disk on the source server. Value range: [1,20]. The value <code>1</code> indicates that this data disk will be migrated to the first data disk on the destination CVM.</td></tr>
	<tr><td>DataDisks.Size</td><td>Integer</td><td>Yes</td><td>Size of the data disk on the source server. Unit: GB. Value range: [10,16000].</td></tr>
	<tr><td>DataDisks.MountPoint</td><td>String</td><td>Yes</td><td>Mount target of the data disk on the source server, for example, <code>"/mnt/disk1"</code>.</td></tr>
</table>
Example 1: To migrate a Linux source server to a CVM located in Guangzhou, configure the user.json file as follows:

 ```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
}  
```
> You need to replace the parameters with the actual values.
>
Example 2: A Linux source server has one data disk, the mount target is `/mnt/disk1`, and the size of the data disk is `10` GB. To migrate this server to a CVM located in Guangzhou, configure the user.json file as follows:
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
> You need to replace the parameters with the actual values.
>
- <span id="clientJsonState">Description of client.json file parameters:</span>
<table>
	<tr><th>Parameter</th><th>Type</th><th>Required</th><th>Description</th></tr>
	<tr><td>Client.Net.Mode</td><td>Integer</td><td>Yes</td><td>Default value: <code>0</code>. Valid values:<code>0</code> (<a href="#DefaultMode">default mode)</a>), <code>1</code> (<a href="#Scenario1">private network migration mode: scenario 1</a>), <code>2</code> (<a href="#Scenario2">private network migration mode: scenario 2</a>), <code>3</code> (<a href="#Scenario3">private network migration mode: scenario 3</a>). Choose a value based on your actual migration modes or scenarios.</td></tr>
	<tr><td>Client.Net.Proxy.Ip</td><td>String</td><td>No</td><td>IP address of the network proxy. If you select <a href="#Scenario3">private network migration mode: scenario 3</a>, this parameter must be specified.</td></tr>
	<tr><td>Client.Net.Proxy.Port</td><td>Integer</td><td>No</td><td>Port of the network proxy. If you select <a href="#Scenario3">private network migration mode: scenario 3</a>, this parameter must be specified.</td></tr>
	<tr><td>Client.Net.Proxy.User</td><td>String</td><td>No</td><td>Username of the network proxy. If you select <a href="#Scenario3">private network migration mode: scenario 3</a>, and the network proxy needs to be authenticated, this parameter must be specified.</td></tr>
	<tr><td>Client.Net.Proxy.Password</td><td>String</td><td>No</td><td>Password of the network proxy. If you select <a href="#Scenario3">private network migration mode: scenario 3</a>, and the network proxy needs to be authenticated, this parameter must be specified.</td></tr>
	<tr><td>Client.Extra.IgnoreCheck</td><td>Bool</td><td>No</td><td>Default value: <code>false</code>. Upon launch, the migration tool automatically checks the environment of the source server. To skip this check, configure this parameter to <code>true</code>.</td></tr>
</table>

- <span id="_linuxTxtState">Description of rsync\_excludes\_linux.txt file parameters:</span>
This file excludes files on the Linux source server that do not need to be migrated, or configuration files under specified directories. By default, the file already excludes the following directories and files. **Do not delete or modify them.**
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
To exclude other directories or files, append them to the rsync\_excludes\_linux.txt file. For example, to exclude all content on the data disk mounted on `/mnt/disk1`, configure the rsync\_excludes\_linux.txt file as follows:
```sh
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
Parameter | Description
---|---
`--help` | Prints help information.
`--check` | Checks the source server without migration.
`--log-file` | Configures the log file name, which is `log` by default.
`--log-level` | Configures the logging level. Valid values: `1` (ERROR level), `2` (INFO level), and `3` (DEBUG level). Default value: `2`.
`--clean` | Enables the destination CVM to forcibly exit the migration mode and cleanse the site. For example, if the console prompts `Please execute '--clean' option manually.`, you need to specify this parameter and run the tool for the destination CVM to exit the migration mode.
`--version` | Prints the version number.

## Pre-Migration Checks
Before migration, check the following items of the source server and destination CVM:
<table>
	<tr><th style="width: 15%;">Destination CVM</th><td><ol  style="margin: 0;"><li>Storage: cloud disks (including system disks and data disks) of the destination CVM must have sufficient storage to store data from the source server.</li><li>Security group: ports 443 and 80 must be open in a security group.</li><li>Bandwidth: we recommend increasing the bandwidth for faster migration. The traffic consumed during migration will be approximately equal to the data volume. Change your network billing method in advance if needed.</li><li>Operating system: we recommend that the destination CVM and the source server use the same operating system. Otherwise, the images created later may be inconsistent with the actual operating system. For example, when you migrate a source server with the CentOS 7 system, choose a destination CVM with the CentOS 7 system.</li></ol></td></tr>
	<tr><th>Linux source server</th><td><ol  style="margin: 0;"><li>Check and install virtIO. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking VirtIO Drivers in Linux</a>.</li><li>Check whether rsync and grub2-install (or grub-install) are installed.</li><li>Check whether SELinux is enabled. If yes, disable it.</li><li>When a migration request is sent to the Tencent Cloud API, the API checks the generated token based on the current UNIX time. Make sure that the current system time is correct.</li></ol></td></tr>
</table>

> 
> - You can use tool commands to automatically check the source server, for example, `sudo ./go2tencentcloud_x64 --check`.
> - By default, the go2tencentcloud migration tool performs checks automatically upon launch. To skip the check and migrate forcibly, configure the `Client.Extra.IgnoreCheck` field to `true` in the client.json file.
> 

## Migration Directions
If you use go2tencentcloud provided by Tencent Cloud for migration, the migration process includes the following three stages. You can intuitively view the migration progress when the tool is running.
- **Stage 1**: initialize the remote instance.
- **Stage 2**: transfer data.
- **Stage 3**: release the remote instance.

Each stage will generate some subtasks to perform related operations, and some time-consuming subtasks may have a maximum timeout period by default. The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. The migration tool supports resumable data transfer.

> The destination CVM enters migration mode after the migration starts. Do not reinstall the system, shut down, terminate, or reset passwords of the destination CVM until the migration is completed and the destination CVM exits the migration mode. 
>

### Migration directions in default mode

1. In the user.json file, configure the source server and destination CVM for the migration.
Configure the required parameters based on [description of user.json file parameters](#userJsonState).
2. In the client.json file, configure the migration mode and other parameters.
Configure `Client.Net.Mode` in the client.json file to `0`, that is, use the [default mode](#DefaultMode). If needed, configure other parameters based on [description of client.json file parameters](#clientJsonState).
3. (Optional) Exclude files and directories on the source server that do not need to be migrated.
If you need to exclude some files and directories that do not need to be migrated when migrating the Linux source server, append them to the [rsync\_excludes\_linux.txt file](#_linuxTxtState).
4. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as the root user to run the tool.
```
sudo ./go2tencentcloud_x64
```
To configure the log file name and logging level when running the tool, execute the following command:
```
sudo ./go2tencentcloud --log-file=my.log --log-level=3
```
Wait for the migration process to complete. 
If the migration in default mode succeeds, the console outpMigrateut is as follows:
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

### Migration directions in private network migration mode

#### Scenario 1
1. Establish a connection between the source server and the destination CVM.
Establish a connection between the source server and the destination CVM using [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN connection](https://intl.cloud.tencent.com/document/product/1037), or [CCN](https://intl.cloud.tencent.com/document/product/1003).
2. In the user.json file, configure the source server and destination CVM for the migration.
 Configure the required parameters based on [description of user.json file parameters](#userJsonState).
3. In the client.json file, configure the migration mode and other parameters.
Configure `Client.Net.Mode` in the client.json file to `1`, that is, use the [private network migration mode: scenario 1](#Scenario1). If necessary, configure other parameters based on [description of client.json file parameters](#clientJsonState).
4. (Optional) Exclude files and directories on the source server that do not need to be migrated.
If you need to exclude some files and directories that do not need to be migrated when migrating the Linux source server, append them to the [rsync_excludes_linux.txt file](#_linuxTxtState).
5. <span id="Scenario1_step05">Run the tool on a server (such as the gateway) that can access the public network.</span>
For example, on a server that can access the public network, execute the following command to run the tool for migration stage 1.
```
sudo ./go2tencentcloud_x64
```
If `Stage 1 is finished and please run next stage at source machine` is prompted, stage 1 is completed.
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
6. <span id="Scenario1_step06">Run the tool on the source server.</span>
After [step 5](#Scenario1_step05) (stage 1) is completed, copy the entire tool directory in stage 1 to the source server, and then run the tool for migration stage 2.
Execute the following command to run the tool for migration stage 2.
```
sudo ./go2tencentcloud_x64
```
If `Stage 2 is finished and please run next stage at gateway machine` is prompted, stage 2 is completed.
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
7. Run the tool on a server (such as the gateway) that can access the public network.
After [step 6](#Scenario1_step06) (stage 2) is completed, copy the entire tool directory in stage 2 to the server in stage 1, and then run the tool for migration stage 3.
Execute the following command to run the tool for migration stage 3.
```
sudo ./go2tencentcloud_x64
```
If `Migrate successfully` is prompted, the entire migration task is completed.
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)
   
#### Scenario 2

1. Establish a connection between the source server and the destination CVM.
Establish a connection between the source server and the destination CVM using [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN connection](https://intl.cloud.tencent.com/document/product/1037), or [CCN](https://intl.cloud.tencent.com/document/product/1003).
2. In the user.json file, configure the source server and destination CVM for the migration.
 Configure the required parameters based on [description of user.json file parameters](#userJsonState).
3. In the client.json file, configure the migration mode and other parameters.
 Configure `Client.Net.Mode` in the client.json file to `2`, that is, use the [private network migration mode: scenario 2](#Scenario2). If necessary, configure other parameters based on [description of client.json file parameters](#clientJsonState).
4. (Optional) Exclude files and directories on the source server that do not need to be migrated.
If you need to exclude some files and directories that do not need to be migrated when migrating the Linux source server, append them to the [rsync_excludes_linux.txt file](#_linuxTxtState).
5. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as the root user to run the tool.
```
sudo ./go2tencentcloud_x64
```
Wait for the migration process to complete.
If the migration is successful, the console output is as follows:
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)
  
#### Scenario 3

1. Establish a connection between the source server and the destination CVM.
 Establish a connection between the source server and the destination CVM using [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN connection](https://intl.cloud.tencent.com/document/product/1037), or [CCN](https://intl.cloud.tencent.com/document/product/1003).
2. In the user.json file, configure the source server and destination CVM for the migration.
Configure the required parameters based on [description of user.json file parameters](#userJsonState).
3. In the client.json file, configure the migration mode and other parameters.
 1. Configure `Client.Net.Mode` in the client.json file to `3`, that is, use the [private network migration mode: scenario 3](#Scenario3).
 2. Configure `Client.Net.Proxy.Ip` and `Client.Net.Proxy.Port` in the client.json file to the IP address and port of the network proxy, respectively.
If your network proxy needs to be authenticated, enter the username and password of the network proxy in `Client.Net.Proxy.User` and `Client.Net.Proxy.Password`, respectively. You can leave them in blank if authentication is not required. If necessary, you can configure other parameters based on [description of client.json file parameters](#clientJsonState).
4. (Optional) Exclude files and directories on the source server that do not need to be migrated.
If you need to exclude some files and directories that do not need to be migrated when migrating the Linux source server, append them to the [rsync_excludes_linux.txt file](#_linuxTxtState).
5. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as the root user to run the tool.
```
sudo ./go2tencentcloud_x64
```
Wait for the migration process to complete.
If the migration is successful, the console output is as follows:
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)


## Post-Migration Checks
1. If the migration fails, check the error information in log files (under the migration tool directory by default), operation guides, or [About Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting methods.
2. If the migration succeeds, check whether the destination CVM can be launched normally, whether data on the destination CVM is consistent with that on the source server, whether the network is normal, whether other services are running normally, etc.
3. If you have any questions or the migration has an exception, see [About Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [submit a ticket](https://console.cloud.tencent.com/workorder/category).
