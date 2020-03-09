## Introduction

The Network Time Protocol daemon (ntpd) is a daemon of the Linux operating system. It is a complete implementation of NTP and is used to correct the time difference between the local system and the clock source server. Unlike NTPDate which updates time periodically, ntpd corrects time continuously without time gaps. This document uses CentOS7.5 as an example to describe how to install and use ntpd.

## Notes

- Some operating systems use chrony as the default NTP service. Please make sure that ntpd is running and is configured to start automatically on boot. 
 - Use `systemctl is-active ntpd.service` command to see if ntpd is running.
 - Use `systemctl is-enabled ntpd.service` command to see if ntpd is configured to start automatically on boot.
- The communication port of the NTP service is UDP 123. Please make sure that you have opened the port to the Internet before configuring the NTP service.
If the port is not open, please refer to [Adding Security Group Policies](https://intl.cloud.tencent.com/document/product/213/34272) to open it to the Internet.

## Directions
### Installing ntpd

Execute the following command to check if ntpd has been installed.
```
rpm -qa | grep ntp
```
 - If the returned result is similar to the following, it means that ntpd has been installed.
![Checking if ntpd has been installed](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
 - If ntpd has not been installed, please run `yum install ntp` to install it. 
```
yum -y install ntp
```
ntpd uses the client mode by default.

### Configuring NTP
1. Execute the following command to open the configuration file of the NTP service.
```
vi /etc/ntp.conf
```
2. Click **i** to enter the edit mode, find the configuration for server, change the server to the NTP clock source server you want to use, and delete the NTP clock source servers you do not need for the time being. See the figure below:
![Server Configuration](https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)
3. Press **Esc**, enter **:wq**, save the file, and return.

### Launching ntpd

Execute the following command to restart the ntpd service.
```
systemctl restart ntpd.service
```

### Checking the status of ntpd

Execute the following commands to check the status of ntpd according to your needs. 
- Execute the following command to check whether the NTP service port, the UDP 123 port, is being listened normally.
```
netstat -nupl
```
If a result similar to the following is returned, it indicates that the listening is normal.
![netstat -nupl](https://main.qcloudimg.com/raw/d7da764d05135959154920b81fa9f1e4.png)
- Execute the following command to check whether the ntpd status is normal.
```
service ntpd status
```
If a result similar to the following is returned, it indicates that the ntpd status is normal.
![ntpd status](https://main.qcloudimg.com/raw/321e56d0f7797f382d9f6903c0315f96.png)
- Execute the following command to check whether NTP has been started normally and configured to the correct NTP clock source server.
```
ntpstat
```
The IP address of the current NTP clock source server is returned. This IP address should be the IP address of the NTP clock source server configured above. See the figure below:
![](https://main.qcloudimg.com/raw/a99f5da438bafb1d148e9b033f48afad.png)
You can also get the IP address corresponding to the domain name by executing the `nslookup domain name` command.
- Execute the following command to get more detailed NTP service information.
```
ntpq -p
```
A result similar to the following will be returned:
![](https://main.qcloudimg.com/raw/ca9ef4caf98b49ed2c9110198a66e7c3.png)
 - **remote**: the name of the NTP server that responds to this request.
 - **refid**: the NTP server one stratum above to which the NTP server on this stratum is synchronized.
 - **st**: the stratum of the remote server. The stratum of a server can be set to 1 to 16 from the top to the bottom. In order to relieve the load and network congestion, in principle, you should avoid connecting directly to a stratum 1 server.
 - **when**: how many seconds have elapsed since the last successful request.
 - **poll**: the synchronization interval (in seconds). At the beginning, the poll value will be smaller, which means higher frequency of synchronization with the server, so that the time can be adjusted to the correct time range as soon as possible. Later, the poll value will gradually increase, and the synchronization frequency will be lower accordingly.
 - **reach**: an octal value used to test whether the server can be connected. Its value increases every time when the server is successfully connected.
 > **delay**: the round trip time of sending the synchronization request from the local machine to the NTP server.
 > **offset**: the difference in milliseconds (ms) between the host time synchronized through NTP and the time of the time source. The closer the offset is to 0, the closer the time of the host and the NTP server is.
 - **jitter**: a value used for statistics which records the distribution of offsets over a particular number of consecutive connections. The smaller its absolute value, the more accurate the host time.

### Setting the automatic launch of ntpd on startup

1. Execute the following command to set the automatic launch of ntpd at startup.
```
systemctl enable ntpd.service
```
2. Execute the following command to see if chrony is set to launch at startup.
```
systemctl is-enabled chronyd.service
```
If chrony is set to launch at startup, excute the following command to remove chrony from the list of software that runs at startup.
chrony is not compatible with ntpd, which may lead to ntpd start failure.
```
systemctl disable chronyd.service
```


