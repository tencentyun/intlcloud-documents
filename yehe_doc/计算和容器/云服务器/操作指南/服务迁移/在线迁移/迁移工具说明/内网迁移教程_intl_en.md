## Overview
This document describes how to migrate the system and applications from a source server in a self-built IDC or cloud platform to CVM through the online migration tool in **private network** mode.

Compared with the public network mode, migration over the private network has a higher migration transfer speed, which can significantly improve the migration efficiency. Plus, it doesn't restrict the public network access capability of the source server, making the migration configuration more flexible.


## Preparations

- You already have a Tencent Cloud account and a destination CVM.
- Stop applications on the source server to prevent existing applications from being affected by the migration.
- Create and copy `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
- Check that both source servers and destination CVM meet the migration requirements. For example, the cloud disks of the destination CVM should have sufficient capacity to save data migrated from source servers.


## Directions

### Backing up data
- Source server: you can use the source server's snapshot feature or other methods to back up data.
- Destination CVM: you can [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.


### Getting migration tool  
[Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to obtain the compressed migration tool package.


### Choosing migration mode based on network environment
Choose the appropriate migration mode according to the network environments of your source servers and destination CVMs.
Currently, the migration tool supports the public network mode and the private network mode. The private network mode applies to three scenarios. Each migration mode or scenario has different network requirements for source servers and destination CVMs. If both source servers and destination CVMs can access the public network, you can use the default mode for migration. If source servers or destination CVMs cannot directly access the public network, you need to establish a connection between them through [Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/zh/document/product/216) before using the private network mode for migration.

### Checking before migration

Before migration, you need to check the source server and destination CVM separately as detailed below:


<table>
  <tr>
	<th style="width: 15%;">Destination CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		Storage space: the cloud disks of the destination CVM (including system and data disks) should have sufficient capacity to save data migrated from the source server.</li>
		<li>Security group: port 443 and port 80 cannot be restricted in the security group.</li>
		<li>
		Bandwidth settings: we recommend you maximize bandwidths at the two ends to speed up the migration. During the process, the traffic consumed is approximately the amount of data migrated. Adjust the billing mode before the migration if necessary.</li>
		<li>
		OS consistency: if the operating systems of the source server and destination CVM are different, the created image may be inconsistent with the actual operating system. We recommend you use the same operating system for the source server and destination CVM.
		For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM as the destination.</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th>Linux source server</th>
	<td>
	  <ol style="margin: 0;">
		<li>Check and install Virtio. For more information, see: 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>.</li>
		<li>Run 
		the <code>which rsync</code> command to check whether Rsync is installed, and if not, install it as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">How do I install Rsync?</a>.</li>
		<li>Check whether SELinux is enabled, and if yes, disable it as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">How do I disable SELinux?</a>.</li>
		<li>After a migration request is made to the TencentCloud API, the API will use the current UNIX time to check the generated
		token. You need to make sure that the current system time is correct.</li>
		<li>Check the login method of the source server. If your AWS source server uses SSH key pair for login, we recommend you change it to login with password.</li>
		密钥对方式登录，建议更换为密码方式登录。</li>
	  </ol>
	</td>
  </tr>
</table>


<dx-alert infotype="explain" title="">

- You can use tool commands such as `sudo ./go2tencentcloud_x64 --check` to automatically check the source server.
- By default, the go2tencentcloud migration tool automatically starts checking upon launch. To skip checks and perform forced migration, configure `Client.Extra.IgnoreCheck` to `true` in the `client.json` file.
- For more information on the go2tencentcloud migration tool, see [Migration Tool Description](https://intl.cloud.tencent.com/document/product/213/44340).
</dx-alert>


### Starting migration
For different scenarios of migration in private network mode, the steps are as follows:

<dx-tabs>

::: Scenario 1

1. Establish a connection between the source server and the destination CVM.
Establish a connection between the source server and the destination CVM by using [Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/zh/document/product/1037), or [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003).
2. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
    1. Run the following commands in sequence to decompress `go2tencentcloud.zip` and enter the directory.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. Run the following commands in sequence to decompress `go2tencentcloud_tool.zip` and enter the directory.
```sh
unzip go2tencentcloud_tool.zip
```
```sh
cd go2tencentcloud_tool
```
3. In the `user.json` file, configure the destination CVM for the migration.
Follow the [descriptions of parameters in the `user.json` file](https://intl.cloud.tencent.com/document/product/213/44340) to configure the required parameters and their values.
4. In the `client.json` file, configure the migration mode and other parameters.
Set the value of `Client.Net.Mode` in the `client.json` file to `1`; that is, migration [in private network mode in scenario 1](https://intl.cloud.tencent.com/document/product/213/44340) will be performed. In addition, if you need to set other items, follow the [descriptions of parameters in the `client.json` file](https://intl.cloud.tencent.com/document/product/213/44340).
5. (Optional) Exclude files or directories that do not need to be migrated on the source server.
If there are files or directories on the Linux source server that do not need to be migrated, you can add them to the [rsync_excludes_linux.txt](https://intl.cloud.tencent.com/document/product/213/44340) file.
6. [](id:Scenario1_step05)Run the tool on a server (such as gateway) that can access the public network.
For example, on a server that can access the public network, execute the following command to run the tool for migration stage 1.
``` sh
chmod +x go2tencentcloud_x64
sudo ./go2tencentcloud_x64
```
If `Stage 1 is finished and please run next stage at source machine.` is prompted, stage 1 has been completed as shown below:
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
7. [](id:Scenario1_step06)Run the tool on the source server.
After [step 5](#Scenario1_step05) (stage 1) is completed, copy the entire tool directory in stage 1 to the source server, and then run the tool for migration stage 2.
Execute the following command to run the tool for migration stage 2.
```sh
sudo ./go2tencentcloud_x64
```
If `Stage 2 is finished and please run next stage at gateway machine.` is prompted, stage 2 has been completed as shown below:
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
8. Run the tool on a server (such as the gateway) that can access the public network.
After [step 6](#Scenario1_step06) (stage 2) is completed, copy the entire tool directory in stage 2 to the server in stage 1, and then run the tool for migration stage 3.
Execute the following command to run the tool for migration stage 3.
```sh
sudo ./go2tencentcloud_x64
```
If `Migrate successfully` is prompted, the entire migration task has been completed as shown below:
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)

:::
::: Scenario 2

1. Establish a connection between the source server and the destination CVM.
Establish a connection between the source server and the destination CVM by using [Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/zh/document/product/1037), or [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003).
2. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
    1. Run the following commands in sequence to decompress `go2tencentcloud.zip` and enter the directory.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. Run the following commands in sequence to decompress `go2tencentcloud_tool.zip` and enter the directory.
```sh
unzip go2tencentcloud_tool.zip
```
```sh
cd go2tencentcloud_tool
```
3. In the `user.json` file, configure the destination CVM for the migration.
 Follow the [descriptions of parameters in the `user.json` file](https://intl.cloud.tencent.com/document/product/213/44340) to configure the required parameters and their values.
4. In the `client.json` file, configure the migration mode and other parameters.
 Set the value of `Client.Net.Mode` in the `client.json` file to `2`; that is, migration [in private network mode in scenario 2](https://intl.cloud.tencent.com/document/product/213/44340) will be performed. In addition, if you need to set other items, follow the [descriptions of parameters in the client.json` file](https://intl.cloud.tencent.com/document/product/213/44340).
5. (Optional) Exclude files or directories that do not need to be migrated on the source server.
If there are files or directories on the Linux source server that do not need to be migrated, you can add them to the [rsync_excludes_linux.txt](https://intl.cloud.tencent.com/document/product/213/44340) file.
6. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as the root user to run the tool.
```sh
sudo ./go2tencentcloud_x64
```
Please wait for the migration process to complete.
If the following appears on the console, the migration has been completed successfully.
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)



:::

::: Scenario 3

1. Establish a connection between the source server and the destination CVM.
Establish a connection between the source server and the destination CVM by using [Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/zh/document/product/1037), or [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003).
2. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
    1. Run the following commands in sequence to decompress `go2tencentcloud.zip` and enter the directory.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. Run the following commands in sequence to decompress `go2tencentcloud_tool.zip` and enter the directory.
```sh
unzip go2tencentcloud_tool.zip
```
```sh
cd go2tencentcloud_tool
```
3. In the `user.json` file, configure the destination CVM for the migration.
    Follow the [descriptions of parameters in the `user.json` file](https://intl.cloud.tencent.com/document/product/213/44340) to configure the required parameters and their values.
4. In the `client.json` file, configure the migration mode and other parameters.
    1. Set the value of `Client.Net.Mode` in the `client.json` file to `3`; that is, migration [in private network mode in scenario 3](https://intl.cloud.tencent.com/document/product/213/44340) will be performed.
    2. Configure `Client.Net.Proxy.Ip` and `Client.Net.Proxy.Port` in the `client.json` file to the IP address and port of the network proxy.
        If your network proxy needs to be authenticated, configure `Client.Net.Proxy.User` and `Client.Net.Proxy.Password` to the username and password of the network proxy. You may leave them in blank if authentication is not required. If necessary, you can configure other parameters based on the [description of parameters in the `client.json` file](https://intl.cloud.tencent.com/document/product/213/44340).
5. (Optional) Exclude files or directories that do not need to be migrated on the source server.
If there are files or directories on the Linux source server that do not need to be migrated, you can add them to the [rsync_excludes_linux.txt](https://intl.cloud.tencent.com/document/product/213/44340) file.
6. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as the root user to run the tool.
```sh
sudo ./go2tencentcloud_x64
```
Please wait for the migration process to complete.
If the following appears on the console, the migration has been completed successfully.
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)

:::

</dx-tabs>



### Checking after migration

- If the migration fails, check the error information in log files (under the migration tool directory by default), operation guides, or [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting methods.
- If the migration succeeds, check whether the destination CVM can be started normally, whether data on the destination CVM is consistent with that on the source server, whether the network is normal, and whether other system services run normally.

If you have any questions or the migration has an exception, see [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [contact us](https://intl.cloud.tencent.com/document/product/213/34837).











