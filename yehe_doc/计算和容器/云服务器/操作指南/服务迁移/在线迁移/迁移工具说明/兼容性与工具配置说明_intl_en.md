## Supported OS

Operating systems supported by the online migration tool include but are not limited to the following (32-bit or 64-bit):

<table>
	<tr><th>Linux</th><th>Windows</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=7>Windows Server 2008 R2 and above</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18/20 </td></tr>
	<tr><td>Debian 7/8/9/10</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

## Supported Migration Modes

<dx-tabs>

::: Migration in console[](id:consoleMigrate)

The console migration tool currently only supports the public network migration mode, and the data is transferred over the public network for migration.

:::
::: Migration via tool[](id:toolMigrate)

Migration via tool supports **public network migration mode** and **private network migration mode**.

#### Public network migration mode[](id:publicMigration)
If both your source server and destination CVM can access the public network, you can use the public network migration mode.
In the current public network migration mode, the source server calls TencentCloud APIs through the Internet to initiate a migration request, and transfers data to the destination CVM to complete the migration. The public network migration scenario is as shown below:
 ![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)

​    

#### Private network migration mode[](id:intranetMigration)

If your source server or destination CVM is located in a private network or Virtual Private Cloud (VPC), the source server cannot directly establish a connection with the destination CVM through the Internet. In this case, you can use the private network migration mode of the tool. You need to establish a connection between the source server and the destination CVM through [Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/zh/document/product/216).

- [](id:Scenario1)**Scenario 1**: if your source server or destination CVM cannot access the public network, use a server (such as the gateway) that can access the public network to call TencentCloud APIs through the Internet to initiate a migration request, and then transfer data to the destination CVM through the connection to complete the migration. This scenario requires neither the source server nor the destination CVM to be able to access the public network.
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- [](id:Scenario2)**Scenario 2**: if your source server can access the public network, use the source server to call TencentCloud APIs through the Internet to initiate a migration request, and then transfer data to the destination CVM through the connection to complete the migration. This scenario requires the source server, but not the destination CVM, to be able to access the public network.
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- [](id:Scenario3)**Scenario 3**: if your source server can access the public network through a proxy, use the source server to call TencentCloud APIs through the network proxy to initiate a migration request, and then transfer data to the destination CVM through the connection to complete the migration. This scenario requires neither the source server nor the destination CVM to be able to access the public network.
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)


:::

</dx-tabs>




## Files in Compressed Package
After `go2tencentcloud.zip` is decompressed, it contains the following files:
<table>
	<tr><th width="30%">Filename</th><th>Description</th></tr>
	<tr><td>go2tencentcloud_console.zip</td><td>Package for migration in the console.</td></tr>
	<tr><td>go2tencentcloud_tool.zip</td><td>Package for migration via the tool.</td></tr>
	<tr><td>readme.txt</td><td>Directory overview file.</td></tr>
	<tr><td>release_notes.txt</td><td>Migration tool change log.</td></tr>
</table>
After `go2tencentcloud_console.zip` or `go2tencentcloud_tool.zip` is decompressed, it contains the following files:
<table>
	<tr><th width="30%">Filename</th><th>Description</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>Executable program of the migration tool for the 64-bit Linux operating system</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>Executable program of the migration tool for the 32-bit Linux operating system</td></tr>
	<tr><td>user.json</td><td>Configuration file of the source server and the destination CVM during the migration. You need to modify the configurations based on the <a href="#userJsonState">description of parameters in the `user.json` file</a>.</td></tr>
	<tr><td>client.json</td><td>Configuration file of the migration tool, which usually does not need to be modified in case of migration in the console.</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync configuration file, which excludes files and directories that do not need to be migrated in the Linux system.</td></tr>
</table>

<dx-alert infotype="notice" title="">
The configuration files cannot be deleted. You must store them under the same folder as the go2tencentcloud executable program. 
</dx-alert>



### Description of parameters in user.json file[](id:userJsonState)

<dx-tabs>

::: Migration in console[](id:consoleMigrate)

For migration in console, the `user.json` configuration file is as described below:

<table>
	<tr><th>Parameter</th><th>Type</th><th>Required</th><th>Description</th></tr>
	<tr><td>SecretId</td><td>String</td><td>Yes</td><td>Secret ID for your account to access APIs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>Yes</td><td>Secret key for your account to access APIs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td></tr>
</table>

:::
::: Migration via tool[](id:toolMigrate)

For migration via tool, the `user.json` configuration file is as described below:

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
	<td>`SecretId` for your account to access APIs. For more information, see 
	<a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td>
  </tr>
  <tr>
	<td>SecretKey</td>
	<td>String</td>
	<td>Yes</td>
	<td>`SecretKey` for your account to access APIs. For more information, see 
	<a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>.</td>
  </tr>
  <tr>
	<td>Region</td>
	<td>String</td>
	<td>Yes</td>
	<td>Region of the destination CVM. Only the region is required, not the AZ. For more information, see 
	<a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and AZs</a>.</td>
  </tr>
  <tr>
	<td>InstanceId</td>
	<td>String</td>
	<td>Yes</td>
	<td>Instance ID of the destination CVM, which in the format of 
	<code>ins-xxxxxxxx</code>.</td>
  </tr>
  <tr>
	<td>DataDisks</td>
	<td>Array</td>
	<td>No</td>
	<td>List of data disks to be migrated from the source server. Each element indicates a data disk. Up to 20 data disks are supported.</td>
  </tr>
  <tr>
	<td>DataDisks.Index</td>
	<td>Integer</td>
	<td>No</td>
	<td>Serial number of the data disk. The value range is [1,20].
	<code>1</code> indicates that the data disk will be migrated to the first data disk mounted to the destination CVM.
	<code>2</code> indicates that the data disk will be migrated to the second data disk mounted to the destination CVM, and so on.</td>
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

You can refer to the sample in <a href="https://intl.cloud.tencent.com/document/product/213/35640">Online Migration Tool</a> to modify the configuration file as needed.

:::

</dx-tabs>


### Descriptions of parameters in client.json file[](id:clientJsonState)

<dx-tabs>

::: Migration in console[](id:consoleMigrate)

For migration in console, there is usually no need to modify the `client.json` configuration file.

:::
::: Migration via tool[](id:toolMigrate)

For migration via tool, the `client.json` configuration file is as described below:

<table>
  <tr>
	<th>Parameter Name</th>
	<th>Type</th>
	<th>Required<br></th>
	<th>Description</th>
  </tr>
  <tr>
	<td>Client.Net.Mode</td>
	<td>Integer</td>
	<td>Yes</td>
	<td>Migration mode parameter, which is public network migration mode by default with the value of <code>0</code>. Valid values: <code>0</code> (<a href="#publicMigration">public network migration mode</a>), <code>1</code> (<a href="#Scenario1">private network migration mode: scenario 1</a>), <code>2</code> (<a href="#Scenario2">private network migration mode: scenario 2</a>), <code>3</code> (<a href="#Scenario3">private network migration mode: scenario 3</a>). For more information on private network migration, see <a href="https://intl.cloud.tencent.com/document/product/213/44341">Private Network Migration</a>.</td>
  </tr>
  <tr>
	<td>Client.Extra.IgnoreCheck</td>
	<td>Bool</td>
	<td>No</td>
	<td>The default value is <code>false</code>, that is, the migration tool automatically checks the source server environment upon startup by default. To skip the check, set this parameter to <code>true</code>.</td> 
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
	<td>Transfer check. Setting it to <code>true</code> can enhance the transfer consistency check, but will increase the CPU load of the source server and slow down the transfer. The default value is <code>false</code>, which indicates no check.</td> 
  </tr>
</table>




<dx-alert infotype="explain" title="">
Except for the above parameters, other configuration items in the `client.json` file usually don't need to be entered.
</dx-alert>

:::

</dx-tabs>

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

## Migration Tool Parameters

<dx-tabs>

::: Migration in console[](id:consoleMigrate)

For migration in console, the migration tool parameters are as described below:

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
<td>Checks the source server without migration.</td>
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
</tbody></table>

:::
::: Migration via tool[](id:toolMigrate)

For migration via tool, the migration tool parameters are as described below:

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
<td>Checks the source server without migration.</td>
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
<td>Enables the destination CVM to forcibly exit the migration mode and cleanse the site. For example, if the console prompts <code>Please execute '--clean' option manually.</code>, you need to specify this parameter and run the tool for the destination CVM to exit the migration mode.</td>
</tr>
<tr>
<td><code>--version</code></td>
<td>Prints the version number.</td>
</tr>
</tbody></table>

:::

</dx-tabs>

