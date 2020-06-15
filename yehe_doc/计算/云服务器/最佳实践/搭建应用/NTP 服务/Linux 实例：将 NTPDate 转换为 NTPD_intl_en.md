## Overview

NTPDate is a breakpoint update for time synchronization of your new instances. NTPD is a stepwise daemon for time synchronization of your running instances. This document uses the CentOS 7.5 operating system as an example and introduces how to transition from NTPDate to NTPD on CVMs.

## Prerequisites
The NTP service communicates on the port UDP 123. Please make sure that you have opened the port to the Internet before transitioning to the NTP service.
If the port is not open, please refer to [Adding Security Group Policies](https://intl.cloud.tencent.com/document/product/213/34272) to open it to the Internet.

## Directions

### Transitioning from NTPDate to NTPD manually
#### Shutting down NTPDate
1. Run the following command to export the `crontab` configuration, and filter NTPDate.
```
crontab -l |grep -v ntpupdate > /tmp/cronfile
```
2. Run the following command to update the NTPDate configuration.
```
crontab /tmp/cronfile
```
3. Run the following command to modify the `rc.local` file.
```
vim rc.local
```
4. Press **i** to enter the edit mode and delete the `ntpupdate` configuration line.
5. Press **Esc** and enter **:wq** to save and close the file.

#### Configuring NTPD
1. Run the following command to open the configuration file of the NTP service.
```
vi /etc/ntp.conf
```
2. Press **i** to enter the edit mode and locate the `server` configurations. Change the value of `server` to the NTP clock source server you want to use (such as `time1.tencentyun.com`), and delete unwanted values, as shown below：
![Server configuration](https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)
3. Press **Esc** and enter **:wq** to save and close the file.


### Transitioning from NTPDate to NTPD automatically
1. Download the `ntpd_enable.sh` script.
```
wget https://image-10023284.cos.ap-shanghai.myqcloud.com/ntpd_enable.sh
```
2. Run the following command to transition from NTPDate to NTPD using the `ntpd_enable.sh` script.
```
sh ntpd_enable.sh
```



