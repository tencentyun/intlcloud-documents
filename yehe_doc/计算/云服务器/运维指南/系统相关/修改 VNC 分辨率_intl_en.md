## Overview

Some Linux system images have lower VNC display resolutions by default. For example, the VNC resolution for CentOS is only 720 \* 400. You can set the VNC resolution to 1024 \* 768 by modifying the parameter `grub`.
If Windows system images have very low VNC resolutions, some applications may fail to be properly displayed or opened. To avoid these issues, you need to modify the resolutions of Windows system images.

This document describes how to adjust the VNC display resolution of a CVM.

## Directions

### Modifying the VNC resolution of a Windows CVM instance

>? The steps below describe how to modify the VNC resolution of a Windows instance on the Windows Server 2012 operating system.

1. [Log in to a Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Right-click on the desktop and select **Screen resolution**, as shown below:
![](https://main.qcloudimg.com/raw/b8ec8e8ec22002532a4a517150079d2d.png)
3. In the “Screen Resolution” window, set **Resolution** to your desired value and click **Apply**, as shown below:
![](https://main.qcloudimg.com/raw/b90a33fa0600846888a15154f1e656dc.png)
4. In the pop-up window, click **Keep changes**.
5. Click **OK** to close the “Screen Resolution” window.

### Modifying the VNC resolution of a Linux CVM instance

More recent Linux images such as CentOS 7, CentOS 8, Ubuntu, and Debian 9.0 adopt a default VNC resolution of 1024 \* 768, which can be used without any modifications. The guide below introduces how to modify the VNC resolutions of Linux instances on the CentOS 6 and Debian 7.8 operating systems.

#### CentOS 6

A CentOS 6 image has a VNC resolution of 720 \* 400 by default. To set its resolution to 1024 \* 768, modify the launch parameter `grub` as follows:
- [Log in to a Linux Instance Using the Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:
 - [Log in to a Linux Instance via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Log in to a Linux Instance via a SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
 - [Log in to a Linux Instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to open the `/etc/grub.conf` file.
```
vi /etc/grub.conf
```
3. Press **i** to switch to the editing mode, and add `vga=792` to the parameter `grub`, as shown below:
![](https://main.qcloudimg.com/raw/3c2193fa370c48a7af149c63720da077.png)
4. Press **Esc**, enter **:wq**, and save and close the file.
5. Run the following command to reboot the CVM.
```
reboot
```

#### Debian 7.8

Both Debian 7.8 and Debian 8.2 images have VNC resolutions of 720 \* 400 by default. To set their resolutions to 1024 \* 768, modify the launch parameter `grub` as follows:
- [Log in to a Linux Instance Using the Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:
 - [Log in to a Linux Instance via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Log in to a Linux Instance via a SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
 - [Log in to a Linux Instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to open the `grub` file.
```
vi /etc/default/grub
```
3. Press **i** to switch to the editing mode and add `vga=792` to the end of the parameter value `GRUB_CMDLINE_LINUX_DEFAULT`.
![](https://main.qcloudimg.com/raw/f8e275c35b65b7b2d26cfbd7a8ae4dd6.png)
4. Press **Esc**, enter **:wq**, and save and close the file.
5. Run the following command to update the `grub.cfg` file.
```
grub-mkconfig -o /boot/grub/grub.cfg
```
6. Run the following command to reboot the CVM.
```
reboot
```


## Appendix

The table below compares the Linux instance's resolution and VGA parameters:
<table>
	<tr><th>Resolution</th><td>640 * 480</td><td>800 * 600</td><td>1024 * 768</td></tr>
	<tr><th>VGA</th><td>786</td><td>789</td><td>792</td></tr>
</table>
