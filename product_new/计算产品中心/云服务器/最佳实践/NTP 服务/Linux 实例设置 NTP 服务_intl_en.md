## Scenario

The Network Time Protocol daemon (ntpd) is a daemon of the Linux operating system. It is a complete implementation of NTP and is used to correct the time difference between the local system and the clock source server. Unlike ntpdate which updates time periodically, ntpd corrects time continuously without time gaps. This document describes how to install and use ntpd.

## Notes

* Some operating systems use chrony as the default NTP service. Use `systemctl is-active ntpd.service` to check if ntpd is running; use `systemctl is-enabled ntpd.service` to check if ntpd automatically run at startup. For details, please refer to the section on how to set the automatic launch of ntpd on startup.
* The communication port of the NTP service is UDP 123. Make sure you have opened the port before setting the NTP service. You can check if the port is open on the instance with `netstat -nupl`. For information on how to open the port, please see [Operation Guide on Security Groups](https://intl.cloud.tencent.com/document/product/213/18197).

> **Note:**
> The following takes operations on a CentOS 7.5 64bit instance as an example.

## Directions
### Installation

-  Use the following command to determine if ntpd has been installed:
```
rpm -qa | grep ntp
```
![Determine if ntpd has been installed](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
- If it has not been installed, use `yum install ntp` to install it. If you do not make any configuration, ntpd will work in client mode by default.
```
yum -y install ntp
```

### Configuration
- Open and edit NTP service configuration file with vim.
```
vi /etc/ntp.conf
```
- Find the configuration for server, change the server to the NTP clock source server you want to use, and delete the NTP clock source servers you do not need for the time being.
![Server configuration](	https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)

### Start
- Start the NTP service with `service ntpd start`. If NTP has already been started, restart it with `service ntpd restart`.
```
service ntpd start
```
![Start ntp](https://main.qcloudimg.com/raw/470afd5f311b5ba3ad321ed12d974c88.png)

### Status Check
-  Check whether UDP 123, the NTP service port, is monitored normally with `netstat`.
```
netstat -nupl
```
![netstat -nupl](https://main.qcloudimg.com/raw/e7eb5ed8529fdc1366210ef76cf09bd3.png)
- Check whether the ntpd status is normal with the following command:
```
service ntpd status
```
![ntpd status](	https://main.qcloudimg.com/raw/8af337c167f295938f5edbc005032809.png)
- Use `ntpstat` to see if ntpd is properly started and configured to the correct NTP clock source server. This command outputs the IP address of the current NTP clock source server. This IP address should be the IP address of the NTP clock source server you configured above (you can use the `nslookup domain name` to obtain the IP address corresponding to the domain name).
![ntpstat](https://main.qcloudimg.com/raw/83d49c87c485989123acbb9a30d92d0c.png)

- You can get more detailed information on the NTP service with `ntpq -p`.
![ntpq](https://main.qcloudimg.com/raw/87df34053b422b0c03e038e4e5a9fde0.png)
> remote: the name of the NTP server that responds to this request.
> refid: the NTP server one stratum above to which the NTP server on this stratum is synchronized.
> st: the stratum of the remote server. NTP uses a hierarchical structure with a server at the top, multiple relay servers in the midde, and the client at the bottom. The stratum of a server can be set to 1 to 16 from the top to the bottom. In order to relieve the load and network congestion, in principle, you should avoid connecting directly to a stratum 1 server.
> when: how many seconds has elapsed since the last successful request.
> poll: the synchronization interval (in seconds). At the beginning, the poll value will be smaller, which means higher frequency of synchronization with the server, so that the time can adjusted to the correct time range as soon as possible. Later, the poll value will gradually increase, and the synchronization frequency will be lower accordingly.
> reach: an octal value used to test whether the server can be connected. Its value increases every time when the server is successfully connected.
> delay: the round trip time of sending the synchronization request from the local machine to the NTP server.
> offset: the difference in milliseconds (ms) between the host time synchronized through NTP and the time of the time source. The closer the offset is to 0, the closer the time of the host and the NTP server is.
> jitter: a value used for statistics which records the distribution of offsets over a particular number of consecutive connections. Simply put, the smaller its absolute value is, the more accurate the host time is.

### Setting the automatic launch of ntpd on startup

- Set the automatic launch of ntpd on startup with the command below.
```
systemctl enable ntpd.service
```

- Use the command below to see if chrony is set to launch at startup.
```
systemctl is-enabled chronyd.service
```

- chrony is not compatible with ntpd, which may lead to ntpd start failure. Use the following command to remove chrony from the list of software that runs at startup.
```
systemctl disable chronyd.service
```


