## Overview
CFS monitoring plugin is a plugin integrated with Tencent Cloud CVM Agent for monitoring the performance of CFS file systems and client connections. You are strongly recommended to install it on your clients such as CVM or TKE instances for better use of CFS.

>!Before installing the plugin, please make sure that your client has Tencent Cloud CVM Agent installed. For more information, please see [Installing CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211).

## OS Support

Currently, the CFS monitoring plugin **supports clients mounted over NFS, but not over CIFS/SMB**, and the following operating systems. There may be compatibility issues with other kernel versions of Linux.


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
>!There may be a delay of 1-3 minutes before you can see the client list.
