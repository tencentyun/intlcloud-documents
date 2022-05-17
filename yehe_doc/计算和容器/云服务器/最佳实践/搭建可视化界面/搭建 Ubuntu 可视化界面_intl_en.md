## Overview
Virtual Network Console (VNC) is a remote control tool software developed by AT&T European Research Laboratory. An open-source software based on UNIX and Linux operating systems, VNC features robust remote control capability, high efficiency, and strong practicability. Its performance is comparable to any remote control software in Windows or Mac. This document will guide you through on how to build a visual Ubuntu desktop by using VNC.

## Prerequisites
You have purchased a Linux instance with the Ubuntu OS; if not, please see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/zh/document/product/213/10517).


## Directions


### Configuring instance security group

The VNC service uses the TCP protocol and port 5901 by default. Therefore, you need to open port 5901 in the security group bound to the instance by adding a rule for opening protocol port `TCP:5901` in **Inbound Rules**. For more information, please see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).


### Installing software packages
1. [Log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to switch to the "root" account.
```
sudo -i
```
3. Run the following command to obtain and update to the latest version.
```
apt-get update
```
4. Run the following command to install the software packages required by the desktop environment, including desktop applications such as system panel, window manager, file browser, and terminal.
```bash
apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
```



### Configuring VNC

1. Run the following system-specific command to install VNC.
<dx-tabs>
::: Ubuntu 18.04
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
2. [](id:step02)Run the following command to launch VNC and set a password.
```
vncserver
```
If the result similar to the following is returned, it indicates that VNC has been launched successfully.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
3. Run the following command to access the VNC configuration file.
```
vi ~/.vnc/xstartup
```
4. Press **i** to enter edit mode, and modify the configuration file as follows.
```
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"
gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
```
5. Press **Esc** and enter **:wq**. Save and close the file.
6. Run the following commands to restart the desktop process.
```
vncserver -kill :1 # Enter the command to terminate the original desktop process (wherein :1 is the number of the desktop)
```
```
vncserver -geometry 1920x1080 :1 # Generate a new session
```
7. [Click here](https://www.realvnc.com/en/connect/download/viewer/) to download and install VNC Viewer. Select the version that matches your operating system.
8. Type `CVM IP address: 1` into VNC Viewer, and press **Enter**.
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
9. In the pop-up window, click **Continue**.
10. Enter the VNC password set in [step 2](#step02) and click **OK**.



