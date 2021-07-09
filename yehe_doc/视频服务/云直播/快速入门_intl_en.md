This document describes how to get started with LVB. Before trying out LVB, you’re advised to read the [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819) of CSS to get familiar with its **billable items** and **prices**.

<span id="step0"></span>

## Preparations

1. Sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629). Unverified users cannot purchase CSS instances in the Chinese mainland.
2. Go to the [CSS service activation page](https://console.cloud.tencent.com/live?from=product-banner-use-lvb), indicate your consent to the “Tencent Cloud Service Terms”, and click **Apply for Activation** to activate the CSS service.

<span id="step1"></span>

## Step 1. Add domain names

To use CSS, you should have at least one **push domain name**, and one **playback domain name**. You cannot use one domain name for both push and playback.

<span id="step1_1"></span>

1. Prepare your own domain names. For domain names in Chinese mainland regions, ICP filing is required.

   

2. Log in to the CSS console, enter **[Domain Management](https://console.intl.cloud.tencent.com/live/domainmanage)**, and click **Add Domain**.

3. On the domain name adding page, enter your domain name, select the domain name type, and click **Confirm**.
   ![](https://main.qcloudimg.com/raw/bee8085a9d29641ddab913fdcd9c75ab.png)

>?
>
>- CSS provides a test domain name `xxxx.livepush.myqcloud.com`. You can use it to test live push, but you’re not advised to use it as the push domain name for business purposes.
>- After the domain name is added successfully, you can view its information in the domain name list in **Domain Management**. For how to manage it, please see [Domain Management](https://intl.cloud.tencent.com/document/product/267/31056).
>- For more information on live streaming domain names, please see [Basic CSS Features](https://intl.cloud.tencent.com/document/product/267/7968).
>  <span id="step1_1_1"></span>

4. Once your domain name is added, the system will assign it a CNAME domain name (suffixed with `.tlivecdn.com` or `.tlivepush.com`), which cannot be accessed before you complete the CNAME configuration at your DNS service provider. After the CNAME configuration takes effect, you can use CSS. The following example shows you how to add a CNAME record by assuming Tencent Cloud is your DNS service provider:
   1. Log in to the [Tencent Cloud Domain Name Service console](https://console.cloud.tencent.com/domain).
   2. Find the target domain name, and click **Resolve**.
   3. On the domain name resolution page, click **Add Record**.
   4. In the new line, enter the domain name prefix as the host record, select CNAME as the record type, and enter the CNAME domain name as the record value.
   5. Click **Save**.

>!
>
>- After a CNAME record is successfully added, it takes some time for the CNAME configuration to take effect. If the configuration fails, you cannot use CSS.
>- After the CNAME configuration succeeds, you can see that the CNAME status has changed to ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png) in **[Domain Management](https://console.intl.cloud.tencent.com/live/domainmanage)** of the CSS console.
>- If the CNAME configuration failure persists, consult your DNS service provider.
>- For more information on how to configure with other DNS service providers, please see [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).

<span id="step2"></span>

## Step 2. Get push URL

1. Select **CSS Toolkit** > **[Address Generator](https://console.intl.cloud.tencent.com/live/addrgenerator/addrgenerator)**.
2. On the **Address Generator** page, configure as follows:
   1. Select **Push Domain** for **Domain Type**.
   2. Select the push domain name you added in **Domain Management**.
   3. Enter an **AppName**. It is `live` by default.
   4. Enter a custom `StreamName`, such as `liveteststream`.
   5. Select the URL expiration time, such as `2021-05-31 23:59:59`.
   6. Click **Generate Address** to generate a push URL.
      ![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)

>? 
>
>- In the push URL, `live` is the default `AppName`, `txSecret` is the signature for playing back the stream, and `txTime` is the URL expiration time.
>- In addition to the above method, you can also find the push domain name in **[Domain Management](https://console.intl.cloud.tencent.com/live/domainmanage)** of the CSS console, click **Manage**, and select **Push Configuration**. In the **Push Address Generator** section, enter a push URL expiration time and a custom `StreamName`, and then click **Generate Push Address** to generate a push URL.
>- You can create and configure a desired [feature template](https://intl.cloud.tencent.com/document/product/267/34223) before generating the push URL based on your business needs and bind it to the push domain name. For prices of CSS value-added features, please see [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819).

<span id="step3"></span>

## Step 3. Push live stream

You can enter the generated push URL into the push software as appropriate for your use cases.

- For push on PCs, you’re advised to use OBS. For detailed directions, please see [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).
- For push on web, you’re advised to use **[Web Push](https://console.intl.cloud.tencent.com/live/tools/webpush)**: select a push domain name, enter a custom `StreamName`, select a URL expiration time, turn the camera on, and click **Start Push**.
- For push on mobile devices, download and install Tencent Video Cloud Demo, open it, select **Mobile Live Video Broadcasting** > **Push (Camera)**, enter the push URL into the address box manually or by scanning the QR code, and then tap the start icon in the bottom-left corner.

>? You can integrate Tencent Cloud [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071) into customized apps for live push.

<span id="step4"></span>

## Step 4. Get playback URL

1. After the push succeeds, select **[Stream Management](https://console.intl.cloud.tencent.com/live/streammanage)** > **Live Streams**, view the status of the target stream, and click **Test** to play back it.
2. Select **CSS Toolkit** > **[Address Generator](https://console.intl.cloud.tencent.com/live/addrgenerator/addrgenerator)**, and perform the following:
   1. Select **Playback Domain** for **Domain Type**.
   2. Select a playback domain name you added in **Domain Management**.
   3. Enter an **AppName**. It is `live` by default.
   4. Enter the `StreamName` in the push URL to play back the corresponding stream.
   5. Select a URL expiration time, such as `2021-05-31 23:59:59`.
   6. To generate a playback URL for a transcoded stream, please select a transcoding template which must be bound to the domain name in the playback URL. For directions on how to bind a transcoding template, please see [Live Transcoding > Binding Domain Name](https://intl.cloud.tencent.com/document/product/267/31071).
   7. Click **Generate Address** to generate a playback URL.
      ![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
      <span id="step4_1"></span>
3. You can use the following methods to test whether a live stream can be played back normally in different use cases:
   1. For playback test on PCs, you are advised to use tools such as [VLC](https://intl.cloud.tencent.com/document/product/267/32483). For more information, please see [Live Playback](https://intl.cloud.tencent.com/document/product/267/31559).
   2. For playback test on web, you are advised to use the TCPlayerLite player in the Player SDK. For more information, please see [Live Playback](https://intl.cloud.tencent.com/document/product/267/31559).
   3. For playback test on mobile devices, you are advised to download and install Tencent Video Cloud Toolkit App, select **Mobile Live Video Broadcasting** > **LVB Playback**, enter the playback URL into the address box manually or by scanning the QR code, and tap the play icon in the bottom-left corner.

>? To push/play back a stream on an app, you can integrate the [MLVB SDK](https://intl.cloud.tencent.com/) into the app to supplement the CSS service. If you encounter any problem during the trial period, please see [FAQs](https://intl.cloud.tencent.com/document/product/267/7968).

## Operations

- To enable **live recording**, please create a recording template and bind it to a domain name first. For more information, please see [Creating Recording Template](https://intl.cloud.tencent.com/document/product/267/34223).
- To enable **live transcoding**, please create a transcoding template and bind it to a domain name first. For more information, please see [Creating Transcoding Template](https://intl.cloud.tencent.com/document/product/267/31071).
- To enable **live watermarking**, please create a watermark template and bind it to a domain name first. For more information, please see [Creating Recording Template](https://intl.cloud.tencent.com/document/product/267/31073).
- To enable **live screencapture and porn detection**, please create a screencapture and porn detection template and bind it to a domain name first. For more information, please see [Creating Screencapture and Porn Detection Template](https://intl.cloud.tencent.com/document/product/267/31072).
- To enable **live stream mixing**, please call the stream mixing API [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997).


## FAQs

- [What are the differences between push, live streaming, and video on demand?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.8E.A8.E6.B5.81.E3.80.81.E7.9B.B4.E6.92.AD.E5.92.8C.E7.82.B9.E6.92.AD.E5.88.86.E5.88.AB.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
- [What push protocols are supported?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.8E.A8.E6.B5.81.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [What playback protocols are supported?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.92.AD.E6.94.BE.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [What does a playback address consist of?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.92.AD.E6.94.BE.E5.9C.B0.E5.9D.80.E7.94.B1.E4.BB.80.E4.B9.88.E7.BB.84.E6.88.90.EF.BC.9F)
- [How do I splice multiple live stream URLs?](https://intl.cloud.tencent.com/document/product/267/38393)
