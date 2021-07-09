This document describes how to get started with LEB. Before trying out LEB, you’re advised to read the [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819) of LEB to get familiar with its **billable items** and **prices**.

[](id:step0)

## Preparations
1. Sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Go to the [CSS service activation page](https://console.cloud.tencent.com/live?from=product-banner-use-lvb), indicate your consent to the “Tencent Cloud Service Terms”, and click **Apply for Activation** to activate the CSS service.
>?  
 
>- The steps to configure domain names for LEB are the same as those for LVB. If you have activated LVB, you can get started with LEB from [step 4. Get a playback URL](#step4).

[](id:step1)

## Step 1. Add domain names
To use CSS, you should have at least one **push domain name**, and one **playback domain name**. You cannot use one domain name for both push and playback.
You can add **[your own domain names](https://intl.cloud.tencent.com/document/product/267/35970)**.

1. Prepare your domain name.
	 
	 
  
2. Log in to the CSS console, enter **[Domain Management](https://console.intl.cloud.tencent.com/live/domainmanage)**.
3. Click **Add Domain**.
4. Enter your domain name, select the domain name type, and click **Confirm**.
![](https://main.qcloudimg.com/raw/bee8085a9d29641ddab913fdcd9c75ab.png)
>?
>- CSS provides a test domain name `xxxx.livepush.myqcloud.com`. You can use it to test live push, but you’re not advised to use it as the push domain name for business purposes.
>- After the domain name is added successfully, you can view its information in the domain name list in **Domain Management**. For how to manage it, please see [Domain Management](https://intl.cloud.tencent.com/document/product/267/31056).
>- For more information on live streaming domain names, please see [Basic CSS Features](https://intl.cloud.tencent.com/document/product/267/7968).
5. Once your domain name is added, the system will assign it a CNAME domain name (suffixed with `.tlivecdn.com` or `.tlivepush.com`), which cannot be accessed before you complete the CNAME configuration at your DNS service provider. After the CNAME configuration takes effect, you can use CSS. The following example shows you how to add a CNAME record by assuming Tencent Cloud is your DNS service provider:[](id:step1_1_1)
    1. Log in to the [Tencent Cloud Domain Name Service console](https://console.cloud.tencent.com/domain).
    2. Find the target domain name, and click **Resolve**.
    3. On the domain name resolution page, click **Add Record**.
    4. In the new line, enter the domain name prefix as the host record, select CNAME as the record type, and enter the CNAME domain name as the record value.
    5. Click **Save**.
>!
>- After a CNAME record is successfully added, it takes some time for the CNAME configuration to take effect. If the configuration fails, you cannot use CSS.
>- After the CNAME configuration succeeds, you can see that the CNAME status has changed to ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png) in **[Domain Management](https://console.intl.cloud.tencent.com/live/domainmanage)** of the CSS console.
>- If the CNAME configuration failure persists, consult your DNS service provider.
>- For more information on how to configure with other DNS service providers, please see [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).

## Step 2. Get push URL

1. Select **CSS Toolkit** > **[Address Generator](https://console.intl.cloud.tencent.com/live/addrgenerator/addrgenerator)**.
2. On the **Address Generator** page, configure as follows:
   1. Select **Push Domain** for **Domain Type**.
   2. Select a push domain name you added in **Domain Management**.
   3. Enter a custom `StreamName`, such as `liveteststream`.
   4. Select a URL expiration time, such as `2021-05-25  23:59:59`.
   5. Click **Generate Address** to generate a push URL.
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)

>? 
>- In the push URL, `live` is the default `AppName`, `txSecret` is the signature for playing back the stream, and `txTime` is the URL expiration time.
>- In addition to the above method, you can also find the push domain name in **[Domain Management](https://console.intl.cloud.tencent.com/live/domainmanage)** of the CSS console, click **Manage**, and select **Push Configuration**. In the **Push Address Generator** section, enter a push URL expiration time and a custom `StreamName`, and then click **Generate Push Address** to generate a push URL.
>- You can create and configure a desired [feature template](https://intl.cloud.tencent.com/document/product/267/34223) before generating the push URL based on your business needs and bind it to the push domain name. For prices of CSS value-added features, please see [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819).

[](id:step3)
## Step 3. Push live stream

You can enter the generated push URL into the push software as appropriate for your use cases.
- For push on PCs, you’re advised to use OBS. For detailed directions, please see [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).
- For push on web, you’re advised to use **CSS Toolkit** > **[Web Push](https://console.intl.cloud.tencent.com/live/tools/webpush)**: select a push domain name, enter a custom `StreamName`, select a URL expiration time, turn the camera on, and click **Start Push**.    
- For push on mobile devices, download and install Tencent Video Cloud Demo, open it, select **Mobile Live Video Broadcasting** > **Push (Camera)**, enter the push URL into the address box manually or by scanning the QR code, and then tap the start icon in the bottom-left corner.

>? 
>
>- You can integrate Tencent Cloud [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071) into customized apps for live push.
- LEB solution for web does not support decoding and playing back B-frames. For details, please see [B-Frames](#b_frame).

[](id:step4)

## Step 4. Get playback URL

1. After the push succeeds, select **[Stream Management](https://console.intl.cloud.tencent.com/live/streammanage)** > **Live Streams**, view the status of the target stream, and click **Test** to play back it.
2. Select **CSS Toolkit** > **[Address Generator](https://console.intl.cloud.tencent.com/live/addrgenerator/addrgenerator)**, and perform the following:
   1. Select **Playback Domain** for **Domain Type**.
   2. Select a playback domain name you added in **Domain Management**.
   3. Enter the `StreamName` in the push URL to play back the corresponding stream.
   4. Select a URL expiration time, such as `2021-05-31 23:59:59`.
   5. Select a transcoding template if you want to get a playback URL for a transcoded stream. This step is not needed if you want to get a playback URL for the original stream.
   6. Click **Generate Address** to generate an LEB pull URL whose format is `webrtc://domain/path/stream_id`.
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)
3. You can use the following methods to test whether a live stream can be played back normally in different use cases:
   - **Playback test on web**: you’re advised to use [WebRTC Live Demo](https://webrtc-demo.myqcloud.com/pull-sdk/index.html) to test playback.
   - **Playback test on mobile devices**: you are advised to download and install Tencent Video Cloud Toolkit app, select **Mobile Live Video Broadcasting** > **LEB Playback**, enter the playback URL into the address box manually or by scanning the QR code, and tap the play icon in the bottom-left corner.
>? To push/play back a stream on an app, you can integrate the [MLVB SDK](https://intl.cloud.tencent.com/zh/document/product/1071) into the app to supplement the CSS service. If you encounter any problems, please see [FAQs](#que).

## Step 5. Start to use LEB
- **LEB solution for mobile devices**: supports B-frame decoding and AAC audio codec. This solution is integrated into the MLVB SDK. For how to use it, please see LEB Pull.
- **LEB solution for web**: the solution is integrated into the TCPlayerLite player. For how to use it, please see Web (H5) Player.

[](id:que)
## FAQs
[](id:play_url)
### Generate pull URL
The format of LEB pull URL is the same as that of LVB pull URL except that the former starts with `rtmp` while the latter starts with `webrtc`. 

LEB pull URL format: `webrtc://domain/path/stream_id` or `webrtc://domain/path/stream_id?txSecret=xxx&txTime=xxx` ([hotlink protection](https://intl.cloud.tencent.com/document/product/267/31560) enabled). For how to generate a pull URL, please see [Get playback URL](#step4).

>? You can also pull transcoded streams of different resolutions and bitrates. For information about generating playback URLs for transcoded streams, please see [Live Remuxing and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).

[](id:b_frame)
### B-frames
LEB solution for web **does not support decoding and playing back B-frames**. If the original stream contains B-frames, the backend will remove them by transcoding, which will result in latency and **incur transcoding fees**. We recommend not pushing streams with B-frames. You can also adjust the video codec parameter on push client software (such as OBS) to remove B-frames. If you use OBS for push, you can set to disable B-frames, as shown below:
![](C:\Users\v_vqyuyang\AppData\Roaming\Typora\typora-user-images\image-20210701111645219.png)

[](id:a_transcoding)
### Audio transcoding
Pull by web browser only supports standard WebRTC protocol and does not support AAC audio codec. If you push streams with audios in AAC format, the audios will be transcoded into Opus format, which will incur [audio transcoding fees](https://intl.cloud.tencent.com/document/product/267/39604).