## Overview

The Network Time Protocol daemon (ntpd) is a daemon of the Linux operating system. It is a complete implementation of NTP and is used to correct the time difference between the local system and the clock source server. Unlike ntpdate, which updates time periodically, ntpd corrects time continuously without time gaps. This document uses CentOS 7.5 as an example to describe how to install and configure ntpd.

## Notes

- Some operating systems use chrony as the default NTP service. Please make sure that ntpd is running and is configured to launch automatically at startup.
 - Run the `systemctl is-active ntpd.service` command to see if ntpd is running.
 - Run the `systemctl is-enabled ntpd.service` command to see if ntpd is configured to launch automatically at startup.
- The communication port of the NTP service is UDP 123. Please make sure that you have opened the port to the Internet before configuring the NTP service.
If the port is not open, please refer to [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272) to open it to the Internet.

## Directions

### Installing ntpd

Run the following command to check whether ntpd has been installed.
```
rpm -qa | grep ntp
```
 - If the following result is returned, ntpd has been installed.
![Checking if ntpd has been installed](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
 - If ntpd has not been installed, run the `yum install ntp` command to install it. 
```
yum -y install ntp
```
ntpd uses the client mode by default.

### Configuring NTP
1. Run the following command to open the configuration file of the NTP service.
```
vi /etc/ntp.conf
```
2. Press **i** to switch to the editing mode and locate the `server` configurations. Change the value of `server` to the NTP clock source server you want to use (such as `time1.tencentyun.com`) and delete unwanted values, as shown below:
![Server configuration](https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)
3. Press **Esc** and enter **:wq** to save and close the file.

### Launching ntpd

Run the following command to restart the ntpd service.
```
systemctl restart ntpd.service
```

### Checking the status of ntpd

Run the following commands to check the status of ntpd as needed. 
- Run the following command to check whether the NTP is normally listening on the service port UDP 123.
```
netstat -nupl
```
If the following result is returned, the listening is normal.
![netstat -nupl](https://main.qcloudimg.com/raw/d7da764d05135959154920b81fa9f1e4.png)
- Run the following command to check whether the ntpd status is normal.
```
service ntpd status
```
If the following result is returned, the ntpd status is normal.
![ntpd status](https://main.qcloudimg.com/raw/321e56d0f7797f382d9f6903c0315f96.png)
- Run the following command to get more detailed NTP service information.
```
ntpq -p
```
The following result will be returned:
![](https://main.qcloudimg.com/raw/ca9ef4caf98b49ed2c9110198a66e7c3.png)
 - **remote**: the name of the NTP server that responds to this request.
 - **refid**: the NTP server one stratum above to which the NTP server on this stratum is synchronized.
 - **st**: the stratum of the remote server. The stratum of a server can be set to 1 through 16 from high to low. In order to relieve the load and network congestion, you should avoid connecting directly to a stratum 1 server.
 - **when**: the number of seconds that have elapsed since the last successful request.
 - **poll**: the synchronization interval (in seconds) between local and remote servers. At the beginning, the `poll` value will be smaller, which indicates a higher synchronization frequency, so that the time can be adjusted to the correct time range as soon as possible. Later, the `poll` value will gradually increase, and the synchronization frequency will decrease accordingly.
 - **reach**: an octal value used to test whether the server can be connected. Its value increases every time the server is successfully connected.
 - **delay**: the round trip time of sending the synchronization request from the local machine to the NTP server.
 - **offset**: the time difference in milliseconds (ms) between the host and the time source through NTP. The closer the offset is to 0, the closer the times of the host and the NTP server are.
 - **jitter**: a value used for statistics that records the distribution of offsets over a particular number of consecutive connections. The smaller its absolute value is, the more accurate the host time is.

### Setting the automatic launch of ntpd at startup

1. Run the following command to automatically launch ntpd at startup.
```
systemctl enable ntpd.service
```
2. Run the following command to check whether chrony is set to launch at startup.
```
systemctl is-enabled chronyd.service
```
If chrony is set to launch at startup, run the following command to remove chrony from the auto-start list.
chrony is not compatible with ntpd, which may lead to ntpd start failure.
```
systemctl disable chronyd.service
```

### Enhancing ntpd security

Run the following commands sequentially to enhance the security of the `/etc/ntp.conf` configuration file.
```
interface ignore wildcard
```
```
interface listen eth0
```
