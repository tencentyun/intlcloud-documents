## Overview
This document describes how to use CFS Turbo on Linux clients. The standard login method, i.e., login via WebShell, is used in the example below.

## Prerequisites

- You have [created a file system and mount target](https://intl.cloud.tencent.com/document/product/582/9132).
- You have [created an instance](https://intl.cloud.tencent.com/document/product/213/4855) in a VPC of CCN.
- There is a compute instance that can communicate with the storage system and, in the VPC where CFS Turbo is located in CCN, port 988 of all IP addresses are opened bidirectionally.

## Directions

### Automatic installation

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Find the CVM instance you purchased in the instance list and click **Log In** on the right.
3. In the **Log in to Linux Instance** pop-up window, select **Standard login method** and click **Log In Now**.
4. On the WebShell login page, enter the username and password and click **OK**.
5. Run the following command to load the automation tool:
```
wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/tools/cfs_turbo_client_setup
```
6. Run the following command to set permissions for the automation tool:
```
chmod a+x cfs_turbo_client_setup
```
7. Run the following command to execute the automation tool:
```
sudo ./cfs_turbo_client_setup
```
 - If the information below is returned, installation is successful.
![](https://main.qcloudimg.com/raw/71cc3fdd2e94887cf4976bb80692792c.png)
 - If the information below is returned, the kernel version is not supported currently. For the versions supported, refer to the [kernel version list](#CVMKernelVersion) below.
![](https://main.qcloudimg.com/raw/cf1eb0ca5d9f5097099f472ae3ff7929.png)
>? Ubuntu 16.04 LTS does not support automatic download due to the mirror issue. You have to install it [manually](#ManualInstallation).
>

<span id="ManualInstallation"></span>
### Manual installation

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Find the CVM instance you purchased in the instance list and click **Log In** on the right.
3. In the **Log in to Linux Instance** pop-up window, select **Standard login method** and click **Log In Now**.
4. On the WebShell login page, enter the username and password and click **OK**.
5. Run the following command to view the kernel version of the instance:
```
uname -a
```
6. Depending on the kernel version, run the corresponding commands to download the two installation packages.
>! If the kernel version is not listed in the table below, update the kernel before you install the client.
>
<span id="CVMKernelVersion"></span>
<table>
	<tr><th>OS Version</th><th>Kernel Version</th><th>Command</th></tr>
	<tr><td rowspan="10">Ubuntu</td><td>4.15.0-142 18.04.4 LTS (Bionic Beaver)</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-142/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-142/cfsturbo-client-utils.x86_64.deb<code></pre></td></tr>
	<tr><td>4.15.0-142
16.04.7 LTS (Xenial Xerus)</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.15.0-142/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.15.0-142/cfsturbo-client-utils.x86_64.deb</code></pre></td></tr>
	<tr><td>4.15.0-118</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-118/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-118/cfsturbo-client-utils.x86_64.deb</code></pre></td></tr>
	<tr><td>4.15.0-76</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-76/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-76/cfsturbo-client-utils.x86_64.deb</code></pre></td></tr>
	<tr><td>4.15.0-62</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-62/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-62/cfsturbo-client-utils.x86_64.deb</code></pre></td></tr>
	<tr><td>4.15.0-45</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-45/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-45/cfsturbo-client-utils.x86_64.deb</code></pre></td></tr>
	<tr><td>4.15.0-30</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-30/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/4.15.0-30/cfsturbo-client-utils.x86_64.deb</code></pre></td></tr>
	<tr><td>5.4.0-42</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/5.4.0-42/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/5.4.0-42/cfsturbo-client-utils.x86_64.deb</code></pre></td></tr>
	<tr><td>5.4.0-48</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/5.4.0-48/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/5.4.0-48/cfsturbo-client-utils.x86_64.deb</code></pre></td></tr>
	<tr><td>5.4.0-62</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/5.4.0-62/cfsturbo-client-modules.x86_64.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu/5.4.0-62/cfsturbo-client-utils.x86_64.deb</code></pre></td></tr>
	<tr><td rowspan="6">CentOS</td><td>3.10.0-1160</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-1160/kmod-cfsturbo-client.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-1160/cfsturbo-client.x86_64.rpm</code></pre></td></tr>
	<tr><td>3.10.0-1127</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-1127/kmod-cfsturbo-client.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-1127/cfsturbo-client.x86_64.rpm</code></pre></td></tr>
	<tr><td>3.10.0-1062</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-1062/kmod-cfsturbo-client.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-1062/cfsturbo-client.x86_64.rpm</code></pre></td></tr>
	<tr><td>3.10.0-957</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-957/kmod-cfsturbo-client.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-957/cfsturbo-client.x86_64.rpm</code></pre></td></tr>
	<tr><td>3.10.0-862</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-862/kmod-cfsturbo-client.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-862/cfsturbo-client.x86_64.rpm</code></pre></td></tr>
	<tr><td>3.10.0-693</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-693/kmod-cfsturbo-client.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos/3.10.0-693/cfsturbo-client.x86_64.rpm</code></pre></td></tr>
</table>
7. Run the command corresponding to your OS to install the client.
 - Ubuntu:
```
sudo dpkg -i
```
 - CentOS:
```
yum install
```
8. Log in to the CFS console and go to the [File System](https://console.cloud.tencent.com/cfs/fs?rid=1) page.
9. Click the ID/name of the target Turbo file system and then select the **Mount Target Info** tab.
10. Click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" /> to copy the command.

11. Switch to the CVM instance to run the mount command copied.
The mount commands are described as follows. You can select one to fit your business needs.
 -If you want extended attributes supported and all operations to be executed synchronously by default (data will not be lost due to instance reboots, but the performance will be affected), copy and run the following command:
 For example:
```shell
sudo mount.lustre -o sync,user_xattrXXXXXXXXXXXXXXXXXXX
```
 - If you want extended attributes supported but don't need operations to be executed synchronously (some data cached in memory might be lost due to instance reboots, but the performance is good), copy and run the following command:
 For example:
```shell
sudo mount.lustre -o user_xattrXXXXXXXXXXXXXXXXXXX
```
 - If you do not need the extended attributes supported or the operations to be executed synchronously (some data cached in memory might be lost due to instance reboots, but the performance is good): copy and run the following command:
 For example:
```shell
sudo mount.lustre XXXXXXXXXXXXXXXXXXX
```



