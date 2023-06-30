## Overview
This document introduces how to adjust the resolution of the instance login via VNC through the CVM console.

If Windows system images have very low VNC resolutions, some applications may fail to be properly displayed or opened. To avoid these issues, you need to modify the resolutions of Windows system images.
Some Linux system images have lower VNC display resolutions by default. For example, the VNC resolution for CentOS is only 720 \* 400. You can set the VNC resolution to 1024 \* 768 by modifying the parameter `grub`.
<dx-alert infotype="explain" title="">
More recent Linux images such as CentOS 7, CentOS 8, Ubuntu, and Debian 9.0 adopt a default VNC resolution of 1024 \* 768, which can be used without any modifications.
</dx-alert>












## Prerequisites
You have logged in to the instance via VNC. For details, see the following documents:
 - [Logging into Windows Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 - [Logging into Linux Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32494).


## Directions

<dx-tabs>
::: Windows instances
<dx-alert infotype="explain" title="">
The steps below describe how to modify the VNC resolution of a Windows instance on the Windows Server 2012 operating system.
</dx-alert>



1. Right-click on the desktop and select **Screen resolution**, as shown below:
![](https://main.qcloudimg.com/raw/b8ec8e8ec22002532a4a517150079d2d.png)
2. In the “Screen Resolution” window, set **Resolution** to your desired value and click **Apply**, as shown below:
![](https://main.qcloudimg.com/raw/b90a33fa0600846888a15154f1e656dc.png)
3. In the pop-up window, click **Keep changes**.
4. Click **OK** to close the “Screen Resolution” window.


:::
::: Linux instances

The steps below describe how to modify the VNC resolution of a Linux instance on the CentOS 6 and Debian 7.8 operating systems.


#### CentOS 6

A CentOS 6 image has a VNC resolution of 720 \* 400 by default. To set its resolution to 1024 \* 768, modify the launch parameter `grub` as follows:
1. Run the following command to open the `/etc/grub.conf` file.
```
vi /etc/grub.conf
```
2. Press **i** to switch to the editing mode, and add `vga=792` to the parameter `grub`, as shown below:
![](https://main.qcloudimg.com/raw/3c2193fa370c48a7af149c63720da077.png)
3. Click **Esc** and enter **:wq** to save and close the file.
4. Run the following command to restart the CVM.
```
reboot
```



#### Debian 7.8

Both Debian 7.8 and Debian 8.2 images have VNC resolutions of 720 \* 400 by default. To set their resolutions to 1024 \* 768, modify the launch parameter `grub` as follows:
1. Run the following command to open the `grub` file.
```
vim /etc/default/grub
```
2. Press **i** to switch to the editing mode and add `vga=792` to the end of the parameter value `GRUB_CMDLINE_LINUX_DEFAULT`, as shown below:
![](https://main.qcloudimg.com/raw/f8e275c35b65b7b2d26cfbd7a8ae4dd6.png)
3. Click **Esc** and enter **:wq** to save and close the file.
4. Run the following command to update the `grub.cfg` file.
```
grub-mkconfig -o /boot/grub/grub.cfg
```
5. Run the following command to reboot the CVM.
```
reboot
```

:::
</dx-tabs>



## Appendix

The VGA parameter values corresponding to different Linux instance resolutions are listed below:
<table>
	<tr><th>Resolution</th><td>640 * 480</td><td>800 * 600</td><td>1024 * 768</td></tr>
	<tr><th>VGA</th><td>786</td><td>789</td><td>792</td></tr>
</table>
