This document describes how to get started with LEB. Before trying out LEB, you’re advised to read the [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819) of LEB to get familiar with its **billable items** and **prices**.

[](id:step0)
## Preparations
1. Sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629). Unverified users cannot purchase CSS instances in the Chinese mainland.
2. Go to the [CSS service activation page](https://console.cloud.tencent.com/live?from=product-banner-use-lvb), indicate your consent to the "Tencent Cloud Service Terms", and click **Apply for Activation** to activate the CSS service.
>?  
>- After the CSS service is activated, 20 GB of playback traffic for use in the Chinese mainland will be gifted.
>- The steps to configure domain names for LEB are the same as those for LVB. If you have activated LVB, you can get started with LEB from [Step 4. Get a playback URL](#step4).

[](id:step1)

## Step 1. Add domain names
To use CSS, you should have at least one **push domain name**, and one **playback domain name**. You cannot use one domain name for both push and playback.
You can add **[your own domain names](https://intl.cloud.tencent.com/document/product/267/35970)**.

1. Prepare your own domain names. For domain names in Chinese mainland regions, ICP filing is required.

2. Log in to the CSS console and enter **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**.

3. Click **Add Domain**.

   ![](https://main.qcloudimg.com/raw/771bbce97962dcd1cffdd94324941280.png)
>?
>- CSS provides a test domain name `xxxx.livepush.myqcloud.com`. You can use it to test live push, but you're not advised to use it as the push domain name for business purposes.
>- After the domain name is added successfully, you can view its information in the domain name list in **Domain Management**. For how to manage it, see [Domain Management](https://intl.cloud.tencent.com/document/product/267/31056).
>- For more information on live streaming domain names, please see [Basic CSS Features](https://intl.cloud.tencent.com/document/product/267/7968).
5. Once your domain name is added, the system will assign it a CNAME domain name (suffixed with `.tlivecdn.com` or `.tlivepush.com`), which cannot be accessed before you complete the CNAME configuration at your DNS service provider. After the CNAME configuration takes effect, you can use CSS. The following example shows you how to add a CNAME record by assuming Tencent Cloud is your DNS service provider:[](id:step1_1_1)
    1. Log in to the [Tencent Cloud Domain Name Service console](https://console.cloud.tencent.com/domain).
    2. Find the target domain name and click **Resolve**.
    3. On the domain name resolution page, click **Add Record**.
    4. In the new line, enter the domain name prefix as the host record, select CNAME as the record type, and enter the CNAME domain name as the record value.
    5. Click **Save**.
>!
>- After a CNAME record is successfully added, it takes some time for the CNAME configuration to take effect. If the configuration fails, you cannot use CSS.
>- After the CNAME configuration succeeds, you can see that the status symbol of the CNAME address in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the CSS console has changed to ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png).
>- If the CNAME configuration failure persists, consult your DNS service provider.
>- For more information on how to configure with other DNS service providers, see [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).

## Step 2. Get push URL

1. Select **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**.
2. On the **Address Generator** page, configure as follows:
   1. Select **Push Domain** for **Domain Type**.
   2. Select a push domain name you added in **Domain Management**.
   3. Enter a custom `StreamName`, such as `liveteststream`.
   4. Select a URL expiration time, such as `2021-05-25 23:59:59`.
   5. Click **Generate Address** to generate a push address.
![](https://main.qcloudimg.com/raw/5a377614d5da22c5193bef68f4a3a6e7.png)

>? 
>- In the push URL, `live` is the default `AppName`, `txSecret` is the signature for playing back the stream, and `txTime` is the URL expiration time.
>- Here is another way to generate a push URL: In **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, find the push domain name you want use to generate a push URL, click **Manage**, select **Push Configuration**, enter an expiration time for the address and a custom `StreamName`, and click **Generate Push Address**.
>- You can create and configure a desired [feature template](https://intl.cloud.tencent.com/document/product/267/31069) before generating the push URL based on your business needs and bind it to the push domain name. For prices of CSS value-added features, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819).

[](id:step3)
## Step 3. Push live stream

You can enter the generated push URL into the push software as appropriate for your use cases.
- For push on PCs, you're advised to use OBS. For subsequent steps, see [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).
- For push on web, you're advised to use **CSS Toolkit** > **[Web Push](https://console.cloud.tencent.com/live/tools/webpush)**: select a push domain name, enter a custom `StreamName`, select a URL expiration time, turn the camera on, and click **Start Push**.    
- For push on mobile devices, download and install [Tencent Video Cloud Demo](https://intl.cloud.tencent.com/document/product/1071/38147), open it, select **Mobile Live Video Broadcasting** > **Push (Camera)**, enter the push URL into the address box manually or by scanning the QR code, and then tap the start icon in the bottom-left corner.

>? 
>- You can integrate Tencent Cloud [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071) into customized apps for live push.
>- The LEB solution for web does not support decoding and playing back B-frames. For details, see [B-Frames](#b_frame).

[](id:step4)
## Step 4. Get playback URL

1. After push succeeds, select **[Stream Management](https://console.cloud.tencent.com/live/streammanage)** > **Online Streams**, view the status of the push address, and click **Test** to play back the stream online.
2. Select **CSS Toolbox** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** to get a playback address and configure as follows:
   1. Select the type of generation, such as playback domain name.
   2. Select a playback domain name you added in **Domain Management**.
   3. Enter the `StreamName` in the push URL to play back the corresponding stream.
   4. Select a URL expiration time, such as `2021-05-25 23:59:59`.
   5. Select a transcoding template if you want to get a playback URL for a transcoded stream. This step is not needed if you want to get a playback URL for the original stream.
   5. Click **Generate Address** to generate an LEB playback URL whose format is `webrtc://domain/path/stream_id`.
![](https://main.qcloudimg.com/raw/5025e22cd8c4c555d7de3e0360e13d11.png)
3. You can use the following methods to test whether a live stream can be played back normally in different use cases:
   - **Playback test on web**: you’re advised to use [WebRTC Live Demo](https://tcplayer.vcube.tencent.com/webrtc-demo/index.html) to test playback.
>?
>- WebRTC Live Demo supports the multi-definition feature. You can configure transcoding templates for HD and SD in **Feature Configuration** > [**Live Transcoding**](https://console.cloud.tencent.com/live/config/transcode) in the CSS console, enter a WebRTC stream address containing a transcoding template, test it, and then play it back. (If you don't need to test this feature, simply enter a WebRTC original stream in the demo.)
>- For more information on live transcoding operations and billing, see [CSS Transcoding](https://intl.cloud.tencent.com/document/product/267/31071).
   - **Playback test on mobile devices**: you're advised to download and install [Tencent Video Cloud Toolkit](https://intl.cloud.tencent.com/document/product/1071/38147) app, select **Mobile Live Video Broadcasting** > **LEB Playback**, enter the playback URL you get from push trial into the address box manually or by scanning the QR code, and tap the play icon in the bottom-left corner.
>? To push/play back a stream on an app, you can integrate the [MLVB SDK](https://intl.cloud.tencent.com/product/mlvb) into the app to supplement the LEB service. If you encounter any problems, see [FAQs](#que).

## Step 5. Start to use LEB
- **LEB solution for mobile devices**: supports B-frame decoding and AAC audio codec. This solution is integrated into the MLVB SDK. For how to use it, see [LEB Playback](https://intl.cloud.tencent.com/document/product/1071/41875).
-**LEB solution for web**: has been integrated into the TCPlayerLite player.

[](id:que)
## FAQs
[](id:play_url)
### Generating playback URL
The format of LEB playback URL is the same as that of LVB playback URL except that the former starts with `webrtc` while the latter starts with `rtmp`.

LEB playback URL format: `webrtc://domain/path/stream_id` or `webrtc://domain/path/stream_id?txSecret=xxx&txTime=xxx` ([hotlink protection](https://intl.cloud.tencent.com/document/product/267/31560) enabled). For how to generate a playback URL, please see [Get playback URL](#step4).

>? You can also pull transcoded streams of different resolutions and bitrates. For information about generating playback URLs for transcoded streams, please see [Live Remuxing and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).

[](id:b_frame)
### B-frames
The LEB solution for web **does not support decoding and playing back B-frames**. If the original stream contains B-frames, the backend will remove them by transcoding, which will result in latency and **incur transcoding fees**. We recommend not pushing streams with B-frames. You can also adjust the video codec parameter on push client software (such as OBS) to remove B-frames. If you use OBS for push, you can set to disable B-frames, as shown below:
![](https://main.qcloudimg.com/raw/b28d5919589364e6a1f78d62e0b58c47.png)

[](id:a_transcoding)
### Audio transcoding
Playback by web browser only supports standard WebRTC protocol and does not support AAC audio codec. If you push streams with audio in AAC format, the audio will be transcoded into Opus format, which will incur [audio transcoding fees](https://intl.cloud.tencent.com/document/product/267/39604).
