[](id:que1)
### Is there an upper limit on the number of concurrent viewers? 
CSS does not limit the number of concurrent viewers. A live stream can be viewed by as many users as the network allows. However, if you have set a bandwidth limit, new viewers will be unable to watch a live stream once the limit is reached.

[](id:que2)
### How do I use transcoding for playback?
You may want to use different bitrates and resolutions under different network conditions. You can [create transcoding templates](https://console.cloud.tencent.com/live/config/transcode) with different bitrates and resolutions in the console. For more information about transcoding, see [Best Practice > CSS Encapsulating and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).

[](id:multirate)
 #### Original definition, HD, and SD
The three commonly used playback bitrates for original-definition, HD, and SD streams are as follows: 
 - For an original-definition stream, the playback bitrate is the same as the publishing bitrate.
 - For an HD (1080p) stream, the recommended playback bitrate is 2,000 Kbps.
 - For an SD (720p) stream, the recommended bitrate is 1,000 Kbps.

[](id:que3)
### How can I use time shifting for replay?
You can use the time shifting feature to replay highlights. The feature supports only the HLS protocol for the time being. For more information on time shifting and how to activate it, see [Best Practices > CSS Time Shifting](https://intl.cloud.tencent.com/document/product/267/31565).

[](id:que4)
### How can I use HTTPS for playback?
If you want your playback domain name to support HTTPS, make sure you have a valid certificate and private key, and go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), find your playback domain name, click **Manage**, select **Advanced Configuration**, and add configurations in **HTTPS Configuration**. It may take a while (2 hours) for the configurations to take effect, after which your streams can be played back over the HTTPS protocol.

[](id:que5)
### How can I use an acceleration node outside the Chinese mainland for playback?
CSS has CDN nodes across the Chinese mainland and around the world, with extensive coverage and high stability. If your end users are outside the Chinese mainland, you can select **Global Acceleration** or **Hong Kong/Macao/Taiwan (China Region) and other regions** for acceleration region when configuring your domain name in [Domain Management](https://console.cloud.tencent.com/live/domainmanage).
>! Global acceleration supports only the HTTP-FLV and HLS protocols for the time being.

[](id:que6)
### How can I enable hotlink protection?
To prevent unauthorized users from accessing your playback URLs, which would consume your Tencent Cloud traffic, you are strongly advised to enable hotlink protection for your playback URLs to avoid potential losses caused by hotlinking. With CSS, hotlink protection for playback URLs is controlled by four parameters: `txTime`, `key` (hash key), `txSecret`, and the validity period.

| Hotlink Protection Parameter | Description | Remarks |
|---------|---------|---------|
| txTime | Effective time of playback URL |It is a Unix hexadecimal time.<br> If the value of `txTime` is greater than the time of a request, the stream can be played back successfully; otherwise the request will be rejected.|
| key | MD5 key | You can customize a key as well as set a master and slave key.<br> If your master key is leaked, you can use the slave key to splice playback URLs and change the value of the master key.|
| txSecret | Encryption parameter in playback URL | The value of this parameter is calculated based on `key`, `StreamName`, and `txTime` using the MD5 algorithm. <br>`txSecret` = MD5 (key+StreamName+txTime) |
| Validity period | Validity period of playback URL | It must be greater than 0.<br> If `txTime` is set to the current time and the validity period is 300 seconds, then the playback URL expiration time is the current time + 300 seconds.|

#### Hotlink protection URL calculation
The calculation of a hotlink protection URL requires three parameters: `key` (a random string), `StreamName` (stream name), and `txTime` (in the hexadecimal format).
Suppose you set `key` to **somestring**, the stream name (`StreamName`) to **test**, `txTime` to **5c2acacc** (2019-01-01 10:05:00), the HD bitrate to **900 Kbps**, and the name of the transcoding template to **900**.
The playback URL for an original-definition stream would be:
```
txSecret = MD5(somestringtest5c2acacc) = b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.flv?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.m3u8?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
```
The playback URL for an HD stream would be:
```
txSecret = MD5(somestringtest_9005c2acacc) = 4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.flv?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.m3u8?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
```

#### Enabling hotlink protection
1. Log in to the CSS console and click **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**.
2. Find and click your playback domain name or click **Manage** to enter the details page.
3. Select **Access Control** and click **Edit**.
4. Enable **Playback Authentication** and click **Save**.

>!
>- It takes **30 minutes** for the configuration to take effect.
>- HTTP-FLV: ongoing playback can continue even after the URL expires, but new requests for playback via the URL will be rejected.
>- HLS: as HLS breaks a stream into short chunks, it keeps requesting M3U8 files to get the latest TS segments. Suppose you set `txTime` to the current time and the validity period to 10 minutes, then an HLS playback URL request sent 10 minutes after the current time will be rejected. To avoid this, you can update the HLS request URL dynamically on the server or set longer validity periods.

[](id:que7)
### What format requirements must a master key for playback authentication meet? Is there any limit on its validity period?
A master key for playback authentication can be a random combination of uppercase and lowercase letters and digits and must not be longer than 256 bits.
We recommend that you set the validity period to the duration of a live stream.


[](id:que8) 
### I recorded live streams. How can I get the recording files?
Recording files are automatically saved in the VOD system after generation and can be found via:
- [VOD console](https://intl.cloud.tencent.com/document/product/267/31563)
- [Recording event notification](https://intl.cloud.tencent.com/document/product/267/31563)
- [VOD querying APIs](https://intl.cloud.tencent.com/document/product/267/31563)

