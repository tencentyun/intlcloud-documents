## Operation Scenarios
After push is successful for a domain name, you can log in to the LVB Console, enter the `StreamName` of the push address in the playback address generator to generate a playback address for the corresponding live stream, and then use it to watch the stream.

## Prerequisites
 - You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).
 - You have added a **playback domain name**.

## Directions
1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **playback domain** to be configured or **Manage** to enter the domain management page.
2. Select **Playback Configuration** > **Playback Address Generator** and configure as follows:
	1. Select an expiration time, such as `2019-02-28 23:59:59`.
	2. Enter a custom `StreamName`, such as `liveteststream`. The `StreamName` of the playback address must be the same as that of the push address to play back the corresponding stream.
	3. Click **Generate Playback Address**.
![](https://main.qcloudimg.com/raw/6bea977acb754ec9c36422aef3189f39.png)
3. If playback authentication is not enabled for your playback domain name, you can view three types of playback addresses under the domain name in **Playback Configuration** > **Playback Address**, i.e., RTMP, FLV, and HLS. Replace the `StreamName` to associate with a push address, and then you can play back the live stream at the playback address.
![](https://main.qcloudimg.com/raw/8d8a9ee63dc12045da418c1539051eb6.png)

>For more information on LVB playback, please see [LVB Playback](https://intl.cloud.tencent.com/document/product/267/31559).




## Playback Address
### 1. Generation rules for playback address
```
RTMP format: rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
FLV format: http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
M3U8 format: http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- **domain**: your playback domain name which has obtained an ICP filing for service in Mainland China.
- **AppName**: LVB application name, which is `live` by default and customizable.
- **StreamName**: user-defined stream name which is used to identify a live stream.
- **txSecret**: authentication string generated after playback authentication is enabled.
- **txTime**: timestamp set for a playback address which represents the expiration time of the address in the console.

>
>- If you have enabled domain name authentication, the actual expiration time will be `txTime` + authentication expiration time.
>- For your convenience, the time set in the console is the actual expiration time. If you have enabled domain name authentication, `txTime` will be calculated according to the formula when the playback address is generated.

### 2. Transcoded playback address
If a transcoding template is configured for the playback domain name and you want to play back a transcoded live stream, you can get the transcoded playback address by adding `_transcoding template name` after the `StreamName` in the original playback address.

For example, if the original playback address is `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)` and the name of the transcoding template associated with the domain name is `hd`, then the transcoded playback address will be `http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`.

### 3. H.265 playback address
If H.265 is used for push and you want to play back the H.265 live stream, you need to add `_h265` after `StreamName` and generate a new playback address.
>
>- If `_h265` is not added, the H.264 live stream will be played back, which will incur transcoding fees.
>- After `_h265` is added after `StreamName`, a new playback address needs to be generated. You cannot add it directly to the existing playback address; otherwise, the playback address will not work.

For example, if the original playback address is `http://domain/AppName/StreamName1.flv?txSecret=Md5(key+StreamName1+hex(time))&txTime=hex(time)` and H.265 is used for push, then the playback address that needs to be generated with `StreamName1_h265` will be `http://domain/AppName/StreamName1_h265.flv?txSecret=Md5(key+StreamName1_h265+hex(time))&txTime=hex(time)`.
