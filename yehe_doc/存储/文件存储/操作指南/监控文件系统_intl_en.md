## Overview

To use the CFS monitoring feature, you need to first install the CFS monitoring plugin on your clients such as CVM or TKE instances.

## Installing CFS Monitoring Plugin


#### Prerequisites
CFS monitoring plugin is a plugin integrated with Tencent Cloud CVM Agent to monitor the performance of CFS file systems and client connections.

>Before installing the plugin, please make sure that your client has Tencent Cloud CVM Agent installed. For more information, please see [Installing CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211).

#### OS support
Currently, CFS monitoring plugin **supports clients mounted over NFS, but not over CIFS/SMB**, and the following operating systems. There may be compatibility issues with other kernel versions of Linux.



<table>
   <tr>
      <th>OS</th>
      <th>Version</th>
   </tr>
   <tr>
      <td rowspan=8>CentOS</td>
      <td>CentOS 7.6 64-bit</td>
   </tr>
	  <tr>
      <td>CentOS 7.5 64-bit</td>
   </tr>
   <tr>
      <td>CentOS 7.4 64-bit</td>
   </tr>
   <tr>
      <td>CentOS 7.3 64-bit</td>
   </tr>
   <tr>
      <td>CentOS 7.2 64-bit</td>
   </tr>
   <tr>
      <td>CentOS 6.9 64-bit</td>
   </tr>
   <tr>
      <td>CentOS 6.9 32-bit</td>
   </tr>
   <tr>
      <td>CentOS 6.8 64-bit</td>
   </tr>
   <tr>
      <td>Ubuntu</td>
      <td>Ubuntu Server 16.04.1 LTS 64-bit</td>
   </tr>
</table>



#### Feature description

How the plugin works and its key features:

- How it works: the plugin reads data from NFS-related logs in `/proc/self/mountstats` and `/var/log/messages`, including performance, status, and mount parameters but not your actual business data.
- Key features: it reads the status of mount points on the client using CFS, performs mount point availability scans, and collects performance-related data.

## Installing on Linux

You can log in to the Linux-based instance and follow the steps below to obtain and install the CFS monitoring plugin: [Download the plugin](#step1) > [Grant the installer execution permissions](#step2) > [Install the plugin](#step3).

<span id="step1"></span>

#### Download the plugin

You can run the command below to download the CFS monitoring plugin to the current directory of the client.

```sh
## Download CFS monitoring plugin
wget http://mirrors.tencentyun.com/install/cfs/cfs_barad_plugin_installer_release_v11
```

<span id="step2"></span>

#### Grant the installer execution permissions

Grant CFS monitoring plugin installer execution permissions by running this command:

```sh
## Grant the installer execution permissions
chmod +x cfs_barad_plugin_installer_release_v11
```

<span id="step3"></span>

#### Install the plugin

You can run the following command to install the CFS monitoring plugin. A success message will be returned if the installation is successful.

```sh
## Install the plugin
./cfs_barad_plugin_installer_release_v11
```

After successful installation, `cfs barad plugin install success` will be displayed as shown below:
![](https://main.qcloudimg.com/raw/d4138a9caa55d3b2ef030f658b3e86e9.png)

>? For Ubuntu clients, root permissions are required, that is, prepend `sudo` to the beginning of the command.

## Installing on Windows

Windows clients are not supported currently.

## Monitoring Visiting Clients

Log in to the [CFS Console](https://console.cloud.tencent.com/cfs), click a file system name, and select **Mounted Clients** to view the list of clients to which the file system is mounted. If the plugin has not been installed on any client, no information will be available.

> !There may be a delay of 1-3 minutes before you can see the client list.


## Performance Monitoring

Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/product/cfs) where you can view the health status and alarm information about each file system on the CFS monitoring page.

#### Monitoring metrics

Click any file system ID/name in the page above to enter the details page. You can select any time window to view the usage of the monitored file system.

The monitoring metrics supported by CFS are as follows:

| Metric Name  |  Description   | Unit   | Level |
| ------------ | ------------------------------ | ---- | ---------- |
| Storage usage | File system storage usage at the current time | GB | Single file system |
| Read bandwidth | Average amount of data read from the file system per second | KB/s | Single file system |
| Write bandwidth | Average amount of data written to the file system per second | KB/s | Single file system |
| Read IOPS  | Average number of reads from the file system per second  | Reads/second | Single file system |
| Write IOPS  | Average number of writes on the file system per second  | Writes/second | Single file system |

> !Because of local cache on the client, the **read bandwidth** and **read IOPS** of the file system obtained by Cloud Monitor may be slightly less than the actual usage.

#### Alarm policies

You can enter the alarm policy page to view alarm policies associated with the file system. Click a policy name to view the policy details or unbind it.

## Setting an Alarm

Tencent Cloud allows you to configure alarm and notification policies for your file system based on monitoring metrics. If you want to create or bind a policy for your file system, do so in the [Alarm Policy](https://console.cloud.tencent.com/monitor/policylist) page of the console.
In the **Cloud Monitoring** console, click **Alarm Configuration** > **Alarm Policy** to enter the alarm policy page. For more information, see [Create Alarm](https://intl.cloud.tencent.com/document/product/248/6126).

