This document introduces how to use the migration tool "go2tencentcloud" to migrate the CVM online.


## Migration Process
The migration process of the tool is shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/89072a07336ffe9574dfc8d0bc96de65.png)

## Preparations

- You already have a Tencent Cloud account and a destination CVM.
- Stop applications on the source server to prevent existing applications from being affected by the migration.
- [Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package.
- You can create a key and obtain the `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
- Check that both source servers and destination CVM meet the migration requirements. For example, the cloud disks of the destination CVM should have sufficient capacity to save data migrated from source servers.
- We recommend you back up your data in the following ways before migrating:
 - Source server: You can use the source server snapshot feature or other methods to back up data.
 - Destination CVM: You can create a snapshot as instructed in [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.

## Migration Directions


### Modifying configuration file[](id:modifyConfiguration)

1. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
    i. Run the following commands in sequence to decompress `go2tencentcloud.zip` and enter the directory.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    ii. Run the following commands in sequence to decompress `go2tencentcloud_tool.zip` and enter the directory.
```sh
unzip go2tencentcloud_tool.zip
```
```sh
cd go2tencentcloud_tool
```
<dx-alert infotype="explain" title="">
The files in the `go2tencentcloud` directory will not be migrated. Do not place the files to be migrated in this directory.
</dx-alert>
2. In the `user.json` file, configure the destination CVM for the migration.
Configure the required and desired values based on the `user.json` file parameter description. Replace the corresponding parameter values with your desired configuration values. Examples are shown below:
 - Example 1: To migrate a Linux source server to a CVM located in Guangzhou, configure the `user.json` file as follows:
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
} 
```
 - Example 2: A Linux source server has one data disk, of which the mount point is `/mnt/disk1`, and the size is `10` GB. To migrate this server to a CVM (with at least one data disk mounted) located in the Guangzhou region, configure the `user.json` file as follows:
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
 - Example 3: A Linux source server has two data disks. The mount point for disk 1 is `/mnt/disk1`, and the size is `10` GB. The mount point for disk 2 is `/mnt/disk2`, and the size is `20`GB. To migrate this server to a CVM (with at least two data disks mounted) located in Guangzhou, with disk 1 and disk 2 of the source server to be migrated to the first and second data disks of the destination CVM respectively, configure the `user.json` file as follows:
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
2. (Optional) In the `client.json` file, configure the migration mode and other parameters.
- Configure the required values based on the parameter description of the `client.json` file. If neither the source server or destination CVM can access the public network directly, you can establish a connection between them through [VPC peering connections](https://intl.cloud.tencent.com/document/product/553), [VPN connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216) and then migrate via the private network mode.
3. (Optional) Exclude files and directories on the source server that do not need to be migrated.
Add files or directories that do not need to be migrated from the Linux source server to `rsync\_excludes\_linux.txt`.

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
		OS consistency: If the OSs of the source server and target CVM are inconsistent, the created image may be inconsistent with the actual OS. We recommend that the OS of the target CVM be the same as that of the source host. For example, to migrate a CentOS 7 source host, select a CentOS 7 CVM as the target.
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
- You can use tool commands such as `sudo ./go2tencentcloud_x64 --check` to automatically check the source server.
- By default, the go2tencentcloud migration tool automatically performs checks upon launch. To skip checks and perform forced migration, configure `Client.Extra.IgnoreCheck` to `true` in the client.json file.
</dx-alert>



### Initiating migration

Run the following command to run the tool.
This document takes a 64-bit Linux source server as an example. Go to the `go2tencentcloud_tool` directory and run the following command as the root user to run the tool.
```sh
sudo ./go2tencentcloud_x64
```

### Waiting for migration to end

If you use go2tencentcloud supporting checkpoint restart provided by Tencent Cloud for migration, the migration process includes the following three stages. You can intuitively view the migration progress when the tool is running.

- **Stage 1**: The destination CVM enters the migration mode, and is ready for migration.
- **Stage 2**: The destination CVM is in the migration mode, and receives data migrated.
- **Stage 3**: The destination CVM exits the migration mode, and the migration completes.

Each stage will generate some subtasks to perform related operations, and some time-consuming subtasks may have maximum timeout periods by default. The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to complete.

<dx-alert infotype="notice" title="">
The destination CVM enters migration mode after the migration starts. Do not reinstall the system, shut down, terminate, or reset passwords of the destination CVM until the migration is completed and the destination CVM exits the migration mode. 
</dx-alert>

If the migration via the public network mode succeeds, the console output is as follows:
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

### Checking after the Migration

- If the migration fails, check the error information in log files (under the migration tool directory by default), operation guides, or FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting methods.
- If the migration is successful, check whether the target CVM starts up normally, whether data on the target CVM is consistent with that on the source server, and whether the network and other system services are normal.

If you have any questions or the migration has an exception, see FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [Contact Us](https://intl.cloud.tencent.com/document/product/213/34837).
