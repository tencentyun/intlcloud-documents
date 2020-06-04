## Scenario

Some of Linux system images have lower VNC display resolution by default, even only 720 \* 400 for CentOS 6. You can set the VNC resolution to 1024 \* 768 by modifying the parameter `grub`.
If Windows system images have a very low VNC resolution, their applications may be unable to properly display or open. To avoid these issues, you need to modify the resolution.

This document guides you through on how to adjust the VNC display resolution of CVMs.

## Directions

### Modifying the VNC resolution of Windows CVM instances

> The guide below introduces how to modify the VNC resolution of Windows instances on the Windows Server 2012 operating system.
>

1. [Log in to Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Right-click on the desktop and select **Display resolution**, as shown below:
![](https://main.qcloudimg.com/raw/b8ec8e8ec22002532a4a517150079d2d.png)
3. In the “Display” window, set **Resolution** to the desirable value and click **Apply**, as shown below:
![](https://main.qcloudimg.com/raw/b90a33fa0600846888a15154f1e656dc.png)
4. In the pop-up window, click **Keep changes**.
5. Click **OK** to close the “Display” window.

### Modifying the VNC resolution of  Linux CVM instances

More recent Linux images such as CentOS 7, CentOS 8, Ubunt, and Debian 9.0, adopt a default VNC resolution of 1024 \* 768, which can be used without any modification. The guide below introduces how to modify the VNC resolution of Linux instances on CentOS 6 and Debian 7.8 operating systems.

### CentOS 6

CentOS 6 image has a VNC resolution of 720 \* 400 by default. To set its resolution to 1024 \* 768, you can modify the launch parameter `grub` as follows:
- [Log in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
 - [Logging in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Logging in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
 - [Logging in to Linux Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to open the `/etc/grub.conf` file.
```
vi /etc/grub.conf
```
3. Press **i** to switch to the edit mode, and add `vga=792` to the parameter `grub`, as shown below:
![](https://main.qcloudimg.com/raw/3c2193fa370c48a7af149c63720da077.png)
4. Press **Esc**, enter **:wq**, save the file and return.
5. Run the following command to reboot the CVM.
```
reboot
```

#### Debian 7.8

Both Debian 7.8 and Debian 8.2 images have a VNC resolution of 720 \* 400 by default. To set their resolution to 1024 \* 768, you can modify the launch parameter `grub` as follows:
- [Log in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
 - [Logging in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Logging in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
 - [Logging in to Linux Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to open the `grub` file.
```
vi /etc/default/grub
```
3. Press **i** to switch to the edit mode and append the parameter value `GRUB_CMDLINE_LINUX_DEFAULT` with `vga=792`.
![](https://main.qcloudimg.com/raw/f8e275c35b65b7b2d26cfbd7a8ae4dd6.png)
4. Press **Esc**, enter **:wq**, save the file and return.
5. Run the following command to update the `grub.cfg` file.
```
grub-mkconfig -o /boot/grub/grub.cfg
```
6. Run the following command to reboot the CVM.
```
reboot
```


## Appendix

The table below lists the relationships between resolution and VGA.
<table>
	<tr><th>Resolution</th><td>640 * 480</td><td>800 * 600</td><td>1024 * 768</td></tr>
	<tr><th>VGA</th><td>786</td><td>789</td><td>792</td></tr>
</table>
