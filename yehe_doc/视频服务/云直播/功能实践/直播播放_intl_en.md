## Preparations
1. Activate the [CSS service](https://console.cloud.tencent.com/live?from=product-banner-use-lvb) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Log in to the [CSS console](https://console.cloud.tencent.com/live/livestat) to get a push address for CSS push. For detailed directions, please see [CSS Push](https://intl.cloud.tencent.com/document/product/267/31558).
3. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage), click **Add Domain**, enter your ICP filed domain name, select **Playback domain** as the type, and click **Save**.
>!
>
>- If you do not have a domain name, you can purchase one through **[Tencent Cloud Domain Service](https://intl.cloud.tencent.com/)**. You can also purchase one at another domain name service provider.
4. Log in to the [Tencent Cloud Domain Service console](https://console.cloud.tencent.com/domain) and configure CNAME for the successfully added playback domain name. For detailed directions, please see [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).

## Getting Playback Address
Select **Auxiliary Tools** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** in the CSS console to get a playback address and configure as follows:
- Select **playback domain name** as the type of address to generate.
- Select the playback domain name you added in **Domain Management**.
- Enter the same `StreamName` as that of the push address. The `StreamName` of the playback address must be the same as that of the push address to play back the corresponding stream.
- Select the expiration time of the address, such as `2019-12-13  23:59:59`.
- Click **Generate Address**.
![](https://main.qcloudimg.com/raw/a2f130098eb40df252956ffb3752d230.png)
>?In addition to the above method, you can also select a playback domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the CSS console, click **Manage**, select **Playback Configuration**, select the expiration time of the playback address, enter the same `StreamName` as that of the push address, and click **Generate Playback Address**.

## CSS Playback
You need to successfully perform [CSS push](https://intl.cloud.tencent.com/document/product/267/31558) first before the stream can be watched at the playback address. You can use the following methods to test live streaming based on your business scenario:

### Scenario 1. PC playback
You can use tools such as [VLC](https://intl.cloud.tencent.com/document/product/267/32483), FFmepg, and [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/player/demo/player.html) for playback.
### Scenario 2. Mobile playback
1. Download and install the [Tencent Video Cloud demo](https://intl.cloud.tencent.com/document/product/1071/38147).
2. Open **MLVB** > **CSS Pull**.
3. Enter the playback address in the text box or scan the QR code of the playback address.
4. Tap **Play** in the bottom-left corner for playback.

>? If you need to push/play back a stream in an app, you can integrate the [MLVB SDK](https://intl.cloud.tencent.com/product/mlvb) to use the CSS service, which supports RTMP, HTTP-FLV, and HLS playback protocols.

### Scenario 4. Web playback
We recommend you choose TCPlayerLite in the player SDK for playback. Based on Tencent Cloud's powerful backend functionality and AI technology, TCPlayerLite provides excellent playback capabilities for live streaming and video on-demand. Deeply integrated with the Tencent Cloud CSS and VOD services, Player+ features smooth and stable playback performance, advertising placement, and data monitoring.
>! Currently, most mobile browsers on the market do not support HTTP-FLV playback. Therefore, for web playback, we recommend you select the HTTP-FLV playback protocol for PC browsers and HLS for mobile browsers.


## FAQs
- [What playback protocols are supported?](https://intl.cloud.tencent.com/document/product/267/7968)
- [What does a playback address consist of?](https://intl.cloud.tencent.com/document/product/267/7968)
- [How can I use live transcoding?](https://intl.cloud.tencent.com/document/product/267/35598)
- [How can I use time shifting for replay?](https://intl.cloud.tencent.com/document/product/267/35598)
- [How can I use HTTPS for playback?](https://intl.cloud.tencent.com/document/product/267/35598)
- [How can I use a global cache node for playback?](https://intl.cloud.tencent.com/document/product/267/35598)
- [How can I enable hotlink protection?](https://intl.cloud.tencent.com/document/product/267/35598)

