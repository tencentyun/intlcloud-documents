## Overview

The Network Time Protocol daemon (NTPD) is a daemon of Linux operating systems, and also a complete implementation of the NTP protocol. You can use it to synchronize time between the local system and time source servers. Unlike NTPDate which updates time periodically, NTPD corrects time continuously without time gaps. This document describes how to install and configure NTPD on CentOS 7.5.

## Notes

- Some operating systems use chrony as the default NTP service. Please make sure that NTPD is running and is configured to launch automatically at startup.
 - Run the `systemctl is-active NTPD.service` command to see if NTPD is running.
 - Run the `systemctl is-enabled NTPD.service` command to see if NTPD is configured to launch automatically at startup.
- The NTP service communicates on the port UDP 123. Please make sure that you have opened the port to the Internet before configuring the NTP service.
If the port is not open, please refer to [Adding Security Group Policies](https://intl.cloud.tencent.com/document/product/213/34272) to open it to the Internet.

## Directions

### Installing NTPD

Run the following command to check whether NTPD has been installed.
```
rpm -qa | grep ntp
```
 - If the following result is returned, NTPD has been installed.
![Checking if NTPD has been installed](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
 - If NTPD has not been installed, run the `yum install ntp` command to install it. 
```
yum -y install ntp
```
NTPD uses the client mode by default.

### Configuring NTP
1. Run the following command to open the configuration file of the NTP service.
```
vi /etc/ntp.conf
```
2. Press **i** to enter the edit mode and locate the `server` configurations. Change the value of `server` to the NTP clock source server you want to use (such as `time1.tencentyun.com`), and delete unwanted values, as shown below:
![Server configuration](https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)
3. Press **Esc** and enter **:wq** to save and close the file.

### Launching NTPD

Run the following command to restart the NTPD service.
```
systemctl restart ntpd.service
```

### Checking the status of NTPD

Run the following commands to check for the NTPD status according to your needs. 
- Run the following command to check whether the NTP is normally listening on the service port UDP 123.
```
netstat -nupl
```
If the following result is returned, the listening is normal.
![netstat -nupl](https://main.qcloudimg.com/raw/d7da764d05135959154920b81fa9f1e4.png)
- Run the following command to check whether the NTPD status is normal.
```
service NTPD status
```
If the following result is returned, the NTPD status is normal.
![NTPD status](https://main.qcloudimg.com/raw/321e56d0f7797f382d9f6903c0315f96.png)
- Run the following command to check whether NTP has been started normally and configured to the correct NTP clock source server.
```
ntpstat
```
The IP address of the current NTP clock source server that is configured earlier is returned, as shown below:
![](https://main.qcloudimg.com/raw/a99f5da438bafb1d148e9b033f48afad.png)
You can also get the IP address corresponding to the domain name by running the command `nslookup domain name`.
- Run the following command to get NTP service details.
```
ntpq -p
```
The following result will be returned:
![](https://main.qcloudimg.com/raw/ca9ef4caf98b49ed2c9110198a66e7c3.png)
 - **remote**: the name of the NTP server that responds to this request.
 - **refid**: the NTP server one stratum above to which the NTP server on this stratum is synchronized.
 - **st**: the stratum of the remote server. The stratum of a server can be set to 1 to 16 from the top to the bottom. In order to relieve the load and network congestion, in principle, you should avoid connecting directly to a stratum 1 server.
 - **when**: how many seconds have elapsed since the last successful request.
 - **poll**: the synchronization interval (in seconds) between local and remote servers. At the beginning, the `poll` value will be smaller, which means a higher frequency of synchronization, so that the time can be adjusted to the correct time range as soon as possible. Later, the `poll` value will gradually increase, and the synchronization frequency will be lower accordingly.
 - **reach**: an octal value used to test whether the server can be connected. Its value increases every time when the server is successfully connected.
 - **delay**: the round trip time of sending the synchronization request from the local machine to the NTP server.
 - **offset**: the time difference in milliseconds (ms) between the host and the time source through NTP. If its value is closer to 0, the time on the host approaches to that of the NTP server more.
 - **jitter**: a value used for statistics which records the distribution of offsets over a particular number of consecutive connections. The smaller its absolute value, the more accurate the host time.

### Setting the automatic launch of NTPD at startup

1. Run the following command to automatically launch NTPD at startup.
```
systemctl enable ntpd.service
```
2. Run the following command to check whether chrony is set to launch at startup.
```
systemctl is-enabled chronyd.service
```
If chrony is set to launch at startup, run the following command to remove chrony from the auto-start list.
chrony is not compatible with NTPD, which may lead to NTPD start failure.
```
systemctl disable chronyd.service
```

### Enhancing NTPD security

Run the following command sequentially to add security to the `/etc/ntp.conf` configuration file.
```
interface ignore wildcard
```
```
interface listen eth0
```
