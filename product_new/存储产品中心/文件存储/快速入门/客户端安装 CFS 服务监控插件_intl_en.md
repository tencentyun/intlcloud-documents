## Overview
The CFS service monitoring plugin is a plugin integrated with the Cloud Monitor component to monitor the performance of CFS file systems and client connections. You are strongly recommended to install it on your clients such as CVM or TKE instances to better manage the CFS service.

>Before installing the plugin, please make sure that your client has the Cloud Monitor component installed. For more information, please see [Installing Cloud Monitor Component](https://intl.cloud.tencent.com/document/product/248/6211).

## OS Support

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

Log in to the [CFS Console](https://console.cloud.tencent.com/cfs), click a file system name to enter the file system details page, and select **Mounted Clients** to view the information of the clients to which the file system is mounted. If the plugin has not been installed on a client, no information will be available.
>Client information display may have a delay of 1–3 minutes.
