## Operation Scenarios
The push configuration can be used to generate a push address under the corresponding push domain name. By pushing a live stream to the push address, the live stream can be transmitted (uploaded) to LVB.

## Prerequisites
- You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).
- You have added a [push domain name](https://cloud.tencent.com/document/product/267/20381).

## Push Address Generator
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and select the push domain name to be configured or click **Manage** to enter its details page.
![](https://main.qcloudimg.com/raw/d28864eb5bcc9c36ecc51dbfa0a8f61d.png)
2. Select **Push Configuration** > **Push Address Generator** and configure as follows:
	1. Select an expiration time, such as `2019-10-31 23:59:59`.
	2. Enter a custom `StreamName`, such as `liveteststream`.
	3. Click **Generate Push Address**.
![](https://main.qcloudimg.com/raw/bd1d0e5ed9bbc71e0751b948b18d86ab.png)
>Click **Generate Push Address** and the system will generate an RTMP push address with `StreamName`. You can test, disable, or delete it in [stream management](https://intl.cloud.tencent.com/document/product/267/31068) after implementing [LVB push](https://intl.cloud.tencent.com/document/product/267/31558) according to your business scenario. The RTMP push address is in the format of `rtmp://domain/live/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`, where:
>- `domain`: LVB push domain name.
>- `AppName`: application name, which is `live` by default. If you want to customize it, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for configuration.
>- `StreamName`: user-defined stream name which is used to identify a live stream.
>- `txSecret`: authentication string generated after push authentication is enabled.
>- `txTime`: timestamp set for a push address which represents the expiration time of the address in the console.

> 
>- The generated push address is valid before the set expiration time. You can generate a new address after the old one expires.
>- After the push address is generated, LVB push can be started. However, to view live broadcasting, a playback address is required. For more information, please see [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058).

## Push Address Sample Code
Sample code for generating push addresses in PHP and Java is provided for your reference, which can be viewed in the following way:
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and select a push domain name or click **Manage** on the right to enter its details page.
2. Select the **Push Configuration** tab and scroll down to find **Push Address Sample Code**.
3. Click the tag button above the code to switch to the desired programming language as shown below:
![](https://main.qcloudimg.com/raw/bdea9b0d03852a7483cf5a9d6eb00a87.png)


