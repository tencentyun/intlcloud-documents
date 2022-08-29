This document shows you how to get started with LEB. Before using LEB, please read [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819) to learn about its **billable items** and **prices**.

[](id:step0)
## Prerequisites
1. You have [signed up for a Tencent Cloud account](https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F).
2. Go to the [CSS console](https://console.cloud.tencent.com/live?from=product-banner-use-lvb), agree to **Tencent Cloud Service Agreement**, and click **Apply for Activation** to activate CSS.
>?  
>- After activating CSS, you will get 20 GB of playback traffic for the Chinese mainland for free.
>- The steps to configure domain names for LEB are the same as those for LVB. If you are already using LVB, you can skip to [Step 4. Get a playback URL](#step4).

[](id:step1)
## Step 1. Add domain names
To use CSS, you should have at least one **push domain name** and one **playback domain name**. You cannot use one domain name for both push and playback.
You can [add your own domain names](https://intl.cloud.tencent.com/document/product/267/35970).

1. Register your domain name. ICP filing is required if you want to use the domain in the Chinese mainland.

2. Log in to the CSS console and select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar.

3. Click **Add Domain**.

   ![](https://main.qcloudimg.com/raw/771bbce97962dcd1cffdd94324941280.png)
>?
>- CSS provides a test domain name `xxxx.livepush.myqcloud.com`. You can use it to test push, but we do not recommend using it for business purposes.
>- After the domain name is added successfully, you can view its information in the domain name list in **Domain Management**. For information on how to manage your domains, see [Domain Management](https://intl.cloud.tencent.com/document/product/267/31056).
>- For more information on domain names for live streaming, see [Live Streaming Basics](https://intl.cloud.tencent.com/document/product/267/7968).
5. Once your domain name is added, the system will assign it a canonical name (suffixed with `.tlivecdn.com` or `.tlivepush.com`), which cannot be accessed before you complete CNAME configuration at your DNS service provider. The following example shows you how to add a CNAME record if you use Tencent Cloud’s DNS service:[](id:step1_1_1)
    1. Log in to the [DNS console](https://console.cloud.tencent.com/domain).
    2. Find your domain name and click **Resolve**.
    3. On the domain name resolution page, click **Add Record**.
    4. Enter your domain name prefix for **Host Record**, select CNAME for **Record Type**, and enter the canonical name for **Record Value**.
    5. Click **Save**.
>!
>- It takes a while for CNAME configuration to take effect. You can use CSS only after it does.
>- After the CNAME configuration takes effect, you will see the ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png) icon before the CNAME address in [Domain Management](https://console.cloud.tencent.com/live/domainmanage).
>- If your CNAME configuration fails to take effect, please contact your DNS provider.
>- For how to add CNAME records with other DNS providers, see [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).

## Step 2. Get a push URL

1. Go to **CSS Toolkit** > [Address Generator](https://console.intl.cloud.tencent.com/live/addrgenerator/addrgenerator).
2. Complete the following settings:
   1. Select **Push Domain** for **Domain Type**.
   2. Select a push domain name you added in **Domain Management**.
   3. Enter a custom `StreamName`, such as `liveteststream`.
   4. Select a URL expiration time, such as `2021-05-25 23:59:59`.
   5. Click **Generate Address** to generate a push address.
![](https://main.qcloudimg.com/raw/5a377614d5da22c5193bef68f4a3a6e7.png)

>? 
>- The default value of `AppName` is `live`. `txSecret` is the signature for playback, and `txTime` is the URL expiration time.
>- Here is another way to generate a push URL: In [Domain Management](https://console.cloud.tencent.com/live/domainmanage), find the domain name you want to use for push and click **Manage**. Under **Push Configuration**, select an expiration time for the URL, enter a custom `StreamName`, and click **Generate Push Address**.
>- Before generating a push URL, you can create [templates](https://intl.cloud.tencent.com/document/product/267/31069) and bind them to your push domain. For the prices of CSS value-added services, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819).

[](id:step3)
## Step 3. Start pushing


To start pushing, provide the push URL generated to the software you use for push.
- For push on PCs, we recommend you use OBS. You need to [configure the OBS plugin](https://intl.cloud.tencent.com/document/product/267/42131) first. For subsequent steps, see [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).
- For push on web, we recommend you use [Web Push](https://console.intl.cloud.tencent.com/live/tools/webpush): Click **Generate**. In the pop-up window, select a push domain name, enter a custom `StreamName`, select a URL expiration time, and click **Confirm**. Turn the camera on, and click **Start Push**.
- For push from mobile devices, download the TCToolkit app, open it, go to the live push page, and enter the push URL manually or scan the QR code generated in the previous step to auto-fill the URL. Tap **Start Push**.

>? 
>
>- You can integrate the MLVB SDK into your app to implement the push feature.
>- The LEB solution for web does not support decoding or playing B-frames. For details, see [B-Frames](#b_frame).

[](id:step4)
## Step 4. Get the playback URL

1. After push succeeds, select [Stream Management](https://console.cloud.tencent.com/live/streammanage) on the left sidebar. Under the **Live Streams** tab, you can view the status of the push URL. You can also click **Preview** to play the stream.
2. Go to **CSS Toolkit** > [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) and complete the following settings:
   1. Select **Playback Domain** for **Domain Type**.
   2. Select a playback domain name you added in **Domain Management**.
   3. For **StreamName**, enter the `StreamName` in the push URL.
   4. Select a URL expiration time, such as `2021-05-25 23:59:59`.
   5. Select a transcoding template if you want to transcode the stream and get a playback URL of the transcoded stream. This step is not necessary if you play the original stream.
   5. Click **Generate Address** to generate an LEB playback URL whose format is `webrtc://domain/path/stream_id`.
![](https://main.qcloudimg.com/raw/5025e22cd8c4c555d7de3e0360e13d11.png)
3. You can use the following methods to test playback in different scenarios:
   - **Playback on web**: We recommend you use the [TCPlayer demo](https://tcplayer.vcube.tencent.com) to test playback.
>?
>- The demo supports changing video quality during playback. You can create a transcoding template to output HD and SD videos in **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode), enter in the demo a WebRTC URL containing the transcoding template, and play it. If you don't need to test this feature, enter the original WebRTC URL.
>- For more information on live transcoding and its billing, see [Live Transcoding](https://intl.cloud.tencent.com/document/product/267/31071).

   - **Playback on mobile devices**: We recommend you use the TCToolkit app to test playback on mobile devices. Open the app, select **Live broadcast > LEB Player**, enter the playback URL manually or scan the QR code generated in the previous step to auto-fill the URL, and then tap **Start Playback**.
>? If you want to play the stream in your app, you can integrate the MLVB SDK. If you have any questions, see [FAQs](#que).

## Step 5. Use LEB
Our LEB solution for **mobile devices** supports B-frame decoding and playback of AAC files. It has been integrated into the MLVB SDK.

[](id:que)
## FAQs
[](id:play_url)
### Generating playback URLs
The format of LEB URLs is the same as that of LVB URLs except that the former start with `webrtc` while the latter start with `rtmp`.

LEB playback URL format: `webrtc://domain/path/stream_id` or `webrtc://domain/path/stream_id?txSecret=xxx&txTime=xxx` ([hotlink protection](https://intl.cloud.tencent.com/document/product/267/31560) enabled). For how to generate a playback URL, see [Get the playback URL](#step4).

>? You can use URLs of transcoded streams to play at different resolutions and bitrates. For how to generate a playback URL for a transcoded stream, see [Live Remuxing and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).

[](id:b_frame)
### B-frames
The LEB solution for web **does not support decoding or playing B-frames**. If a stream contains B-frames, the backend will remove them in transcoding, which will increase latency and **incur transcoding fees**. Please avoid pushing streams with B-frames or use streaming software such as OBS to remove them by adjusting the video encoding parameters. The figure below shows how to remove B-frames using OBS:
![](https://main.qcloudimg.com/raw/b28d5919589364e6a1f78d62e0b58c47.png)

[](id:a_transcoding)
### Audio transcoding
Playback using browsers only supports the standard WebRTC protocol and does not support AAC. If a stream pushed contains audio in AAC format, the system will transcode the audio into Opus format, which will incur [audio transcoding](https://intl.cloud.tencent.com/document/product/267/39604) fees.
