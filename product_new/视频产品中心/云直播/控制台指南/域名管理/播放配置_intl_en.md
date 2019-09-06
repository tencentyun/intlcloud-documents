## Scenario
After the push address of a push domain name is generated, if you want to view the live streaming content pushed to the push address, you need to get the playback address generated for the playback domain name in the playback configuration and add the StreamName to it to associate it with the push address. In this way, you can get the playback address where you can view the live stream.

## Prerequisites
 You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Steps
1. Select **Manage Domain** in the left sidebar, click the playback domain name to be configured or click **Manage** in the operation column to enter the domain name management page.
 ![](https://main.qcloudimg.com/raw/4c5032073fac98ce308d353c8e218cd4.png)

2. In the **Playback Configuration** tab, you can view three types of playback addresses under the domain name, i.e., RTMP, FLV, and HLS. By replacing the StreamName (stream name) in the playback address with a user-defined stream ID, you can associate the playback address with the push address. After they are associated, you can go to the playback address to play back the live stream. For the generation of push address, see [Push Configuration](https://intl.cloud.tencent.com/document/product/267/31059).
 ![](https://main.qcloudimg.com/raw/15afd6e0a641e14eca632e0df7cdbecb.png)

3. The playback address is generated according to the following rules:
        RTMP format: rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
        FLV format: http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
        M3U8 format: http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)

>- domain: your domain name which has been filed on ICP record.
>- AppName: application name which is "live" by default. If you want to customize it, you need to submit a ticket for configuration.
>- StreamName: user-defined stream name used to label the live stream.
>- txSecret: authentication string generated after playback authentication is enabled.
>- txTime: Timestamp set for the playback address which represents the validity period of the address in the console.

4. If a transcoding template is configured for the playback domain name and you need to play back the transcoded live stream, you can get the transcoded playback address by adding `_transcoding template name` after the StreamName in the original playback address.
For example, if the original playback address is `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)` and the name of the transcoding template associated with the domain name is `hd`, the transcoded playback address should be `http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.

5. If you use H.265 for push and need to play back H.265 live stream, you need to add `_265` at the end of the playback address; otherwise, transcoding fees will be incurred when H.264 live stream is played back.
For example, if the original playback address is `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)` and H.265 is used for push, the playback address of the original stream should be `http://domain/AppName/StreamName_265.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.
