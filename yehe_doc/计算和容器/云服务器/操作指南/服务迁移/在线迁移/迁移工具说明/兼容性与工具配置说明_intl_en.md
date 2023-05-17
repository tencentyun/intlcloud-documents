## Supported Operating Systems

Operating systems supported by the online migration tool include but not limited to the following:

<table>
	<tr><th>Linux</th><th>Windows</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=8>Windows Server 2008<br>Windows Server 2012<br>Windows Server 2016<br>Windows Server 2019<br>Windows Server 2022</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18/20 </td></tr>
	<tr><td>Debian 7/8/9/10</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 5/6/7/8</td></tr>
	<tr><td>Oracle Linux 5/6/7/8</td></tr>
</table>

## Supported Migration Modes

<dx-tabs>
::: Public network migration mode[](id:publicMigration)
If both your source server and destination CVM can access the public network, you can use the public network migration mode.
In the current public network migration mode, the source server calls Tencent Cloud APIs through the Internet to initiate a migration request, and transfers data to the destination CVM to complete the migration. The public network migration scenario is shown below:
 ![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)
:::
::: Private network migration mode[](id:intranetMigration)
If your source server or destination CVM is located in a private network or Virtual Private Cloud (VPC), the source server cannot directly establish a connection with the destination CVM through the Internet. In this case, you can use the private network migration mode of the tool. You need to establish a connection between the source server and the destination CVM through [VPC peering connection](https://intl.cloud.tencent.com/document/product/553), [VPN connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216).

- [](id:Scenario1)**Scenario 1**: This scenario is applicable to the migration via [Online Migration Tool](https://intl.cloud.tencent.com/document/product/213/35640). If your source server or the destination CVM cannot access the public network, you can first access the Tencent Cloud API via the internet through a server with public network access (such as a gateway) to initiate a migration request, and then transfer data and migrate to the destination CVM through the connection. This scenario does not require the source server and destination CVM can access the public network.
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- [](id:Scenario2)**Scenario 2**: If your source server can access the public network, use the source server to call Tencent Cloud APIs through the Internet to initiate a migration request, and then transfer data to the destination CVM through the connection to complete the migration. This scenario requires the source server, but not the destination CVM, to be able to access the public network.
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- [](id:Scenario3)**Scenario 3**: If your source server can access the public network through a proxy, use the source server to call Tencent Cloud APIs through the network proxy to initiate a migration request, and then transfer data to the destination CVM through the connection to complete the migration. This scenario requires neither the source server nor the destination CVM to be able to access the public network.
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)
:::
</dx-tabs>


## Files in the Compressed Package
After `go2tencentcloud.zip` is decompressed, it contains the following files:
<table>
	<tr><th width="30%">File Name</th><th>Description</th></tr>
	<tr><td>go2tencentcloud-linux.zip</td><td>The migration zip for Linux system.</td></tr>
	<tr><td>go2tencentcloud-windows.zip</td><td>The migration zip for Windows system.</td></tr>
	<tr><td>readme.txt</td><td>Directory overview file.</td></tr>
	<tr><td>release_notes.txt</td><td>Migration tool change log.</td></tr>
</table>

After `go2tencentcloud-linux.zip` is decompressed, it contains the following files:
<table>
	<tr><th width="30%">File Name</th><th>Description</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>Executable program of the migration tool for the 64-bit Linux operating system.</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>Executable program of the migration tool for the 32-bit Linux operating system.</td></tr>
	<tr><td>user.json</td><td>User information in the migration.</td></tr>
	<tr><td>client.json</td><td>Configuration file of the migration tool.</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync configuration file, which excludes files and directories that do not need to be migrated in the Linux system.</td></tr>
</table>

After `go2tencentcloud-windows.zip` is decompressed, it contains the following files:
<table>
	<tr><th width="30%">File Name</th><th>Description</th></tr>
	<tr><td>go2tencentcloud_x64.exe</td><td>Executable program of the migration tool for the 64-bit Windows operating system.</td></tr>
	<tr><td>user.json</td><td>User information in the migration.</td></tr>
	<tr><td>client.json</td><td>Configuration file of the migration tool.</td></tr>
	<tr><td>client.exe</td><td>Executable program of the migration tool for the Windows operating system.</td></tr>
</table>

<dx-alert infotype="notice" title="">
The configuration files cannot be deleted. You must store them under the same folder as the go2tencentcloud executable program. 
</dx-alert>

### Parameters in the user.json file[](id:userJsonState)

The user.json configuration file is described as below:

<table>
	<tr><th>Parameter</th><th>Type</th><th>Required</th><th>Description</th></tr>
	<tr><td>SecretId</td><td>String</td><td>Yes</td><td>Secret ID for your account to access APIs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>Yes</td><td>Secret key for your account to access APIs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td></tr>
</table>

### Parameters in the client.json file[](id:clientJsonState)

The client.json configuration file is described as below:

<table>
  <tr>
	<th>Parameter</th>
	<th>API Type</th>
	<th>Required<br></th>
	<th>Description</th>
  </tr>
  <tr>
	<td>Client.Extra.IgnoreCheck</td>
	<td>Bool</td>
	<td>No</td>
	<td>The default value is  
	<code>false</code>. The default value is false. The migration tool automatically checks the source server environment upon startup by default. To skip the check, set this parameter to  
	<code>true</code>.</td>
  </tr>
  <tr>
	<td>Client.Extra.Daemon</td>
	<td>Bool</td>
	<td>No</td>
	<td>The default value is  
	<code>false</code>. If you need the migration tool to run in the background, set this parameter to  
	<code>true</code>.</td>
  </tr>
  <tr>
	<td> Client.Net.Proxy.Ip</td>
	<td>String</td>
	<td>No</td>
	<td>The default value is empty. In the private network migration <a href="#Scenario3">Scenario 3</a>, the IP address of the network proxy needs to be configured.</td>
  </tr>
	 <tr>
<td> Client.Net.Proxy.IPv6</td>
	<td>Bool</td>
	<td>No</td>
	<td>It defaults to <code>false</code>. Set it to <code>true</code> if you want to transfer data via IPv6. Otherwise, the migration data will be transferred via IPv4.</td>
  </tr>
  <tr>
	<td> Client.Net.Proxy.Port</td>
	<td>String</td>
	<td>No</td>
	<td>The default value is empty. In the private network migration <a href="#Scenario3">Scenario 3</a>, the port of the network proxy needs to be configured.</td>
  </tr>
   <tr>
	<td> Client.Net.Proxy.User</td>
	<td>String</td>
	<td>No</td>
	<td>The default value is empty. In the private network migration <a href="#Scenario3">Scenario 3</a>, if your network proxy needs to be verified, configure the username of the network proxy.</td>
  </tr>
   <tr>
	<td> Client.Net.Proxy.Password</td>
	<td>String</td>
	<td>No</td>
	<td>The default value is empty. In the private network migration <a href="#Scenario3">Scenario 3</a>, if your network proxy needs to be verified, configure the password of the network proxy.</td>
  </tr>
</table>

<dx-alert infotype="explain" title="">
Except for the above parameters, other configuration items in the `client.json` file usually don't need to be entered.
</dx-alert>

### rsync\_excludes\_linux.txt file description[](id:_linuxTxtState)

This file is used to exclude files on the Linux source server or configuration files under specified directories that do not need to be migrated. By default, the rsync\_excludes\_linux.txt file already excludes the following directories and files. **Do not delete or modify the existing configurations.**
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
To exclude other directories or files, append them to the rsync\_excludes\_linux.txt file. For example, to exclude all content on the data disk attached to `/mnt/disk1`, configure the rsync\_excludes\_linux.txt file as follows:
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

## Parameters of the Migration Tool

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
<td><code>--version</code></td>
<td>Prints the version number.</td>
</tr>
<tr>
<td><code>--clean</code></td>
<td>Ends the migration task.</td>
</tr>
</tbody>
</table>
