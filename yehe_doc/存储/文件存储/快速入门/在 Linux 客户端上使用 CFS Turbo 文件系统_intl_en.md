## Overview
This document describes how to use CFS Turbo on Linux clients.

## Step 1. Create a File System and Mount Target
For detailed directions, please see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).

## Step 2. Log In to the Instance in the CNN
>? This document uses the standard instance login method (WebShell) as an example. For more login methods, please see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
>
1. Create an instance in a VPC of CNN. For more information, please see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
2. Log in to the [CVM console](https://console.cloud.tencent.com/cvm), find the purchased CVM instance, and click **Log In** on the right.
3. In the **Log into Linux instance** window, click **Log In Now**. After this, enter the CVM instance’s username and password and then click **OK** to log in.

## Step 3. Download the Client
1. Run the following command to view the kernel version of the instance:
```
uname -a
```
2. Run the following commands corresponding to the kernel version in sequence to download the two installation packages:
>! If the kernel version is not listed in the table below, upgrade the kernel before you download the client.
>
<table>
	<tr><th>OS Version</th><th>Kernel Version</th><th>Command</th></tr>
	<tr><td rowspan="9">Ubuntu16.04</td><td>4.10.0-42-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-143-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-143-generic/cfsturbo-utils.deb<code></pre></td></tr>
	<tr><td>4.11.0-14-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.11.0-14-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.11.0-14-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.13.0-45-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.13.0-45-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.13.0-45-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.15.0-99-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.15.0-99-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.15.0-99-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.4.0-112-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-112-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-112-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.4.0-116-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-116-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-116-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.4.0-133-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-133-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-133-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.4.0-143-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-143-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-143-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.4.0-157-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-157-generic/cfsturbo-kernel-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu16.04/4.4.0-157-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td rowspan="6">Ubuntu18.04</td><td>4.15.0-30-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-30-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-30-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.15.0-45-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-45-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-45-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.15.0-62-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-62-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-62-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.15.0-76-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-76-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-76-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.15.0-118-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-118-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-118-generic/cfsturbo-utils.deb</code></pre></td></tr>
	<tr><td>4.15.0-142-generic</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-142-generic/cfsturbo-client-modules.deb</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/ubuntu18.04/4.15.0-142-generic/cfsturbo-client-utils.deb</code></pre></td></tr>
	<tr><td>CentOS 7.9</td><td>3.10.0-1160</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.9/3.10.0-1160/kmod-lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.9/3.10.0-1160/lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre></td></tr>
	<tr><td>CentOS 7.8</td><td>3.10.0-1127</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.8/3.10.0-1127/kmod-lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.8/3.10.0-1127/lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre></td></tr>
	<tr><td>CentOS 7.7</td><td>3.10.0-1062</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.7/3.10.0-1062/kmod-lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.7/3.10.0-1062/lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre></td></tr>
	<tr><td>CentOS 7.6</td><td>3.10.0-957</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.6/3.10.0-957/kmod-lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.6/3.10.0-957/lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre></td></tr>
	<tr><td>CentOS 7.5</td><td>3.10.0-862</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.5/3.10.0-862/kmod-lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.5/3.10.0-862/lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre></td></tr>
	<tr><td>CentOS 7.4</td><td>3.10.0-693</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.4/3.10.0-693/kmod-lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre>
	<pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.4/3.10.0-693/lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre></td></tr>
	<tr><td>CentOS 7.3</td><td>3.10.0-514</td>
	<td><pre><code>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.3/3.10.0-514/kmod-lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre>
	<pre>wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/2.12.4/centos7.3/3.10.0-514/lustre-client-2.12.4-1.el7.x86_64.rpm</code></pre></td></tr>
</table>

## Step 4. Install the Client

Run the command corresponding to your OS to install the client.
- **Ubuntu**:
```
sudo dpkg -i
```
- **CentOS*:
```
yum install
```

## Step 5. Mount the Turbo File System

1. Log in to the CFS console and click [File System](https://console.cloud.tencent.com/cfs/fs?rid=1) in the left sidebar.
2. Click the ID/name of the desired Turbo file system and then select the **Mount Target Info** tab.
3. Click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" /> to copy the desired command.
![](https://main.qcloudimg.com/raw/4133842c838460323fea754124bd8548.png)
4. Switch to the CVM instance to run the mount command copied.
In most cases, you are advised to use the first mount command. The mount commands are described as follows:
 - Copy and run the first command if you need the extension attributes supported and all operations to be executed synchronously by default (data will not be lost due to instance restart while I/O performance will be compromised).
 Example:
```
sudo mount.lustre -o sync,user_xattrXXXXXXXXXXXXXXXXXXX
```
 - Copy and run the second command if you need the extension attributes supported but not the synchronous execution for operations (some data cached in memory might be lost due to instance restart but the I/O performance will be fine).
 Example:
```
sudo mount.lustre -o user_xattrXXXXXXXXXXXXXXXXXXX
```
 - Copy and run the third command if you don’t need the extension attributes supported nor the operations to be executed synchronously.
 Example:
```
sudo mount.lustre XXXXXXXXXXXXXXXXXXX
```



