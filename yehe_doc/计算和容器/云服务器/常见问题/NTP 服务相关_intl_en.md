### How do I adjust the synchronization interval of the configured NTP service?
After [configuring the NTP service on a Linux instance](https://intl.cloud.tencent.com/document/product/213/32381), you can restart ntpd to reset the synchronization interval. To manually set the ntpd synchronization interval, perform the following steps:
1. Run the following command to modify the NTP configuration file.
```
vi /etc/ntp.conf
```
2. Press **i** to enter the edit mode and configure as follows:
  1. Add the pound sign (`#`) at the beginning of `server time1.tencentyun.com iburst`, if any, to comment it out.
  2. Add the following configurations. Where, `minpoll 4` means the minimum interval is 2<sup>4</sup>, and `maxpoll 5` means the maximum interval is 2<sup>5</sup>.
```
server time1.tencentyun.com minpoll 4 maxpoll 5
```
The result should be as follows. Enter **:wq** to save changes and close the file.
![](https://main.qcloudimg.com/raw/02d6457d29b4c573605e3c79c5ccfc9f.png)
3. Restart ntpd and run `ntpd -p`. The `poll` value you will see is 16 (namely, 2<sup>4</sup>), as shown in the following figure:
![](https://main.qcloudimg.com/raw/9fa0c72751de74d3b6e72cc1ca831952.png)

### What is the time source of Tencent Cloud’s ntpd servers?
NTP servers usually use the BeiDou satellite clock.
 
### What should I do when the NTP configuration reports the `localhost.localdomain timeout` error?
The error is as shown in the following figure.
![](https://main.qcloudimg.com/raw/1b3158135475e6cfbee28d2373685616.png)
Check and confirm whether you ran `POSTROUTING`. If yes, change the source IP in the `ntp.conf` configuration file to eth0’s IP address.

### Can off-cloud servers share a NTP with Tencent Cloud CVMs? What is the NTP synchronization address?
Tencent Cloud provides private NTP servers for Tencent Cloud resources. For other devices, you can use the public NTP servers provided by Tencent Cloud for synchronization.
- Private NTP servers at:
```
time1.tencentyun.com
time2.tencentyun.com
time3.tencentyun.com
time4.tencentyun.com
time5.tencentyun.com
```
- Public NTP servers at:
```
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

### Why is the time of a CVM instance created from a custom image incorrect?
Please check whether the NTP service is enabled. To use the NTP synchronization feature later, see the following document according to the operating system to set NTP. Then re-create the custom image.
 - [Set the NTP service on a Linux instance](https://intl.cloud.tencent.com/document/product/213/32381)
 - [Set the NTP service on a Windows instance](https://intl.cloud.tencent.com/document/product/213/32380)

### Will the NTP synchronization be affected if a CVM cannot ping the NTP server?
No. As long as you can access your NTP, the synchronization works. 

### Why is the ntp.conf content of a CVM created from a custom image restored?
It may be caused by the Cloud-Init initialization. Please delete the NTP-related configurations in `/etc/cloud/cloud.cfg` before creating a custom image. For more information, see [Cloud-Init & Cloudbase-Init](https://intl.cloud.tencent.com/document/product/213/19670).

### What impact will a modified private network DNS have?
All services involving Tencent Cloud private domain name resolution will be affected. For example,
- The YUM repository uses the Tencent Cloud private domain name. You need to modify the YUM repository after changing DNS.
- The reporting of monitoring data uses the private domain name and will be affected.
- The NTP feature depends on the private domain name to sync server time, and will be affected.

### Why does the local time of a Windows instance reset from the configured EST to Beijing time after restart?
Check that the windowstime service is enabled on the instance. You may need to manually enable it to auto sync the instance’s system time. We recommend enabling the service autostart.

### Why cannot I use the `ntpq -np` command to view the synchronization time?
The error is as shown in the following figure.
![](https://main.qcloudimg.com/raw/88972a2aeda155c10000e8576d16bbe9.png)
Please check whether no IP or incorrect IP is configured for `listen` in the `/etc/ntp.conf` configuration file. Change to the primary private IP of the instance and restart ntpd.

### How do I fix the error occurred when using the public NTP servers to sync time?
The `no server suitable for synchronization found` error is as shown in the following figure.
![](https://main.qcloudimg.com/raw/1909910bc2a86a5f93e09f4601654327.png)
It may be caused by the NTP protection policy in response to the DDoS attacks to the public IP address of the instance. This policy blocks all public inbound traffic at the Tencent Cloud’s source point 123 and causes synchronization exception. We recommend trying to use the private NTP servers to sync time.
