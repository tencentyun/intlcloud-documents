The Network Time Protocol (NTP) is intended to synchronize the clocks on all the computers in a network to Coordinated Universal Time (UTC). Its design takes various network latency into account. When the clocks are synchronized through the public network, the error is within 10 ms; when the clocks are synchronized through the local network, the error can be as small as 1 ms.

Tencent Cloud provides an intranet NTP server for Tencent Cloud intranet devices. For non-Tencent cloud devices, you can use the public network NTP server provided by Tencent Cloud.

### Intranet NTP Server

```
ntpupdate.tencentyun.com
```

### Public Network NTP Server

```
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```



