
### How much traffic does GME voice chat consume?
The bitrate is 30 Kbps for the fluency sound quality, and 64 Kbps for the standard and high sound quality. The traffic is related to the bitrate and also the number of room members who communicate through voice chat. The formula is: bitrate x the number of the members / 8 = bytes.

### The error code 7004 indicating a network error is returned when I am entering a room. How to fix it?
Please check the following for troubleshooting:
1. Whether the parameters of the `EnterRoom` API are valid, such as `AppID`, `UIN`, and `AuthBuffer`. For more information, please see [relevant API documentation](https://intl.cloud.tencent.com/zh/document/product/607/18522).
2. Whether your testing devices are in the private network or public network. If they are in the private network, please troubleshoot as instructed in [How to Deal with the Restrictions of Corporate Firewall](https://intl.cloud.tencent.com/document/product/607/35232).
3. Other network problems below:

### How do I troubleshoot network problems?

- **Network diagnosis**
	- [Click here to check the status of the domain name `tcloud.tim.qq.com`.](https://ping.huatuo.qq.com/tcloud.tim.qq.com)
	- [Click here to check the status of the domain name `gmeconf.qcloud.com`.](https://ping.huatuo.qq.com/gmeconf.qcloud.com)
	- [Click here to check the status of the domain name `yun.tim.qq.com`.](https://ping.huatuo.qq.com/yun.tim.qq.com )

Please use the device with network issues to open the three URLs above in a browser, and wait for the results (the checks take about 5 to 10 seconds to finish). Click **copy result URL and share** and then [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
![](https://main.qcloudimg.com/raw/0b540f4bf6222c6b9548b148496a15bb.png)

- **SSO diagnosis**
Please use the device with network issues to open [tcloud.tim.qq.com](https://tcloud.tim.qq.com) for domain name status checks. Take a screenshot of or copy the results and then [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
The sample code is as follows:
```
{"ActionStatus":"FAIL","ErrorCode":60002,"ErrorInfo":"HTTP parse Error"}
```
