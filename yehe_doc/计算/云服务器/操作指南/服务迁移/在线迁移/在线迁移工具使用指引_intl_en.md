## Overview
Online migration refers to migrating or synchronizing the system and applications on the server or virtual machine from your own IDC, cloud platform, or other source environments to Tencent Cloud without interrupting the system.
Tencent Cloud provides the migration tool [go2tencentcloud](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip). After you run the migration tool on the source server, the entire source server can be migrated to the destination Cloud Virtual Machine (CVM) on Tencent Cloud. With this migration tool, you do not need to prepare, upload, or import images. The source server is directed migrated onto the cloud, which meets service requirements for enterprise cloudification, migration across cloud platforms, migration across accounts or regions, and hybrid cloud deployment.

## Migration Tool

### Supported migration modes

<span id="DefaultMode"></span>
#### Default mode
If both your source server and destination CVM can access the public network, you can use the default migration mode.
In the current default mode, the source server calls the Tencent Cloud APIs through Internet to initiate a migration request, and transfers data to the destination CVM to complete the migration.
![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)

#### Private network migration mode
If your source server or destination CVM is located in a private network or Virtual Private Cloud (VPC), the source server cannot directly set up a connection with the destination CVM through Internet. In this case, you can use the private network migration mode of the tool. If this migration mode is used, you need to set up a connection between the source server and destination CVM by using [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connection](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network ](https://intl.cloud.tencent.com/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216).

- <span id="Scenario1">Scenario 1</span>: if your source server or destination CVM cannot access the public network, use a server (such as the gateway) that can access the public network to call the Tencent Cloud APIs through Internet to initiate a migration request, and then transfer data to the destination CVM through the connection to complete the migration. In this scenario, the source server and destination CVM do not need to have the capability to access the public network.
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- <span id="Scenario2">Scenario 2</span>: if your source server can access the public network, use the source server to call the Tencent Cloud APIs through Internet to initiate a migration request, and then transfer data to the destination CVM through the connection to complete the migration. In this scenario, the source server must have the capability to access the public network, but the destination CVM does not need to have this capability.
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- <span id="Scenario3">Scenario 3</span>: if your source server can access the public network through a proxy, use the source server to call the Tencent Cloud APIs through the network proxy to initiate a migration request, and then transfer data to the destination CVM through the connection to complete the migration. In this scenario, the source server and destination CVM do not need to have the capability to access the public network.
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)

### Supported operating systems
Operating systems supported by the online migration tool include but are not limited to the following (32-bit or 64-bit):
<table>
	<tr><th>Linux Operating System</th><th>Windows Operating System</th></tr>
	<tr><td>CentOS 5/6/7</td><td rowspan=7>-</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18</td></tr>
	<tr><td>Debian 7/8/9</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

### Files in the compressed package

<table>
	<tr><th>File Name</th><th>Description</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>Executable program of the migration tool for the 64-bit Linux operating system.</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>Executable program of the migration tool for the 32-bit Linux operating system.</td></tr>
	<tr><td>user.json</td><td>Configuration file of the source server and destination CVM during the migration. You need to modify the configurations based on the <a href="#userJsonState">description of parameters in the user.json file</a>.</td></tr>
	<tr><td>client.json</td><td>Configuration file of the migration tool. You need to modify the configurations based on the <a href="#clientJsonState">description of parameters in the client.json file</a>.</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync configuration file, which excludes the files and directories that do not need to be migrated in the Linux system.</td></tr>
</table>

>? The configuration files cannot be deleted. You must store these files under the same folder as the go2tencentcloud executable program. 
>

- <span id="userJsonState">Description of parameters in the user.json file:</span>
<table>
	<tr><th>Parameter</th><th>Type</th><th>Required</th><th>Description</th></tr>
	<tr><td>SecretId</td><td>String</td><td>Yes</td><td>Secret ID used by your account to access APIs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>Yes</td><td>Secret key used by your account to access APIs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td></tr>
	<tr><td>Region</td><td>String</td><td>Yes</td><td>Region of the destination CVM. You only need to enter the region, but not the availability zone. For more information on values, see the <a href="https://intl.cloud.tencent.com/document/product/213/6091">region list</a>.</td></tr>
	<tr><td>InstanceId</td><td>String</td><td>Yes</td><td>Instance ID of the destination CVM. The format is <code>ins-xxxxxxxx</code>.</td></tr>
	<tr><td>DataDisks</td><td>Array</td><td>No</td><td>List of data disks to be migrated from the source server. Each element represents one data disk. Up to 20 data disks are supported.</td></tr>
	<tr><td>DataDisks.Index</td><td>Integer</td><td>Yes</td><td>Serial number of the data disk. Value range: [1,20]. The value <code>1</code> indicates that this data disk will be migrated to the first data disk mounted on the destination CVM. Likewise, the value <code>2</code> indicates that this data disk will be migrated to the second data disk mounted on the destination CVM.</td></tr>
	<tr><td>DataDisks.Size</td><td>Integer</td><td>Yes</td><td>Size of the data disk on the source server. Unit: GB. Value range: [10,16000].</td></tr>
	<tr><td>DataDisks.MountPoint</td><td>String</td><td>Yes</td><td>Mount point of the data disk on the source server, for example, <code>"/mnt/disk1"</code>.</td></tr>
</table>
Example 1: to migrate a source Linux server to a CVM located in Guangzhou, configure the user.json file as follows:

 ```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
}  
```
>? You need to replace the parameter values with the actual values.
>
For example, a source Linux server has one data disk, the mount target is `/mnt/disk1`, and the size of the data disk is `10` GB. To migrate this server to a CVM (with at least one data disk mounted) located in the Guangzhou region, configure the user.json file as follows:
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
For example, a source Linux server has two data disks. The mount target for disk 1 is `/mnt/disk1`, and the size is `10` GB. The mount target for disk 2 is `/mnt/disk2`, and the size is `20`GB. To migrate this server to a CVM (with at least two data disks mounted) located in Guangzhou, with disk 1 and disk 2 of the source server to be mounted to the first and second data disks of the destination CVM, respectively, configure the user.json file as follows:
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
>? You need to replace the parameter values with the actual values.
>
- <span id="clientJsonState">Description of parameters in the client.json file:</span>
<table>
	<tr><th>Parameter</th><th>Type</th><th>Required</th><th>Description</th></tr>
	<tr><td>Client.Net.Mode</td><td>Integer</td><td>Yes</td><td>Default value: <code>0</code>. Valid values:<code>0</code> (<a href="#DefaultMode">default mode)</a>), <code>1</code> (<a href="#Scenario1">private network migration mode: scenario 1</a>), <code>2</code> (<a href="#Scenario2">private network migration mode: scenario 2</a>), <code>3</code> (<a href="#Scenario3">private network migration mode: scenario 3</a>). Enter a value based on your actual migration mode or scenario.</td></tr>
	<tr><td>Client.Net.Proxy.Ip</td><td>String</td><td>No</td><td>IP address of the network proxy. If you select <a href="#Scenario3">private network migration mode: scenario 3</a>, this parameter must be specified.</td></tr>
	<tr><td>Client.Net.Proxy.Port</td><td>Integer</td><td>No</td><td>Port of the network proxy. If you select <a href="#Scenario3">private network migration mode: scenario 3</a>, this parameter must be specified.</td></tr>
	<tr><td>Client.Net.Proxy.User</td><td>String</td><td>No</td><td>Username of the network proxy. If you select <a href="#Scenario3">private network migration mode: scenario 3</a>, this parameter must be specified.</td></tr>
	<tr><td>Client.Net.Proxy.Password</td><td>String</td><td>No</td><td>Password of the network proxy. If you select <a href="#Scenario3">private network migration mode: scenario 3</a>, this parameter must be specified.</td></tr>
	<tr><td>Client.Extra.IgnoreCheck</td><td>Bool</td><td>No</td><td>Default value: <code>false</code>. When started, the migration tool automatically checks the environment of the source server. If you need to skip this check, set this parameter to <code>true</code>.</td></tr>
	<tr><td>Client.Rsync.BandwidthLimit</td><td>String</td><td>No</td><td>Bandwidth limit in KBytes/s. The default value is empty, meaning that there is no bandwidth limit to transfer.</td></tr>
	<tr><td>Client.Rsync.Checksum</td><td>Bool</td><td>No</td><td>Transfer checksum. Setting it to <code>true</code> can strengthen transfer consistency check but will increase the CPU load of the source server and slow down the transfer speed. The default value is <code>false</code>, meaning that by default, no check is performed.</td></tr>
</table>
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>Note: </p><p>Apart from the above parameters, other configuration items in the client.json file usually do not need to be specified.</p>
</blockquote>
- <span id="_linuxTxtState">Description of the rsync\_excludes\_linux.txt file:</span>
This file is used to exclude files or configuration files under specified directories on the source Linux server, which do not need to be migrated. By default, the rsync\_excludes\_linux.txt file already excludes the following directories and files. **Do not delete these settings.**
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
If you need to exclude other directories or files, add them at the end of the rsync\_excludes\_linux.txt file. For example, to exclude all content of the data disk mounted on `/mnt/disk1`, configure the rsync\_excludes\_linux.txt file as follows:
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
`--help`| Prints the help information.
`--check`| Checks the source server without performing the migration.
`--log-file`| Sets the log file name, which is `log` by default.
`--log-level`| Sets the log output level. Valid values: `1` (ERROR level), `2`（INFO level), and `3` (DEBUG level). Default value: `2`.
`--clean`| Enables the destination CVM to forcibly exit the migration mode an cleans the site. For example, if `Please execute '--clean' option manually.` is displayed on the console, you need to specify this parameter and run the tool so that the destination CVM exits the migration mode.
`--version`| Prints the version number.

## Checks Before Migration
Before the migration, check the following items of the source server and destination CVM:
<table>
	<tr><th style="width: 15%;">Destination CVM</th><td><ol  style="margin: 0;"><li>Storage: the storage space in its cloud disks (including system disks and data disks) must be sufficient to store the data from the source server.</li><li>Security group: the 443 and 80 ports must be open to the Internet in a security group.</li><li>Bandwidth: we recommend that you increase inbound and outbound bandwidth for faster migration. The traffic consumed during migration will be approximately equal to the data volume. If needed, change your network billing method in advance.</li><li>Operating system: it is recommended that you use the same operating system on both the source server and the destination CVM. Different operating systems will result in inconsistency between the image that will be created later and the actual operating system. For example, when migrating a source server with the CentOS 7 system installed, choose a CVM with the CentOS 7 system installed as the migration destination.</li></ol></td></tr>
	<tr><th>Linux source server</th><td><ol  style="margin: 0;"><li>Check for and install Virtio. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>.</li><li>Check whether rsync is installed by running <code>which rsync</code> for verification. </li><li>Check whether SELinux is enabled. If yes, disable it.</li><li>Ensure the current system time is correct, because the Tencent Cloud API will use the UNIX timestamp to check against the generated token after receiving a migration request.</li></ol></td></tr>
</table>

>? 
> - You can use tool commands such as `sudo ./go2tencentcloud_x64 --check` to automatically check the source server.
> - By default, the go2tencentcloud migration tool automatically performs checking when it is started. If you want to skip the checks and directly perform migration, set `Client.Extra.IgnoreCheck` to `true` in the client.json file.
> 

## Migration Directions
If you use go2tencentcloud provided by Tencent Cloud, the entire migration process is completed in three stages. You can learn the migration progress from the tool when the tool is running.
- **Stage 1**: initialize the remote instance.
- **Stage 2**: transfer data.
- **Stage 3**: release the remote instance.

In each stage, some subtasks are generated to execute related operations. Some time-consuming subtasks also have the maximum timeout by default. The time required for data transfer depends on the size of the data on the source server and network bandwidth. The migration tool supports checkpoint restart of data transfer.

>! After the migration starts, the destination CVM enters the migration mode. Therefore, do not perform the following operations on the destination CVM until the migration is completed and the destination CVM exits the migration mode: system reinstallation, shutdown, termination, and password reset. 
>

### Migration directions in default mode

1. In the user.json file, configure the source server and destination CVM for the migration.
Configure the required parameters based on the [description of parameters in the user.json file](#userJsonState).
2. In the client.json file, configure the migration mode and other parameters.
Set `Client.Net.Mode` in the client.json file to `0`, that is, select the [default mode](#DefaultMode). If necessary, configure other parameters based on [description of parameters in the client.json file](#clientJsonState).
3. (Optional) Exclude files and directories on the source server that do not need to be migrated.
When migrating the source Linux server, if you need to exclude some files and directories that do not need to be migrated, add these files and directories at the end of the [rsync\_excludes\_linux.txt file](#_linuxTxtState).
4. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as `root` to run the tool.
```
sudo ./go2tencentcloud_x64
```
If you need to set the log file name and log output level when running the tool, use the following command:
```
sudo ./go2tencentcloud --log-file=my.log --log-level=3
```
Please wait for the migration process to complete. 
If the migration succeeds in default mode, the console output is as follows:
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

### Migration directions in private network migration mode

#### Scenario 1
1. Set up a connection between the source server and the destination CVM.
Set up a connection between the source server and the destination CVM by using [VPC peering connection](https://intl.cloud.tencent.com/document/product/553), [VPN connection](https://intl.cloud.tencent.com/document/product/1037), or [CCN](https://intl.cloud.tencent.com/document/product/1003).
2. In the user.json file, configure the source server and destination CVM for the migration.
 Configure the required parameters based on the [description of parameters in the user.json file](#userJsonState).
3. In the client.json file, configure the migration mode and other parameters.
Set `Client.Net.Mode` in the client.json file to `1`, that is, select the [private network migration mode: scenario 1](#Scenario1). If necessary, configure other parameters based on [description of parameters in the client.json file](#clientJsonState).
4. (Optional) Exclude files and directories on the source server that do not need to be migrated.
When migrating the source Linux server, if you need to exclude some files and directories that do not need to be migrated, add these files and directories at the end of the [rsync_excludes_linux.txt file](#_linuxTxtState).
5. <span id="Scenario1_step05">Run the tool on a server (such as the gateway) that can access the public network.</span>
For example, on a server that can access the public network, execute the following command to run the tool for migration stage 1.
```
sudo ./go2tencentcloud_x64
```
If the `Stage 1 is finished and please run next stage at source machine.` prompt appears, stage 1 has been completed.
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
6. <span id="Scenario1_step06">Run the tool on the source server.</span>
After [step 5](#Scenario1_step05) (stage 1) is completed, copy the entire tool directory in stage 1 to the source server, and then run the tool for migration stage 2.
Execute the following command to run the tool for migration stage 2.
```
sudo ./go2tencentcloud_x64
```
If the `Stage 2 is finished and please run next stage at gateway machine.` prompt appears, stage 2 has been completed.
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
7. Run the tool on a server (such as the gateway) that can access the public network.
After [step 6](#Scenario1_step06) (stage 2) is completed, copy the entire tool directory in stage 2 to the source server in stage 1, and then run the tool for migration stage 3.
Execute the following command to run the tool for migration stage 3.
```
sudo ./go2tencentcloud_x64
```
If the `Migrate successfully` prompt appears, the entire migration task is completed.
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)
   
#### Scenario 2

1. Set up a connection between the source server and the destination CVM.
Set up a connection between the source server and the destination CVM by using [VPC peering connection](https://intl.cloud.tencent.com/document/product/553), [VPN connection](https://intl.cloud.tencent.com/document/product/1037), or [CCN](https://intl.cloud.tencent.com/document/product/1003).
2. In the user.json file, configure the source server and destination CVM for the migration.
 Configure the required parameters based on the [description of parameters in the user.json file](#userJsonState).
3. In the client.json file, configure the migration mode and other parameters.
 Set `Client.Net.Mode` in the client.json file to `2`, that is, select the [private network migration mode: scenario 2](#Scenario2). If necessary, configure other parameters based on [description of parameters in the client.json file](#clientJsonState).
4. (Optional) Exclude files and directories on the source server that do not need to be migrated.
When migrating the source Linux server, if you need to exclude some files and directories that do not need to be migrated, add these files and directories at the end of the [rsync_excludes_linux.txt file](#_linuxTxtState).
5. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as `root` to run the tool.
```
sudo ./go2tencentcloud_x64
```
Please wait for the migration process to complete.
If the following appears on the console, the migration has been completed successfully.
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)
  
#### Scenario 3

1. Set up a connection between the source server and the destination CVM.
 Set up a connection between the source server and the destination CVM by using [VPC peering connection](https://intl.cloud.tencent.com/document/product/553), [VPN connection](https://intl.cloud.tencent.com/document/product/1037), or [CCN](https://intl.cloud.tencent.com/document/product/1003).
2. In the user.json file, configure the source server and destination CVM for the migration.
Configure the required parameters based on the [description of parameters in the user.json file](#userJsonState).
3. In the client.json file, configure the migration mode and other parameters.
 1. Set `Client.Net.Mode` in the client.json file to `3`, that is, select the [private network migration mode: scenario 3](#Scenario3).
 2. Set `Client.Net.Proxy.Ip` and `Client.Net.Proxy.Port` in the client.json file to the IP address and port of the network proxy.
If your network proxy needs to be authenticated, set `Client.Net.Proxy.User` and `Client.Net.Proxy.Password` to the username and password of the network proxy. If authentication is not needed, you do not need to set these two parameters. If necessary, you can configure other parameters based on the [description of parameters in the client.json file](#clientJsonState).
4. (Optional) Exclude files and directories on the source server that do not need to be migrated.
When migrating the source Linux server, if you need to exclude some files and directories that do not need to be migrated, add these files and directories at the end of the [rsync_excludes_linux.txt file](#_linuxTxtState).
5. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as `root` to run the tool.
```
sudo ./go2tencentcloud_x64
```
Please wait for the migration process to complete.
If the following appears on the console, the migration has been completed successfully.
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)

## Checks after the Migration
1. If the migration fails, check the error information in the log files (under the migration tool directory by default), guides, or [About service migration](https://intl.cloud.tencent.com/document/product/213/32395), and rectify the faults.
2. If the migration succeeds, check whether the destination CVM can be started normally, whether the data on the destination CVM is consistent with that on the source server, whether the network is normal, and whether other system services run normally.
3. If you have any doubt or encounter migration errors, check [About service migration](https://intl.cloud.tencent.com/document/product/213/32395) or [submit a ticket](https://console.cloud.tencent.com/workorder/category).

