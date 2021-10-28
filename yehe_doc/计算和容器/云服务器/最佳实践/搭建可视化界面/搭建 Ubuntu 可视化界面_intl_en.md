## Overview
Virtual Network Console (VNC) is a remote control tool software developed by AT&T European Research Laboratory. An open-source software based on UNIX and Linux operating systems, VNC features robust remote control capability, high efficiency, and strong practicability. Its performance is comparable to any remote control software in Windows or Mac. This document will guide you through on how to build a visual Ubuntu desktop by using VNC.

## Prerequisites
You have purchased a Linux CVM with the Ubuntu OS. If not, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).


## Directions

1. [Log in to a Linux instance using VNC](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to switch to the “root” account.
```
sudo su root
```
3. Run the following command to obtain and update to the latest version.
```
apt-get update
```
4. Select and run the command below according to your system version to install VNC.
<dx-tabs>
::: Ubuntu 16.04/18.04
```
apt-get install vnc4server
```
:::
::: Ubuntu 20.04
```
apt-get install tightvncserver
```
:::
</dx-tabs>
5. <span id="step05"></span>Run the following command to launch VNC and set a password.
```
vncserver
```
If the result similar to the following is returned, it indicates that VNC has been launched successfully.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
6. Run the following command to install the X-windows base package.
```
sudo apt-get install x-window-system-core
```
7. Run the following system-specific command to install the login manager.
<dx-tabs>
::: Ubuntu 16.04/18.04
```
sudo apt-get install gdm
```
:::
::: Ubuntu 20.04
```
sudo apt-get install gdm3
```
:::
</dx-tabs>
8. Run the following command to install Ubuntu desktop.
```
sudo apt-get install ubuntu-desktop
```
During the installation, choose “gdm3” for `Default display manager:`.
9. Run the following command to install the GNOME supporting software.
```
sudo apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
```
10. Run the following command to access the VNC configuration file.
```
vi ~/.vnc/xstartup
```
11. Press **i** to enter edit mode, and modify the configuration file as follows.
```
#!/bin/sh
# Uncomment the following two lines for normal desktop:
export XKL_XMODMAP_DISABLE=1
 unset SESSION_MANAGER
# exec /etc/X11/xinit/xinitrc
unset DBUS_SESSION_BUS_ADDRESS
gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
```
12. Press **Esc** and enter **:wq** to save and close the file.
13. Run the following commands to restart the desktop process.
```
vncserver -kill :1 # Enter the command to terminate the original desktop process (wherein :1 is the number of the desktop)
```
```
vncserver :1 # Generate a new session
```
14. [Click here](https://www.realvnc.com/en/connect/download/viewer/) to download and install VNC Viewer. Select the version that matches your operating system.
15. Type `CVM IP address: 1` into VNC Viewer, and press **Enter**.
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
16. Click **Continue** in the pop-out dialog box.
17. Enter the VNC password set in [Step 5](#step05) and click **OK**.
>? In case of connection timeout, check the network connection and security group configurations. Create an inbound rule `TCP:5901` for the security group to open the listening port 5901 of the VNC Server. For detailed directions, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).









