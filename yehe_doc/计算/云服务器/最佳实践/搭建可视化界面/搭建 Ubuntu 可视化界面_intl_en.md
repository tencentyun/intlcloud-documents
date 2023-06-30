## Scenarios
Virtual Network Console (VNC) is a remote control tool software developed by AT&T European Research Laboratory. An open-source software based on UNIX and Linux operating systems, VNC features robust remote control capability, high efficiency, and strong practicability. Its performance is comparable to any remote control software in Windows or Mac. This document will guide you through on how to build a visual Ubuntu desktop by using VNC.

## Prerequisite
Purchase a Linux CVM using Ubuntu OS.

## Directions


### Configuring instance security group

The VNC service uses the TCP protocol and port 5901 by default. Therefore, you need to add a rule to open TCP:5901 in the security group bound to the instance. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).


### Installing software packages

<dx-tabs>
::: Ubuntu 18.04
1. [Log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to clear the cache and update the software package list.
```shellsession
sudo apt clean all && sudo apt update
```
3. Run the following command to install the software packages required by the desktop environment, including desktop applications such as system panel, window manager, file browser, and terminal.
```shellsession
sudo apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
```
4. Run the following command to install VNC.
```shellsession
apt-get install vnc4server
```
:::
::: Ubuntu 20.04
1. [Log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to clear the cache and update the software package list.
```shellsession
sudo apt clean all && sudo apt update
```
3. Run the following command to install the software packages required by the desktop environment, including desktop applications such as system panel, window manager, file browser, and terminal.
```shellsession
sudo apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
```
4. Run the following command to install VNC.
```shellsession
apt-get install tightvncserver
```
:::
::: Ubuntu 22.04
1. [Log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436).
2. Clear the cache and update the software package list.
```shellsession
sudo apt clean all && sudo apt update
```
3. Install the desktop environment.
```shellsession
sudo apt install xfce4 xfce4-goodies
```
4. Run the following command to install VNC.
```shellsession
sudo apt install tightvncserver
```
:::
</dx-tabs>

### Configuring VNC
<dx-tabs>
::: Ubuntu 18.04
1. [](id:step02)Run the following command to launch VNC and set a password.
```shellsession
vncserver
```
If the result similar to the following is returned, it indicates that VNC has been launched successfully.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
2. Run the following command to access the VNC configuration file.
```shellsession
vi ~/.vnc/xstartup
```
3. Press **i** to enter edit mode, and modify the configuration file as follows.
```shellsession
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"
gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
```
4. Click **Esc** and enter **:wq** to save and close the file.
5. Run the following commands to restart the desktop process.
```shellsession
vncserver -kill :1 # Enter the command to terminate the original desktop process (wherein :1 is the number of the desktop)
```
```shellsession
vncserver -geometry 1920x1080 :1 # Generate a new session
```
6. [Click here](https://www.realvnc.com/en/connect/download/viewer/) to download and install VNC Viewer. Select the version that matches your operating system.
7. Type `CVM IP address: 1` into VNC Viewer, and press **Enter**.
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
8. In the pop-up window, click **Continue**.
9. Enter the VNC password set in [step 2](#step02) and click **OK**.

:::


::: Ubuntu 20.04
1. [](id:step03)Run the following command to launch VNC and set a password.
```shellsession
vncserver
```
If the result similar to the following is returned, it indicates that VNC has been launched successfully.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
2. Run the following command to access the VNC configuration file.
```shellsession
vi ~/.vnc/xstartup
```
3. Press **i** to enter edit mode, and modify the configuration file as follows.
```shellsession
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"
gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
```
4. Click **Esc** and enter **:wq** to save and close the file.
5. Run the following commands to restart the desktop process.
```shellsession
vncserver -kill :1 # Enter the command to terminate the original desktop process (wherein :1 is the number of the desktop)
```
```shellsession
vncserver -geometry 1920x1080 :1 # Generate a new session
```
6. [Click here](https://www.realvnc.com/en/connect/download/viewer/) to download and install VNC Viewer. Select the version that matches your operating system.
7. Type `CVM IP address: 1` into VNC Viewer, and press **Enter**.
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
8. In the pop-up window, click **Continue**.
9. Enter the VNC password set in [step 2](#step03) and click **OK**.

:::

::: Ubuntu 22.04
[](id:g1)
1. Run the following command to launch VNC and set a password.
```shellsession
vncserver
```
If the result similar to the following is returned, it indicates that VNC has been launched successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/5fb63d9cc28d3a0cebd5def424051e7a.png)
2. Go to the [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) official website, download and install VNC Viewer of the version that matches your operating system.
3. Type `CVM IP address: 1` into VNC Viewer, and press **Enter**.
![](https://qcloudimg.tencent-cloud.cn/raw/3e7d432ce674a8587066df25f42595bf.png)
4. In the pop-up window, click **Continue**.
5. Enter the password created in the previous step and click **OK**.
 <dx-alert infotype="notice" title="">
If you forgot the password, log in to the instance and execute `vncpasswd` to resetthe VNC login password.
 </dx-alert>
 Appendix:
Install Chrome:
 - Log in to the instance and execute the following command to download **.deb**:  
```shellsession
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
 - Install **.deb** file
```shellsession
sudo apt install ./google-chrome-stable_current_amd64.deb
```
:::
</dx-tabs>
