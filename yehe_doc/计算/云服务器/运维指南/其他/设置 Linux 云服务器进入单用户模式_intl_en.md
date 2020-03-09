## Scenario

Linux users sometimes need to boot into single user mode to perform special operations, such as password management or sshd repair. This article describes how to boot into single user mode in common Linux distributions.

## Directions

### Determining your Linux distribution

Different distributions of Linux use different methods to boot into single user mode, so be sure to follow the instructions for your Linux distribution.
 - [Process for CentOS 6](#configCentOS6).
 - [Process for CentOS 7](#configCentOS7).
 - [Process for Ubuntu](#configUbuntu).

<span id="configCentOS6"></span>
### CentOS 6

> CentOS 6 uses GRUB. The following process uses CentOS 6.9 as an example. Specific steps may vary slightly depending on the version of the operating system.
> 
1. Log in to the CVM.
2. Run the following command to open `/etc/grub.conf`.
```
vi /etc/grub.conf
```
3. Press **i** to enter edit mode.
4. Find “GRUB_TIMEOUT”, the waiting time before the default entry is booted, and modify its value based on your needs.
The default value of “GRUB_TIMEOUT” is 5 seconds. In order to avoid missing the boot interface because the waiting time is too short, we recommend you change it to 60s or longer.
> This setting affects the system start time. After you complete the tasks that require single user mode, change it back to the default value.
>
5. Press **Esc** to exit edit mode, enter **:wq**, and press **Enter** to
save your file and exit the VI editor.
6. Run the following command to reboot the server.
```
reboot
```
7. Wait for one minute and [use VNC to log into your CVM instance](https://intl.cloud.tencent.com/document/product/213/32494), as shown below:
![](https://main.qcloudimg.com/raw/82a82601e1545274c4f61c8f34f5c100.png)
8. Press any key to enter the menu shown below:
![](https://main.qcloudimg.com/raw/6336b8fd579799108a5765b5b58e2a21.png)
9. Press **e** to enter the kernel editing page and enter **single**, as shown below:
![](https://main.qcloudimg.com/raw/14168276d81a398702e80f9c83186869.png)
10. Press **Enter**, as shown below:
![](https://main.qcloudimg.com/raw/149eeb5776329a5db1ea42ae20cd316d.png)
11. In the interface shown below, press **b** to enter single user mode.
![](https://main.qcloudimg.com/raw/2d6d53de84cd78b3e88319b8538cec8e.png)
12. Run the following command to exit single user mode.
```
exec /sbin/init
```

<span id="configCentOS7"></span>
### CentOS 7

>Unlike CentOS 6, CentOS 7 and above use GRUB 2. The following process uses CentOS 7.5 as an example. Specific steps may vary slightly depending on the version of the operating system.
> 
1. Log in to the CVM.
2. Run the following command to open `/etc/default/grub`.
```
vi /etc/default/grub
```
3. Press **i** to enter edit mode.
4. Find “GRUB_TIMEOUT”, the default boot item wait time, and modify its value based on your needs, as shown below:
The default value of “GRUB_TIMEOUT” is 5 seconds. In order to avoid missing the boot interface because the waiting time is too short, we recommend you change it to 60s or longer.
> This setting affects the system start time. After you complete the tasks that require single user mode, change it back to the default value.
>
![](https://main.qcloudimg.com/raw/5ee3b8d8a4609ca846e3c1e929608b34.png)
5. Press **Esc** to exit edit mode, enter **:wq**, and press **Enter** to
save your file and exit the VI editor.
6. Run the following command to recompile and generate `grub.cfg`.
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
The following appears:
![](https://main.qcloudimg.com/raw/62da54e985f2f78efce045bb2da1e5e5.png)
7. Run the following command to reboot the server.
```
reboot
```
8. Wait for one minute and [use VNC to log into your CVM instance](https://intl.cloud.tencent.com/document/product/213/32494), as shown below:
![](https://main.qcloudimg.com/raw/95dba957dea2da680ffca516dc2b62b3.png)
9. Press **e** to enter the kernel editing interface and add **init=/bin/sh** to the red box area as shown below:
![](https://main.qcloudimg.com/raw/81173f4c723809f1b733a51a2eb002d5.png)
7. Press **Ctrl+X** to start and enter single user mode, as shown below:
![](https://main.qcloudimg.com/raw/b9004e2a1d58a9a09316cf2a8a907399.png)
8. Run the following command to exit single user mode.
```
exec /sbin/init
```

<span id="configUbuntu"></span>
### Ubuntu 

> The following process uses Ubuntu 16.04 as an example. Specific steps may vary slightly depending on the version of the operating system.
>
1. Log in to the CVM.
2. Run the following command to open `/etc/default/grub`.
```
sudo vi /etc/default/grub
```
3. Press **i** to enter edit mode.
4. Find “GRUB_TIMEOUT”, the default boot item wait time, and modify its value based on your needs, as shown below:
The default value of “GRUB_TIMEOUT” is 5 seconds. In order to avoid missing the boot interface because the waiting time is too short, we recommend you change it to 60s or longer.
> 
> - This setting affects the system start time. After you complete the tasks that require single user mode, change it back to the default value.
> - The default account in Ubuntu is not `root`. Use `sudo` instead.
> 
![](https://main.qcloudimg.com/raw/65553c2d5a01113e33b93caa93485dae.png)
5. Press **Esc** to exit edit mode, enter **:wq**, and press **Enter** to
save your file and exit the VI editor.
6. Run the following command to recompile and generate `grub.cfg`.
```
sudo update-grub
```
The following appears:
![](https://main.qcloudimg.com/raw/9e685185ef67e7129ce34b11b5a16061.png)
6. Run the following command to reboot the server.
```
sudo reboot
```
7. Wait for one minute and [use VNC to log into your CVM instance](https://intl.cloud.tencent.com/document/product/213/32494), as shown below:
![](https://main.qcloudimg.com/raw/4893e2a2ed32bbe4241b33b468bdb8cf.png)
8. Press **e** to enter the kernel editing interface and add **rw single init=/bin/bash** to the red box area as shown below:
![](https://main.qcloudimg.com/raw/0879dd0c8c7a720542352a0722f9b9a7.png)
9. Press **Ctrl+X** to start and enter single user mode, as shown below:
![](https://main.qcloudimg.com/raw/ffc6c3cf07a9254fdcb4f6326c3daf75.png)

