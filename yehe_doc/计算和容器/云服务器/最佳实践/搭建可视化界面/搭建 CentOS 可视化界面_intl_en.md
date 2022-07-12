## Overview
This document describes how to build a visual CentOS desktop on CVM instances with CentOS 8.2 or CentOS 7.9 installed.

## Notes
- By default, Tencent Cloud Linux public images are not provided with a GUI component.
- Improper GUI component installation may cause a CVM startup failure. We recommend you to first back up data by [creating custom images](https://intl.cloud.tencent.com/document/product/213/4942) or [creating snapshots](https://intl.cloud.tencent.com/document/product/362/5755).

## Directions
Perform the following operations according to the operating system version of your CVM instance.
<dx-tabs>
::: CentOS\s8.2
1. [Log in to the Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to install the GUI component.
```
yum groupinstall "Server with GUI" -y
```
3. Run the following command to set the default GUI.
```
systemctl set-default graphical
```
4. Run the following command to restart the instance.
```
reboot
```
5. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
If the GUI page appears, it has been successfully set up. Follow the instructions to enter the desktop and continue other operations.
![](https://main.qcloudimg.com/raw/58e12a33b38e0114f5b3116b31f7b026.png)
:::
::: CentOS\s7.9
1. [Log in to the Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to install the GUI component.
```
yum groupinstall "GNOME Desktop" "Graphical Administration Tools" -y
```
3. Run the following command to set the default GUI.
```
ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
```
4. Run the following command to restart the instance.
```
reboot
```
5. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
If the GUI page appears, it has been successfully set up. Follow the instructions to enter the desktop and continue other operations.
![](https://qcloudimg.tencent-cloud.cn/raw/246952ae60c02724727029b6a3c0ef1a.png)
:::
</dx-tabs>
