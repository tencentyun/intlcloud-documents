Based on VOD playback control capability, pseudo-live streaming adds access controls of “playback time constraint” and “syncing playback progress” to achieve pseudo-live streaming. Users first generate on-demand files, and then specify a time point to use such file for pseudo-live streaming. This feature has lower risks and cost compared with real live streaming. 

## Features
- **Low cost**: to convert a VOD video to a common live streaming for distribution, a user needs to use OBS software to push the video to the live streaming system and integrates with the entire system, which incurs high cost for development. Pseudo-live streaming can be realized within VOD platform as long as transcoding and hotlink protection are enabled.
- **Low risk for violating rules**: users can edit on-demand files and perform inappropriate information recognition in advance to avoid risk of violating rules during the live streaming.
- **Simple and flexible**:
	- No live streaming rooms are needed and any videos can be used for pseudo-live streaming.
	- There is no upper limit on concurrencies. You can specify a start time of the pseudo-live streaming and distribute playback URL beforehand.

## Use Cases
- Mainly used in scenarios where videos need to be recorded beforehand and viewed by users concurrently at a preset time. Users can get the playback URL in advance but cannot watch the video before the preset time. 
- Ongoing pseudo-live streaming cannot be sped up. This feature is commonly used in live courses, live gala, and other scenarios of radio and TV.

## Notes

### Limits
As pseudo-live streaming is based on on-demand content, it lacks some capabilities of a real live streaming, such as:
- You cannot collect statistics of “one session” of pseudo-live streaming.
- There is no clear indications of the start and end of a pseudo-live streaming.
- You cannot pause/terminate an ongoing pseudo-live streaming.
- You cannot ban a pseudo-live streaming URL that has been distributed.
- You cannot dynamically change the video content (such as real-time transcoding and watermarking).

### Glossary
**Allowed watch time**: video URL can be distributed to viewers in advance. Pseudo-live streaming cannot be viewed before the start and after the end of it, and can only be viewed when it is “ongoing”.
**Synchronized viewing**: during a pseudo-live streaming, all viewers watch synchronously with the same progress (with differences in minutes).


## Prerequisites
- You have [signed up](https://intl.cloud.tencent.com/register) and [logged in to](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fcloud.tencent.com) a Tencent Cloud account, and completed the identity verification. Unverified users cannot purchase instances of live recording to VOD for Chinese mainland.
- You have activated both the CSS and VOD services. If not, please go to [CSS](https://console.cloud.tencent.com/live/livestat) and [VOD](https://console.cloud.tencent.com/vod/overview) consoles to activate.
- For more information, see [Live Transcoding to VOD](https://intl.cloud.tencent.com/zh/document/product/266/39562).

## Directions
### Step 1. Upload a video to VOD
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/media) (non-admin) and click **Media Assets** > **Video Management** in the left sidebar, and the click **Upload Video**.
You can also use other video upload methods as appropriate for your business. For details, see [Media Upload Overview](https://intl.cloud.tencent.com/document/product/266/9760) and [Live Transcoding to VOD](https://intl.cloud.tencent.com/zh/document/product/266/39562).
<span id="HLS"></span>

### Step 2. Transcode the video into .hls format
1. Videos for pseudo-live streaming must be in .hls format. You can transcode an uploaded video into .hls format according to directions in [Transcoding Task Initiation](https://intl.cloud.tencent.com/document/product/266/33938). You can choose a [transcoding template](https://intl.cloud.tencent.com/document/product/266/14059) as appropriate for your business.
2. After the transcoding is finished, you can view the URL of the .hls format file in [Media Asset Management](https://intl.cloud.tencent.com/document/product/266/33895) in the console or get the URL via the [event notification(https://intl.cloud.tencent.com/document/product/266/33938). 

### Step 3. Enable key hotlink protection
1. To use pseudo-live streaming, you must enable hotlink protection. Please log in to the [VOD console](https://console.cloud.tencent.com/vod) and click **Distribution and Playback** > **Domain Management** in the left sidebar.  Find the target domain name, and click **Set**.
2. Click **Edit** to enable the referer.
3. Enable referer/key hotlink protection.
For details on settings, see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/14060). After the configuration, please save the key for calculating the hotlink protection signature.

### Step 4. Calculate hotlink protection signature
<span id="functio"></span>
#### Signature calculation formula
```plaintext
sign = md5(KEY + Dir + t + plive + exper + rlimit + us)
```
>!Hotlink protection for pseudo-live streaming has one additional parameter compared with a [standard key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986): `plive`, which will be used to calculate the hotlink protection signature.

| Parameter | Value | Description |
| ------ | ---------------------- | -------------------------------------------------- |
| KEY    | 11111111| The key selected by a developer when enabling key hotlink protection                  |
| Dir | /dir1/dir2/ | The remaining part of the original video URL after `myVideo.mp4` is removed |
| t      | 5a71afc0             | Hexadecimal result of the expiration timestamp `1517400000`.          |
|plive|5e344f00|Start time of the pseudo-live streaming (UTC+8) in UNIX timestamp format. For example, `1577808000` means 00:00:00 at January 1, 2020. |
|exper|0| Preview duration. `0` means no limit. |
|rlimit|0|Maximum number of IPs allowed for watching. `0` means no limit.|
| us     | test          | The generated random string.                                   |


Suppose a developer stores a video in VOD with HLS-format playback URL (not the original video URL) as `http://1250000000.vod2.myqcloud.com/vodtranscq125000000/12345678/v.f240.m3u8; `. And the requirements are as follows:
- Key hotlink protection of the URL: `11111111`
- Expiration time `t`: `5e5a8a80` (March 1, 2020 00:00:00)
- Pseudo-live streaming start time `plive`: `5e344f00` (February 1, 2020 00:00:00)
- Preview duration `exper`: `0` (unlimited)
- Maximum number of IPs for watching `rlimit`: `0` (unlimited)
- Random string `us`: `test`


1. Calculate the signature according to [signature calculation formula](#function):
```plaintext
sign = md5(11111111/vodtranscq125000000/12345678/5e5a8a805e344f0000test) = 0af5018df88c00e6629e0fb8939277dd
```
2. Add the generated signature in the `QueryString` of the HLS URL to get the final hotlink protection URL:
```plaintext
http://1250000000.vod2.myqcloud.com/vodtranscq125000000/12345678/v.f240.m3u8?t=5e5a8a80&plive=5e344f00&exper=0&rlimit=0&us=test&sign=0af5018df88c00e6629e0fb8939277dd
```
	>?
	>- Parameters in `QueryString` should be calculated in the same order as for calculating `sign`: `t-plive-exper-rlimit-us-sign`.

## Using Pseudo-Live Streaming
You can put above URL in players supporting HLS playback (such as Safari browser, VLC, and PotPlayer) to try pseudo-live streaming.
>!Chrome browser does not support HLS playback. You need install a plugin.
