## Scenario

Linux users sometimes need to boot into single user mode to perform some special operations, such as password management, sshd corruption, etc. This document describes how to boot into the single user mode in mainstream Linux operating systems.

## Directions

### Determining the Type of the Operating System

Follow different steps based on the type of the operating system.
 - For CentOS 6, follow [the steps for CentOS 6](#configCentOS6).
 - For CentOS 7, follow [the steps for CentOS 7](#configCentOS7).
 - For Ubuntu, follow [the steps for Ubuntu](#configUbuntu).

<span id="configCentOS6"></span>
### CentOS 6

> Centos 6 uses GRUB boot loader. The following steps use CentOS 6.9 as an example. Specific steps vary slightly depending on the version of the operating system.
> 
1. Log in to the CVM instance remotely.
2. Execute the following command to open the `/etc/grub.conf` file.
```
vi /etc/grub.conf
```
3. Press **I** to enter the insert mode.
4. Find “GRUB_TIMEOUT”, the parameter setting the length of waiting time before the default entry is booted, and modify its value based on your needs.
The default value of “GRUB_TIMEOUT” is 5 seconds. In order to avoid missing the boot interface because the waiting time is too short, it is recommended to modify it to 60s or longer.
> This item affects how long it takes for the system to start up. After you complete the configuration, modify it back to the default value.
5. Press **Esc** to exit the insert mode, type **:wq**, and press **Enter**.
Save your settings and exit the VI editor.
6. Execute the following command to reboot the server.
```
reboot
```
7. Wait for about 1 minute, then [log in to the CVM instance via VNC](https://intl.cloud.tencent.com/document/product/213/5436#.E4.BD.BF.E7.94.A8-vnc-.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B). The login interface is as shown below:
![](https://main.qcloudimg.com/raw/82a82601e1545274c4f61c8f34f5c100.png)
8. Press any key to enter the menu as shown below:
![](https://main.qcloudimg.com/raw/6336b8fd579799108a5765b5b58e2a21.png)
9. Press **e** to enter the kernel editing interface and enter **single** as shown below:
![](https://main.qcloudimg.com/raw/14168276d81a398702e80f9c83186869.png)
10. Press **Enter** as shown below:
![](https://main.qcloudimg.com/raw/149eeb5776329a5db1ea42ae20cd316d.png)
11. In the interface as shown below, press **b** to enter the single user mode.
![](https://main.qcloudimg.com/raw/2d6d53de84cd78b3e88319b8538cec8e.png)
12. Execute the following command to exit the single user mode.
```
exec /sbin/init
```

<span id="configCentOS7"></span>
### CentOS 7

> Unlike CentOS 6, CentOS version 7 and above use GRUB 2. The following steps use CentOS 7.5 as an example. Specific steps vary slightly depending on the version of the operating system.
> 
1. Log in to the CVM instance remotely.
2. Execute the following command to open the `/etc/default/grub` file.
```
vi /etc/default/grub
```
3. Press **I** to enter the insert mode.
4. Find “GRUB_TIMEOUT”, the parameter setting the length of waiting time before the default entry is booted, and modify its value based on your needs as shown below:
The default value of “GRUB_TIMEOUT” is 5 seconds. In order to avoid missing the boot interface because the waiting time is too short, it is recommended to modify it to 60s or longer.
> This item affects how long it takes for the system to start up. After you complete the configuration, modify it back to the default value.
>
![](https://main.qcloudimg.com/raw/5ee3b8d8a4609ca846e3c1e929608b34.png)
5. Press **Esc** to exit the insert mode, type **:wq**, and press **Enter**.
Save your settings and exit the VI editor.
6. Execute the following command to recompile and generate the grub.cfg file.
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
The returned result is as follows:
![](https://main.qcloudimg.com/raw/62da54e985f2f78efce045bb2da1e5e5.png)
7. Execute the following command to reboot the server.
```
reboot
```
8. Wait for about 1 minute, then [log in to the CVM instance via VNC](https://intl.cloud.tencent.com/document/product/213/5436#.E4.BD.BF.E7.94.A8-vnc-.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B). The login interface is as shown below:
![](https://main.qcloudimg.com/raw/95dba957dea2da680ffca516dc2b62b3.png)
9. Press **e** to enter the kernel editing interface and add **init=/bin/sh** to the red box area as shown below:
![](https://main.qcloudimg.com/raw/81173f4c723809f1b733a51a2eb002d5.png)
7. Press **Ctrl+X** to start and enter the single user mode as shown below:
![](https://main.qcloudimg.com/raw/b9004e2a1d58a9a09316cf2a8a907399.png)
8. Execute the following command to exit the single user mode.
```
exec /sbin/init
```

<span id="configUbuntu"></span>
### Ubuntu 

> The following steps use Ubuntu 16.04 as an example. Specific steps vary slightly depending on the version of the operating system.
>
1. Log in to the CVM instance remotely.
2. Execute the following command to open the `/etc/default/grub` file.
```
sudo vi /etc/default/grub
```
3. Press **I** to enter the insert mode.
4. Find “GRUB_TIMEOUT”, the parameter setting the length of waiting time before the default entry is booted, and modify its value based on your needs as shown below:
The default value of “GRUB_TIMEOUT” is 5 seconds. In order to avoid missing the boot interface because the waiting time is too short, it is recommended to modify it to 60s or longer.
> 
> - This item affects how long it takes for the system to start up. After you complete the configuration, modify it back to the default value.
> - The default account in Ubuntu is not root, please use the sudo commands.
> 
```
sudo vi /etc/default/grub
```
![](https://main.qcloudimg.com/raw/65553c2d5a01113e33b93caa93485dae.png)
3. Execute the following command to recompile and generate the grub.cfg file.
```
sudo update-grub
```
The returned result is as follows:
![](https://main.qcloudimg.com/raw/9e685185ef67e7129ce34b11b5a16061.png)
4. Execute the following command to reboot the server.
```
sudo reboot
```
5. Wait for about 1 minute, then [log in to the CVM instance via VNC](https://intl.cloud.tencent.com/document/product/213/5436#.E4.BD.BF.E7.94.A8-vnc-.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B). The login interface is as shown below:
![](https://main.qcloudimg.com/raw/4893e2a2ed32bbe4241b33b468bdb8cf.png)
6. Press **e** to enter the kernel editing interface and add **rw single init=/bin/bash** to the red box area as shown below:
![](https://main.qcloudimg.com/raw/0879dd0c8c7a720542352a0722f9b9a7.png)
7. Press **Ctrl+X** to start and enter the single user mode as shown below:
![](https://main.qcloudimg.com/raw/ffc6c3cf07a9254fdcb4f6326c3daf75.png)

