## Overview

Before using the CFS monitoring feature, you need to install the CFS service monitoring plugin on your clients such as CVM or TKE instances to better manage the CFS service.

## Installing Monitoring Plugin


#### Prerequisites
The CFS service monitoring plugin is a plugin integrated with the Cloud Monitor component to monitor the performance of CFS file systems and client connections.

>Before installing the plugin, please make sure that your client has the Cloud Monitor component installed. For more information, please see [Installing Cloud Monitor Component](https://intl.cloud.tencent.com/document/product/248/6211).

#### OS support
Currently, the CFS service monitoring plugin **supports monitoring of clients mounted with NFS (CIFS/SMB not supported)** and the following operating systems. There may be compatibility issues with other kernel editions of Linux.



<table>
   <tr>
      <th>OS</th>
      <th>Edition</th>
   </tr>
   <tr>
      <td rowspan=7>CentOS</td>
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

You can log in to the Linux-based instance and follow the steps below to obtain and install the CFS service monitoring plugin: [Download the plugin](#step1) > [Modify the plugin format](#step2) > [Install the plugin](#step3).

<span id="step1"></span>

#### Download the plugin

You can run the command below to download the CFS service monitoring plugin to the current directory of the client.

```sh
## Downloading CFS Service Monitoring Plugin
wget http://mirrors.tencentyun.com/install/cfs/cfs_barad_plugin_installer_release_v11
```

<span id="step2"></span>

#### Modify the plugin format

You can run the following command to change the CFS service monitoring plugin to an executable format.

```sh
## Modifying File Type
chmod +x cfs_barad_plugin_installer_release_v11
```

<span id="step3"></span>

#### Installing the plugin

You can run the following command to install the CFS service monitoring plugin. A success message will be returned if the installation is successful.

```sh
## Installing Plugin
./cfs_barad_plugin_installer_release_v11
```

After successful installation, `cfs barad plugin install success` will be displayed as shown below:
![](https://main.qcloudimg.com/raw/d4138a9caa55d3b2ef030f658b3e86e9.png)

>For Ubuntu clients, root privileges are required, that is, `sudo` needs to be added before the command.

## Installing on Windows

Windows clients are not supported currently.

## Monitoring Visiting Client

Log in to the [CFS Console](https://console.cloud.tencent.com/cfs), click a file system name to enter the file system details page, and click **Mounted Clients** to view the information of the clients to which the file system is mounted. If the plugin has not been installed on a client, no information will be available.

>Client information display may have a delay of 1–3 minutes.


## Performance Monitoring

Log in to the [CFS Cloud Monitor Console](https://console.cloud.tencent.com/monitor/product/cfs) and click **Cloud Monitor** > **Cloud Product Monitoring** > **CFS** to view the health status of each file system and alarm information on the CFS monitoring page.

#### Viewing file system performance monitoring

Click any file system ID/name in the figure above to enter the details page. You can select the corresponding time window to view the usage of the monitored file system.

The monitoring metrics supported by CFS are as follows:

| Metric Name  |  Description   | Unit   | Level |
| ------------ | ------------------------------ | ---- | ---------- |
| Storage capacity | File system storage capacity at the current time | GB | Single file system |
| Read bandwidth | Average amount of data read from the file system per second | KB/s | Single file system |
| Write bandwidth | Average amount of data written to the file system per second | KB/s | Single file system |
| Read IOPS  | Average number of reads from the file system per second  | Reads/second | Single file system |
| Write IOPS  | Average number of write operations on the file system per second  | Writes/second | Single file system |

>Because of the local cache on the client, the **read bandwidth** and **read IOPS** of the file system obtained by Cloud Monitor may be slightly less than the actual usage.

#### Viewing file system alarm policy

You can enter the alarm policy page to view the alarm policy bound to the file system. Click the policy name to view the policy details or unbind it.

## Setting an Alarm

Tencent Cloud allows you to configure alarm and notification policies for your file system based on monitoring metrics. If you want to create a policy or bind a policy to the file system, please enter the [Cloud Monitor Alarm Policy](https://console.cloud.tencent.com/monitor/policylist) page.
Click **Cloud Monitor** > **Manage Alarms** > **Alarm Policy** to enter the alarm policy page. For more information, please see [Cloud Monitor Alarm Service Guide](https://intl.cloud.tencent.com/document/product/248/6126).

