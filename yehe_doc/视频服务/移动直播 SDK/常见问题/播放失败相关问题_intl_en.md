If you are unable to watch a live broadcast and do not know what the problem is, follow the steps below to locate the problem, which usually takes less than a minute.
![](https://main.qcloudimg.com/raw/a5236d378f73a7f08866f9531d501092.png)

### 1. Checking you playback URL
First, check whether your playback URL is correct. Incorrect URLs are the most common cause of playback failure. Tencent Cloud's LVB service uses a push URL and a playback URL. Make sure that you are not **wrongly using the push URL as the playback URL**.
![](https://main.qcloudimg.com/raw/d4886120f162625b9109417d24c21b5f.png)
>? “domain” is the push/playback domain name; “AppName” and “StreamName” are custom values (default “AppName”: `live`). If push or playback authentication is not enabled, the URL ends before “?”. For example, if the push domain name is `www.push.com`, “AppName” `live`, “StreanName” `test01`, and push authentication is not enabled, the push URL will be `rtmp://www.push.com/live/test01`.
>You can obtain playback URLs for LVB Lite through debugging. Search in code for **startPlay**, where LVB Lite calls the RTMP SDK, and set a debugging breakpoint. The value of `startPlay` is the playback URL.

### 2. Checking video streams
A correct playback URL does not guarantee normal playback. You need to check the video stream as well.
In **LVB**, a playback URL becomes unavailable once the host stops pushing streams.
In **VOD**, you cannot watch a video if the video file has been removed from the cloud.

A common method to check video streams is using VLC, an open-source player for PC that supports a range of protocols.
![](https://main.qcloudimg.com/raw/8c2b9524e8528d5139d15753a09f6689.png)

### 3. Checking the player
If there's no problem with the video stream, the next step is checking whether the player is normal.

- **Web browser**
	**Format**: Mobile browsers support only playback URLs in the **HLS (m3u8) or MP4** format.
	**HLS (m3u8)**: Tencent Cloud uses a lazy start mechanism for HLS transcoding. That is to say, it starts transcoding video to the HLS format only after a viewer requests playback via an HLS URL. This is to prevent the waste of resources, but the problem it brings is that **watching through an HLS playback URL is possible only 30 seconds after the first user sends a request worldwide**.
	- **Tencent Cloud web browser:** Tencent Cloud’s web browser supports playback URLs that use different protocols and can select the best playback strategy based on the platform used (PC/Android/iOS). Additionally, its selective retry logic offers a solution to the lazy start issue.

-  **RTMP SDK**
If playback is possible with the [RTMP SDK demo](https://intl.cloud.tencent.com/document/product/1071/38147), we recommend that you check the integration logic. For details, see the RTMP SDK playback documents [iOS](https://intl.cloud.tencent.com/document/product/1071/38159) and [Android](https://intl.cloud.tencent.com/document/product/1071/38160).

### 4. Checking firewall restrictions
Firewall restrictions are a common cause of playback failure. Many companies’ office networks set restrictions against video playback by having the firewall check whether a HTTP request is for streaming media. If you can watch an LVB using 4G, but not using your company’s office Wi-Fi, it indicates that the cause of the problem is firewall restrictions. Contact your company’s IT department and see if they can lift the restrictions for you IP address.

### 5. Checking the push
If playback is simply impossible with an LVB URL, and no firewall restrictions are set, the problem is likely push failure. You can troubleshoot the issue by following the instructions in FAQs > Push Failure.



 
