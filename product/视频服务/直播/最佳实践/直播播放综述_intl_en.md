## LVB Playback Protocol
LVB currently supports the RTMP protocol for push and RTMP, HTTP-FLV, and HLS protocols for playback. We recommend that you use the HTTP-FLV and HLS protocols. 
- HTTP-FLV has better support for mobile apps and PC applications and lower latency and lag.
- HLS supports all versions of Apple browsers (an HLS playback address can be used to play back a stream directly in Safari, WeChat, and QQ). In addition, HLS can be used for playback sharing in WeChat and QQ.

## How to Get a Playback Address
A Tencent Cloud playback address is mainly composed of playback prefix, playback domain name (domain), application name (AppName), stream name (StreamName), playback protocol suffix, authentication parameter, and other custom parameters.
For example:
```
rtmp://domain/AppName/StreamName?txSecret=xxxxxxxx&txTime=xxxxxx
http://domain/AppName/StreamName.m3u8?txSecret=xxxxxxxx&txTime=xxxxxx
http://domain/AppName/StreamName.flv?txSecret=xxxxxxxx&txTime=xxxxxx
https://domain/AppName/StreamName.m3u8?txSecret=xxxxxxxx&txTime=xxxxxx
https://domain/AppName/StreamName.flv?txSecret=xxxxxxxx&txTime=xxxxxx
```
- **Playback prefix **
 - RTMP playback protocol: **rtmp://**
 - HTTP-FLV playback protocol: **http://** or **https://**
 - HLS playback protocol: **http://** or **https://**
 
- **Playback domain name**
 - If you do not have a domain name, you can go to [Domain Name Registration](https://dnspod.cloud.tencent.com/?from=qcloudProductDns) to apply for one and then add it in [Domain Name Management](https://console.cloud.tencent.com/live/domainmanage).
 - If you already have a domain name, you can apply for [ICP filing](https://cloud.tencent.com/product/ba) for it and then add it in [Domain Name Management](https://console.cloud.tencent.com/live/domainmanage).
 - For the domain name CNAME record, see [CNAME Configuration](https://cloud.tencent.com/document/product/267/19908).
 
- **Application name (AppName)**
Application name refers to the storage path of a live streaming media file. By default, LVB assigns the path **live**.

- **<span id="streamname">Stream name (StreamName)</span>**
Stream name (StreamName) is the unique identifier of a live stream.

- **Authentication parameter and other custom parameters**
Authentication parameter: **txSecret=xxxxxxxx&txTime=xxxxxx**

## Using Playback Transcoding
In consideration of different network factors and to meet your needs for different resolutions at different bitrates, you can set transcoding templates with different bitrates and resolutions in [Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode) (for more information on transcoding, see [Best Practices - LVB Encapsulating and Transcoding](https://cloud.tencent.com/document/product/267/32736)).
 ### <span id="multirate">Original, HD, and SD</span>
In a real playback scenario, three bitrates are generally used: original, HD, and SD.
 - For an original stream, the push bitrate is the same as the original resolution.
 - For an HD stream, bitrate of 2000 Kbps and resolution of 1080p are recommended.
 - For an SD stream, bitrate of 1000 Kbps and resolution of 720p are recommended.

## Using Time Shifting for Replay
If you want to replay highlights in a certain period of time, you can use the time shifting feature which only supports the HLS protocol. For more information on time shifting and how to activate it, see [Best Practices - LVB Time Shifting](https://cloud.tencent.com/document/product/267/32742).
## Playback with HTTPS
If your playback domain name needs to support HTTPS, you should prepare a valid certificate and a valid private key, go to [Domain Name Management](https://console.cloud.tencent.com/live/domainmanage), and select **Playback Domain Name Management** > **Advanced Configuration** > **HTTPS Configuration** to add a configuration. After the configuration is successfully added, it will take effect in 2 hours, and then, your stream can be played back with the HTTPS protocol.

## Using a Global Cache Node for Playback
LVB boasts CDN nodes across Mainland China and around the world with wide coverage and high stability. If your end users are located in Hong Kong, Macao, Taiwan, or foreign countries, you can select **Global Acceleration** or **Outside Mainland China** for the acceleration region when configuring a domain name in [Domain Name Management](https://console.cloud.tencent.com/live/domainmanage) to enjoy coverage by global nodes.
>! The global acceleration of LVB supports only HTTP-FLV and HLS protocols.
## Hotlink Protection for Playback
In order to prevent illegal users from stealing your playback URL for use elsewhere that may cause traffic losses, it is strongly recommended that you enable hotlink protection for your playback address to avoid potential losses caused by hotlinking. A hotlink protection-enabled playback URL in LVB is mainly controlled by four parameters: txTime, key (hash key), txSecret, and validity period.

### Parameters
-  txTime
The effective time of the playback URL in hexadecimal UNIX time. If the current value of txTime is greater than the current request time, the stream can be played back normally; otherwise, the playback will be rejected by the backend.
- key
The key is used as the key for the MD5 calculation and can be customized. You can set a master key and a slave key, so that if your master is accidentally leaked, you can use the slave key to splice the playback URL and change the value of the master key.
- txSecret
It is the encryption parameter in the playback URL. Its value is obtained by performing MD5 encryption on the string spliced by key, StreamName, and txTime.
> txSecret = MD5(key+StreamName+txTime)
- Validity period
The validity period must be set to greater than 0. If txTime is set to the current time and the validity period is 300 seconds, then the playback URL expiration time is the current time + 300 seconds.

### Hotlink Protection URL Calculation
The calculation of a hotlink protection URL requires three parameters: key (a random string), stream name (StreamName), and txTime (in hexadecimal format).
Suppose that the key you set is **somestring**, the stream name (StreamName) is **test**, the txTime is **5c2acacc** (2019-01-01 10:05:00), the HD bitrate is **900 Kbps**, and the transcoding template name is **900**.
Original stream playback address:
```
txSecret = MD5(somestringtest5c2acacc) = b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.flv?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.m3u8?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
```
HD stream playback address:
```
txSecret = MD5(somestringtest_9005c2acacc) = 4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.flv?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.m3u8?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
```

### Enabling Hotlink Protection
Go to the [Domain Management](https://console.cloud.tencent.com/live/domainmanage) page and enter **Playback Domain Name Management** > **Access Control** > **Edit**.


>!
>- HTTP-FLV: The URL of the current playback will be able to continue playing back the stream after txTime expires but will be rejected when it requests a playback again.
>- HLS: As HLS uses a short link, it will continuously request .m3u8 files to get the latest ts segment. Assuming that you set the value of txTime to the current time + 10 minutes, the HLS playback URL request will be rejected after 10 minutes. To solve this problem, you can dynamically update the HLS request address on the server or set the expiration time of the HLS playback address to be longer.


## How to Play back
### Mobile Playback
If you need to integrate the LVB functionality into your mobile app, you can use the LVB SDK, which enables your app to play back live streams in RTMP, HTTP-FLV, and HLS formats. For more information, see [MLVB](https://cloud.tencent.com/product/mlvb).
### Web Playback
If you need to play live streams in PC or mobile browsers, you can choose Tencent Cloud Player+, which, based on Tencent Cloud's powerful backend functionality and AI technology, provides excellent playback capabilities for live broadcasting and video on-demand. Deeply integrated with the Tencent Cloud LVB and VOD services, Player+ features smooth and stable playback performance, advertising placement, and data monitoring. For more information, see [TCPlayerLite](https://cloud.tencent.com/document/product/881/20207).
>! Currently, most mobile browsers on the market do not support HTTP-FLV playback. Therefore, for web-based playback, you are recommended to select the HTTP-FLV playback protocol for PC browsers and HLS for mobile browsers.
## Best Practices for Playback
You can use tools such as VLC, FFmepg, and [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/player/demo/player.html) to play back a live stream for testing.
![](https://main.qcloudimg.com/raw/d286ff2f2a339b8c48ef73e9f0feb409.png)



