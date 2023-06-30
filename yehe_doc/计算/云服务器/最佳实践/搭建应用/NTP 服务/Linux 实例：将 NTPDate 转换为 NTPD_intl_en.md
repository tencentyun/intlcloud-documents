## Overview

The ntpdate is a breakpoint update for the time synchronization of your new instances. The ntpd is a stepwise daemon for the time synchronization of your running instances. This document uses the CentOS 7.5 operating system as an example to introduce how to transition from ntpdate to ntpd on CVMs.

## Prerequisites
The NTP service communicates on the port UDP 123. Please make sure that you have opened the port to the Internet before transitioning to the NTP service.
If the port has not been opened, please refer to [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272) to open it to the Internet.

## Directions
You can choose to transition from ntpdate to ntpd [manually](#manual) or [automatically](#automatic).
<span id="manual"></span>
### Transitioning from ntpdate to ntpd manually
#### Shutting down ntpdate
1. Run the following command to export the `crontab` configuration and filter ntpdate.
```
crontab -l |grep -v ntpupdate > /tmp/cronfile
```
2. Run the following command to update the ntpdate configuration.
```
crontab /tmp/cronfile
```
3. Run the following command to modify the `rc.local` file.
```
vim /etc/rc.local
```
4. Press **i** to switch to the edit mode and delete the `ntpupdate` configuration line.
5. Press **Esc** and enter **:wq** to save and close the file.

#### Configuring ntpd
1. Run the following command to open the configuration file of the NTP service.
```
vi /etc/ntp.conf
```
2. Press **i** to switch to the edit mode and locate the `server` configurations. Change the value of `server` to the NTP clock source server you want to use (such as `time1.tencentyun.com`) and delete unwanted values, as shown below:
![Server configuration](https://main.qcloudimg.com/raw/643dc5bbd2a42307ec10b5d38f756dda.png)
3. Press **Esc** and enter **:wq** to save and close the file.

<span id="automatic"></span>
### Transitioning from ntpdate to ntpd automatically
1. Download the `ntpd_enable.sh` script.
```
wget https://image-10023284.cos.ap-shanghai.myqcloud.com/ntpd_enable.sh
```
2. Run the following command to transition from ntpdate to ntpd using the `ntpd_enable.sh` script.
```
sh ntpd_enable.sh
```

## Relevant Operations
### Checking the status of ntpd
Run the following commands to check the status of ntpd as needed.
- Run the following command to check whether the NTP is listening normally on the service port UDP 123.
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
 - **\***: the NTP server in use currently.
 - **remote**: the name of the NTP server that responds to this request.
 - **refid**: the NTP server one stratum above to which the NTP server on this stratum is synchronized.
 - **st**: the stratum of the remote server. The stratum of a server can be set to 1 through 16 from high to low. In order to relieve the load and network congestion, you should avoid connecting directly to a stratum 1 server.
 - **when**: the number of seconds that have elapsed since the last successful request.
 - **poll**: the synchronization interval (in seconds) between the local and remote servers. At the beginning, the `poll` value will be smaller, which indicates a higher synchronization frequency, so that the time can be adjusted to the correct time range as soon as possible. Later, the `poll` value will gradually increase, and the synchronization frequency will decrease accordingly.
 - **reach**: an octal value used to test whether the server can be connected. Its value increases every time the server is successfully connected.
 - **delay**: the round trip time of sending the synchronization request from the local machine to the NTP server.
 - **offset**: the time difference in milliseconds (ms) between the host and the time source through NTP. The closer the offset is to 0, the closer the times of the host and the NTP server are.
 - **jitter**: a value used for statistics that records the distribution of offsets over a particular number of consecutive connections. The smaller its absolute value is, the more accurate the host time is.
