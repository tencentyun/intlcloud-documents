## Operation Scenarios
Tencent Cloud provides a web push feature which can quickly generate push addresses and test push online.

## Prerequisites
- You have added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- Your device has a camera installed and its browser supports the Flash plugin to call the camera permission.

## Directions
1. Log in to the LVB Console, select **[Web Push](https://console.cloud.tencent.com/live/tools/webpush)**.
2. Perform the following settings on the web push page:
	- Select a push domain name.
	- Enter a custom `StreamName`, such as `test`.
	- Select an expiration time, such as `2020-04-13 23:59:59`.
	- Edit `AppName` which is the address path used to differentiate multiple applications under the same domain name and is `live` by default.
3. Click **Start Push** and grant the camera permission to start the push.
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)
4. If you have already added a playback domain name in **Domain Management**, you can view the generated corresponding playback address below, which consists of the following four parts:
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)
RTMP, FLV, and HLS protocols are supported. You can click the QR code after the address and scan it with the Lite Demo to view the address:
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
