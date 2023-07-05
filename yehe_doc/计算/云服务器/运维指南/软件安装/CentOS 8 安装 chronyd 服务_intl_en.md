## Overview
Currently, native CentOS 8 does not support setting the NTP service. Instead, you need to use chronyd to deliver accurate time. This document describes how to install and configure chronyd on a CentOS 8-based Tencent Cloud CVM instance.

## Directions
### Installing and configuring the chronyd service
1. [Log in to a Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to install the chronyd service.
```
yum -y install chrony
```
3. Run the following command to modify the `chrony.conf` configuration file.
```
vim /etc/chrony.conf
```
4. Press **i** to enter the edit mode, and append the following content to the next line of `#log measurements statistics tracking`.
```
server time1.tencentyun.com iburst
server time2.tencentyun.com iburst
server time3.tencentyun.com iburst
server time4.tencentyun.com iburst
server time5.tencentyun.com iburst
```
The result should be as follows:
![](https://main.qcloudimg.com/raw/578e072599f8d50ea188d3911a9d76c7.png)
5. Press **Esc** and enter **:wq** to save and close the file.
6. Run the following commands in sequence to enable chronyd autostart and restart it.
```
systemctl restart chronyd
```
```
systemctl enable chronyd
```

### Verifying the configurations
1. Run the following command to check whether the clock is synced.
```
date
```
2. Run the following command to check the clock source status.
```
chronyc sourcestats -v
```
If a result similar to the following is returned, the configuration was successful.
![](https://main.qcloudimg.com/raw/6a5f584638de922f5e80b5b138541c9e.png)

## Appendix
### Commands
<table>
<tr>
<th>Command</th><th>Description</th>
</tr>
<tr>
<td>
<code>chronyc sources -v</code>
</td>
<td>Check the clock source.</td>
</tr>
<tr>
<td>
<code>chronyc sourcestats -v</code>
</td>
<td>Check the clock source status.</td>
</tr>
<tr>
<td>
<code>timedatectl set-local-rtc 1</code>
</td>
<td>Set the real time clock. The default format is UTC.
</td>
</tr>
<tr>
<td>
<code>timedatectl set-ntp yes</code>
</td>
<td>Enable the NTP service for synchronization.</td>
</tr>
<tr>
<td>
<code>chronyc tracking</code>
</td>
<td>Calibrate the NTP server.</td>
</tr>
<tr>
<td>
<code>chronyc -a makestep</code>
</td>
<td>Force synchronization of the system clock.</td>
</tr>
</table>
