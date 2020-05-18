<span id="que1"></span>
### Is there a upper limit on the number of online viewers?	
By default, LVB does not limit the number of online viewers for a live stream as long as the network and other conditions permit. However, if you have configured a bandwidth limit, new viewers cannot watch the live stream if there are so many existing viewers that the bandwidth limit is exceeded. In this case, the number of online viewers is limited.

<span id="que2"></span>
### How can I use live transcoding?
In consideration of different network factors and to meet your needs for different resolutions at different bitrates, you can set transcoding templates with different bitrates and resolutions in [Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode). For more information on transcoding, please see [Best Practice - LVB Remuxing and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).

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
If your playback domain name needs to support HTTPS, you should prepare a valid certificate and a valid private key, go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), and select **Playback Domain Name Management** > **Advanced Configuration** > **HTTPS Configuration** to add a configuration. After the configuration is successfully added, it will take effect in 2 hours, and then, your stream can be played back with the HTTPS protocol.

<span id="que5"></span>
### How can I use a global cache node for playback?
LVB has CDN nodes across Mainland China and around the world with wide coverage and high stability. If your end users are located outside Mainland China, you can select **Global Acceleration** or **Hong Kong/Macao/Taiwan (China Region) and other regions** as the acceleration region when configuring a domain name in [Domain Management](https://console.cloud.tencent.com/live/domainmanage) to enjoy coverage by global nodes.
> The global acceleration of LVB supports only HTTP-FLV and HLS protocols.

<span id="que6"></span>
### How can I enable hotlink protection?
In order to prevent malicious users from stealing your playback URL for use elsewhere that may cause traffic losses, you are strongly recommended to enable hotlink protection for your playback address to avoid potential losses caused by hotlinking. A hotlink protection-enabled playback URL in LVB is mainly controlled by four parameters: `txTime`, `key` (hash key), `txSecret`, and validity period.

| Hotlink Protection Parameter | Description | Remarks |
|---------|---------|---------|
| txTime | Effective time of playback URL | This parameter is in hexadecimal UNIX time. <br>If the current value of `txTime` is greater than the current request time, the stream can be played back normally; otherwise, the playback will be rejected by the backend. |
| key | Key for MD5 calculation | This parameter can be customized. You can set a master key and a slave key, <br>so that if your master key is accidentally leaked, you can use the slave key to splice the playback URL and change the value of the master key. |
| txSecret | Encryption parameter in playback URL | The value of this parameter is obtained by performing MD5 encryption on the string spliced by `key`, `StreamName`, and `txTime`. <br>txSecret = MD5(key+StreamName+txTime). |
| Validity period | Validity period of address | The validity period must be set to greater than 0. <br>If `txTime` is set to the current time and the validity period is 300 seconds, then the playback URL expiration time is the current time + 300 seconds. |

#### Hotlink protection URL calculation
The calculation of a hotlink protection URL requires three parameters: `key` (a random string), `StreamName` (stream name), and `txTime` (in hexadecimal format).
Suppose that the `key` you set is **somestring**, the stream name (`StreamName`) is **test**, the `txTime` is **5c2acacc** (2019-01-01 10:05:00), the HD bitrate is **900 Kbps**, and the transcoding template name is **900**, then:
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
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage).
2. Select a playback domain name or click **Manage** to enter its details page.
3. Select **Access Control** and click **Edit**.
4. Enable **Playback Authentication** and click **Save**.

>
>- It takes **30 minutes** for the playback authentication configuration to take effect.
>- HTTP-FLV: the URL of the current playback will be able to continue playing back the stream after `txTime` expires but will be rejected when it requests a playback again.
>- HLS: as HLS uses a short link, it will continuously request .m3u8 files to get the latest ts segment. For example, if you set the value of `txTime` to the current time + 10 minutes, the HLS playback URL request will be rejected after 10 minutes. To solve this problem, you can dynamically update the HLS request address on the server or set the expiration time of the HLS playback address to be longer.

<span id="que7"></span>
### What are the format requirements for the master key in the playback authentication configuration? Is there any limit on its validity period?
The master key in the authentication configuration can contain 256 bits of uppercase and lowercase letters and digits. A random mix of letters and digits is enough.
You are recommended to set its validity period to the duration of the live stream.


<span id="que8"></span>
### After LVB recording is completed, how do I get the recording files?
The generated recording files are automatically stored in the VOD system and can be obtained in the following ways:
- VOD Console
- Recording event notification
- VOD API query

