## Preparations
1. Activate the [CSS service](https://console.cloud.tencent.com/live?from=product-banner-use-lvb).
2. Log in to the [CSS console](https://console.cloud.tencent.com/live/livestat) to get a URL for live push. For detailed directions, please see [Live Push](https://intl.cloud.tencent.com/document/product/267/31558).
3. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage), click **Add Domain**, enter your domain name, select **Playback Domain** as the type, and click **Save**.
4. Log in to the [Tencent Cloud Domain Service Console](https://console.cloud.tencent.com/domain) and configure CNAME for the successfully added playback domain name. For detailed directions, please see [Domain Name CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057).

## Getting Playback URL
Select **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** to get a playback URL and configure as follows:
- Select **Playback Domain** as the type of the URL.
- Select a playback domain name you added in **Domain Management**.
- Enter the same `StreamName` as that of the push URL. The `StreamName` of the playback URL must be the same as that of the push URL to play back the corresponding stream.
- Select the expiration time of the URL, such as `2019-10-18 23:59:59`.
- Click **Generate Address**.
![](https://main.qcloudimg.com/raw/a2f130098eb40df252956ffb3752d230.png)

>? In addition to the above method, you can also select a playback domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the CSS console, click **Manage**, select **Playback Configuration**, enter the expiration time of the playback URL and the `StreamName` same as that in the push URL, and click **Generate Playback Address**.

## Live Playback
A [live push](https://intl.cloud.tencent.com/document/product/267/31558) must be successful before the stream can be watched via the playback URL. You can use the following methods to test live streaming based on your business scenario:

### Scenario 1. Playback on PC client
You can use tools such as [VLC](https://intl.cloud.tencent.com/document/product/267/32483), FFmepg, and [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/player/demo/player.html) for playback.
![](https://main.qcloudimg.com/raw/e47f8d4d9ca63e678439df3e8a17c9b4.png)
### Scenario 2. Playback on mobile client
1. Download the install [Tencent Cloud Toolkit](https://intl.cloud.tencent.com/document/product/1016/30285).
2. Select **MLVB** > **LVB Playback** or **LEB Playback**.
3. Enter the playback URL in the input box or scan the QR code of the playback URL.
4. Tap the play button in the bottom-left corner to start playback.

### Scenario 4. Playback on web
You are recommended to choose TCPlayerLite in the player SDK for playback. Based on Tencent Cloud's powerful backend functionality and AI technology, TCPlayerLite provides excellent playback capabilities for live streaming and video on-demand. Deeply integrated with the Tencent Cloud LVB and VOD services, Player+ features smooth and stable playback performance, advertising placement, and data monitoring.
>! Currently, most mobile browsers on the market do not support HTTP-FLV playback. Therefore, for web-based playback, you are recommended to select the HTTP-FLV playback protocol for PC browsers and HLS for mobile browsers. 

## FAQs
- [What playback protocols are supported?](https://intl.cloud.tencent.com/document/product/267/7968)
- [What does a playback address consist of?](https://intl.cloud.tencent.com/document/product/267/7968)
- [How can I use live transcoding?](https://intl.cloud.tencent.com/document/product/267/35598)
- [How can I use time shifting for replay?](https://intl.cloud.tencent.com/document/product/267/35598)
- [How can I use HTTPS for playback?](https://intl.cloud.tencent.com/document/product/267/35598)
- [How can I use a global cache node for playback?](https://intl.cloud.tencent.com/document/product/267/35598)
- [How can I enable hotlink protection?](https://intl.cloud.tencent.com/document/product/267/35598#que2)

