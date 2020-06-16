<span id="que1"></span>
### Is there an upper limit on the number of online viewers?	
By default, LVB does not limit the number of online viewers for a live stream as long as the network and other conditions permit. However, if you have configured a bandwidth limit, new viewers cannot watch the live stream if there are so many existing viewers that the bandwidth limit is exceeded. In this case, the number of online viewers is limited.

<span id="que2"></span>
### How can I use live transcoding?
In consideration of different network factors and to meet your needs for different resolutions at different bitrates, you can set transcoding templates with different bitrates and resolutions in [Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode). For more information on transcoding, see [Best Practices - LVB Encapsulating and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).

 #### <span id="multirate">Original, HD, and SD</span>
In a real playback scenario, three bitrates are generally used: original, HD, and SD.
 - For an original stream, the push bitrate is the same as the original resolution.
 - For an HD stream, bitrate of 2,000 Kbps and resolution of 1080p are recommended.
 - For an SD stream, bitrate of 1,000 Kbps and resolution of 720p are recommended.

<span id="que3"></span>
### How can I use time shifting for replay?
If you want to replay highlights, you can use the time shifting feature which only supports the HLS protocol.

<span id="que4"></span>
### How can I use HTTPS for playback?
If your playback domain name needs to support HTTPS, you should prepare a valid certificate and a valid private key, go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), find the desired playback domain name, click **Manage**, and select **Advanced Configuration** > **HTTPS Configuration** to add a configuration. After the configuration is successfully added, it will take effect in 2 hours, and then, your stream can be played back with the HTTPS protocol.

<span id="que5"></span>
### How can I use a global cache node for playback?
LVB has CDN nodes across Mainland China and around the world with wide coverage and high stability. If your end users are located outside Mainland China, you can select **Global Acceleration** or **Hong Kong/Macao/Taiwan (China Region) and other regions** as the acceleration region when configuring a domain name in [Domain Management](https://console.cloud.tencent.com/live/domainmanage) to enjoy coverage by global nodes.
> The global acceleration of LVB supports only HTTP-FLV and HLS protocols.

<span id="que6"></span>
### How can I enable hotlink protection?
In order to prevent illegal users from stealing your playback URL for use elsewhere that may cause traffic losses, we strongly recommend enabling hotlink protection for your playback address to avoid potential losses caused by hotlinking. A hotlink protection-enabled playback URL in LVB is mainly controlled by four parameters: `txTime`, `key` (hash key), `txSecret`, and validity period.

| Hotlink Protection Parameter | Description | Remarks |
|---------|---------|---------|
| txTime | The effective time of the playback URL | It is in hexadecimal UNIX time.<br> If the current value of `txTime` is greater than the current request time, the stream can be played back normally; otherwise, the playback will be rejected by the backend.|
| key | The key for the MD5 calculation | It can be customized.<br> You can set a master key and a slave key, so that if your master is accidentally leaked, you can use the slave key to splice the playback URL and change the value of the master key.|
| txSecret | Encryption parameter in playback URL | The value of this parameter is obtained by performing MD5 encryption on the string spliced by `key`, `StreamName`, and `txTime`.<br>`txSecret = MD5(key+StreamName+txTime)`. |
| Validity period | The validity period of the push address | The validity period must be set to greater than 0.<br> If `txTime` is set to the current time and the validity period is 300 seconds, then the playback URL expiration time is the current time + 300 seconds.

#### Hotlink protection URL calculation
The calculation of a hotlink protection URL requires three parameters: `key` (a random string), `StreamName` (stream name), and `txTime` (in hexadecimal format).
Suppose that the `key` you set is **somestring**, the stream name (`StreamName`) is **test**, the `txTime` is **5c2acacc** (2019-01-01 10:05:00), the HD bitrate is **900 Kbps**, and the transcoding template name is **900**.
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

#### Enabling hotlink protection
1. Log in to the LVB Console and enter [Domain Management](https://console.cloud.tencent.com/live/domainmanage).
2. Select a playback domain name or click **Manage** to enter its details page.
3. Select **Access Control** and click **Edit**.
4. Enable **Playback Authentication** and click **Save**.

>
>- It takes **30 minutes** for the playback authentication configuration to take effect.
>- HTTP-FLV: the URL of the current playback will be able to continue playing back the stream after `txTime` expires but will be rejected when it requests a playback again.
>- HLS: as HLS uses a short link, it will continuously request .m3u8 files to get the latest ts segment. Assuming that you set the value of `txTime` to the current time + 10 minutes, the HLS playback URL request will be rejected after 10 minutes. To solve this problem, you can dynamically update the HLS request address on the server or set the expiration time of the HLS playback address to be longer.

<span id="que7"></span>
### What are the format requirements for the master key in the playback authentication configuration? Is there any limit on its validity period?
The master key in the authentication configuration can contain 256 bits of uppercase and lowercase letters and digits. A random mix of letters and digits is enough.
We recommend that you set its validity period to the duration of the live stream.


<span id="que8"></span>
### Can I create an LVB push address to use all the time? What is the maximum length of address validity period?
The main purpose of setting a validity period for the push address is to authenticate and protect the push address to prevent unauthorized push and business losses.
There is no limit on the validity period of a push address, which can be set according to your business needs. You can also splice addresses to generate a push address with a longer validity period. For more information about splicing rules, please see [How to Splice a Push URL](https://intl.cloud.tencent.com/document/product/267/32480).

> We do not recommend a very long validity period of the push address, which may cause LVB to report an error during the use and report a failed authentication.

<span id="que9"></span>
### Will the Tencent Cloud logo be displayed in the LVB video? 
No. 

<span id="que10"></span>
### How long is the LVB latency? 
LVB pushes a stream using the RTMP protocol and plays it using the FLV protocol. Generally, the latency is about 2 to 3 seconds. A long latency often indicates an error.

<span id="que11"></span>
### Can I set the maximum LVB bitrate?
 No. The maximum LVB bitrate is automatically set by the pusher, according to the upload speed of your network. The upper limit of bitrate (or maximum bitrate) depends on the upload speed of your network. If the maximum bitrate is too high, it will cause dropped frames and lag during a live stream. 

<span id="que12"></span>
### How do I delete an LVB room which is no longer used? 
LVB push and playback are currently associated with stream IDs, so you do not have to delete rooms. If you are using the IM service and want to delete IM rooms to avoid hitting its upper limit, please see [Disbanding Groups](https://intl.cloud.tencent.com/document/product/1047/34896).
If you are using the channel mode, you can call the `DeleteLVBChannel` API and input LVB channel IDs as parameters to delete the LVB channels (in batches).

> LVB has no longer provided updates or support for the channel mode.

<span id="que13"></span>
 ### What does the "enabling/disabling LVB push" API do? 
This API is used to forbid a stream during porn detection. For example, if a host is found to play pornographic or terroristic content, this stream can be interrupted or forbidden at any time.


<span id="que14"></span>
### How do I play a video in the background?
The background video playback feature should be provided by devices. You can develop this feature according to the actual business logic. As long as the live stream is not interrupted, in theory, you can play audio in the background.


