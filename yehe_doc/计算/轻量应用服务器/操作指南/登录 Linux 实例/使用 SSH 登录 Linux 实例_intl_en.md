## Overview
This document describes how to use an SSH key to log in to a Linux Lighthouse instance from a Linux, macOS, or Windows computer.

## Supported Operating Systems
Linux, macOS, and Windows (Windows 10 and Windows Server 2019).

## Authentication Method
**Password** or **Key**

## Prerequisites[](id:Prerequisites)
- You have obtained the username (custom username or default username *root*) and password (or key) to log in to the instance.
<dx-alert infotype="notice" title="">
If it is your first time to log in to a Linux instance through the local SSH client, you need to reset the password of the default username (*root*) or bind your key. For detailed directions, see [Resetting Password](https://intl.cloud.tencent.com/document/product/1103/41553) and [Managing Keys](https://intl.cloud.tencent.com/document/product/1103/41392).
</dx-alert>
- Make sure the network connection between the local computer and the instance is working, and the port 22 is open in the firewall policies of the instance (Port 22 is open by default upon the creation of the instance).


## Directions

<dx-tabs>
::: Password login
1. Run the following command to connect to your Linux instance.
<dx-alert infotype="explain" title="">
- Linux distribution without GUI: Run the following command on the system interface directly
- Linux distribution with GUI or macOS: Open the command line interface that comes with the system (e.g., Terminal on macOS) before running the following command
- Windows 10 or Windows Server 2019: Open the command prompt (CMD) before running the following command
</dx-alert>
```
ssh <username>@<IP address or domain name>
```
 - `username` is the obtained username in [Prerequisites](#Prerequisites), such as `root` and `ubuntu`.
 - `IP address or domain name` is the public IP address or custom domain of your Linux instance. You can view the instance's public IP address in the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Enter the password you have obtained, and press Enter to log in.


:::
::: SSH key login
1. Execute the following command to set the private key file readable only to you.
 - macOS: Open the terminal that comes with the system before executing the following command.
 - Linux: Directly execute the following command.
```
chmod 400 <absolute path of the downloaded private key associated with the instance>
```
 - Windows 10 or Windows Server 2019: Open the command prompt (CMD) first and run the following commands in sequence.
```
icacls <path of the downloaded private key file associated with the instance> /grant <Windows system user account>:F
```
```
icacls <path of the downloaded private key file associated with the instance> /inheritancelevel:r
```
2. Execute the following command for remote login.
```
ssh -i <path of the downloaded private key file associated with the instance> <username>@<IP address or domain name>
```
 - `username` is the obtained username in [Prerequisites](#Prerequisites), such as `root` and `ubuntu`.
 - `IP address or domain name` is the public IP address or custom domain of your Linux instance. You can view the instance's public IP address in the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).

  For example, run the `ssh -i /Users/macuser/Downloads/test_private_key root@35.222.45.145` command on macOS to remotely log in to the Linux instance.

:::
</dx-tabs>

