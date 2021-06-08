This document describes how to get started with CSS. Before trying out CSS, we recommend you read the [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819) of CSS to get familiar with the **billable items** and **prices** and avoid confusions.

<span id="step0"></span>
## Preparations

1. Sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629). Unverified users cannot buy instances in Chinese mainland.
2. Go to the [CSS service activation page](https://console.cloud.tencent.com/live?from=product-banner-use-lvb), indicate your consent to the **Tencent Cloud Service Agreement**, and click **Apply for Activation** to activate the CSS service.

<span id="step1"></span>
## Step 1. Add a domain name
To use CSS, you should have at least **two** domain names, one as the **push domain name**, and the other as the **playback domain name**. Push and playback cannot use the same domain name.

<span id="step1_1"></span>
1. Prepare your own domain names. For domain names in Chinese mainland regions, ICP filing is required.
2. Log in to the CSS console, enter **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, and click **Add Domain**.
3. On the domain name adding page, enter your domain name, select the domain name type, and click **OK**.
![](https://main.qcloudimg.com/raw/bee8085a9d29641ddab913fdcd9c75ab.png)
>?
>- CSS provides a test domain name `xxxx.livepush.myqcloud.com` by default. You can use it for push testing, but we recommend you not use it as the push domain name for your real business.
>- After the domain name is added successfully, you can view its information in the domain name list in **Domain Management**. If you need to manage it, please see [Domain Name Management](https://intl.cloud.tencent.com/document/product/267/31056).
>- For more information on CSS domain names, please see [Basic CSS Features](https://intl.cloud.tencent.com/document/product/267/7968).
<span id="step1_1_1"></span>
4. Once your domain name is added, the system will automatically assign it a CNAME domain name (suffixed with `.liveplay.myqcloud.com`), which cannot be accessed directly before you complete the CNAME configuration at your domain name service provider. After the configuration takes effect, CSS can be used properly. The following uses Tencent Cloud as the DNS service provider as an example to describe how to add a CNAME record:
	1. Log in to the [Tencent Cloud Domain Name Service console](https://console.cloud.tencent.com/domain).
	2. Select the domain name for which you want to add a CNAME record and click **Resolve**.
	3. Enter the domain name resolution page and click **Add Record**.
	4. In the new column, enter the domain name prefix as the host record, select CNAME as the record type, and enter the CNAME domain name as the record value.
	5. Click **Save**.
>!
>- After a CNAME record is successfully added, it generally takes some time to take effect. If the CNAME configuration fails, you cannot use CSS.
>- After the CNAME configuration succeeds, you can see that the status symbol of the CNAME address in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the CSS console has changed to ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png).
>- If the CNAME configuration failure persists, please consult your domain name registrar.
>- For more information on how to configure with other DNS service providers, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057).


<span id="step2"></span>
## Step 2. Get a push address
1. Select **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**.
2. Enter the address generator page and configure as follows:
   1. Select **Push domain** as the type of generation.
   2. Select the push domain name you added in **Domain Management**.
   3. Enter a custom `StreamName`, such as `liveteststream`.
   4. Select the expiration time of the address, such as `2019-10-18 23:59:59`.
   5. Click **Generate Address** to generate a push address.
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)

>? 
>- The format of the push address is as follows: `live` is the default `AppName`, `txSecret` is the signature for playing back the stream, and `txTime` is the expiration time of the push address.
>- In addition to the above method, you can also select a push domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the CSS console, click **Manage**, select **Push Configuration**, enter the expiration time of the push address and the custom `StreamName`, and click **Generate Push Address** to generate a push address.
>- You can create and configure a desired [feature template](https://intl.cloud.tencent.com/document/product/267/34223) before generating the push address based on your actual business needs and bind it to the push domain name. For prices of value-added features, please see [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819).

<span id="step3"></span>
## Step 3. Push a live stream

You can enter the generated push address into the corresponding push software according to your business scenario.
- For push on PCs, we recommend you use OBS. For detailed directions, please see [OBS Push](https://intl.cloud.tencent.com/document/product/267/31569).
- For push on web, we recommend you go to **CSS Toolkit** > **[Web Push](https://console.cloud.tencent.com/live/tools/webpush)**, select the push domain name, enter the custom `StreamName`, select the address expiration time, open the camera, and click **Start Push**.
- For push on mobile devices, download and install "Tencent Video Cloud Demo", open it, select **MLVB** > **Camera Push**, enter the push address into the address box manually or by scanning the QR code, and tap **Start** in the bottom-left corner to start push.

>? Customized apps can integrate with the [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071) provided by Tencent Cloud to implement the push function.

<span id="step4"></span>
## Step 4. Get a playback address

1. After push succeeds, select **[Stream Management](https://console.cloud.tencent.com/live/streammanage)** > **Online Streams**, view the status of the push address, and click **Test** to play back the stream online.
2. Select **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** to get a playback address and configure as follows:
   1. Select **Playback domain** as the type of generation.
   2. Select the playback domain name you added in **Domain Management**.
   3. Enter the same `StreamName` as that of the push address. The `StreamName` of the playback address must be the same as that of the push address to play back the corresponding stream.
   4. Select the expiration time of the address, such as `2019-10-13 23:59:59`.
   5. Click **Generate Address** to generate a playback address.
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
<span id="step4_1"></span>
3. You can use the following methods to test whether a live stream can be played back normally based on your business scenario:
   1. For stream test on PCs, we recommend you use tools such as [VLC](https://intl.cloud.tencent.com/document/product/267/32483). For more information, please see [CSS Playback](https://intl.cloud.tencent.com/document/product/267/31559).
   2. For stream test on web, we recommend you use TCPlayerLite in the Player SDK. For more information, please see [CSS Playback](https://intl.cloud.tencent.com/document/product/267/31559).
   4. For stream test on mobile devices, we recommend you download and install Tencent Video Cloud Demo, open it, select **MLVB** > **CSS Pull**, enter the playback address into the address box manually or by scanning the QR code, and tap **Play** in the bottom-left corner to start watching.

>? If you need to push/play back a stream in an app, you can integrate the [MLVB SDK](https://intl.cloud.tencent.com/zh/product/mlvb) to use the CSS service. If you encounter any problem during the trial, please see [FAQs](https://intl.cloud.tencent.com/zh/document/product/267/7968).

## Relevant Operations
- To enable **CSS recording**, create a recording template and bind it to a domain name. For more information, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34223).
- To enable **CSS transcoding**, create a transcoding template and bind it to a domain name. For more information, please see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31071).
- To enable **CSS watermark**, create a watermark template and bind it to a domain name. For more information, please see [Watermark Configuration](https://intl.cloud.tencent.com/document/product/267/31073).
- To enable **CSS screencapture and porn detection**, create a screencapture and porn detection template and bind it to a domain name. For more information, please see [Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31072).
- To enable **CSS stream mixing**, call the stream mixing API. For more information, please see [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997).




## FAQs
- [What are the differences between push, CSS, and VOD?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.8E.A8.E6.B5.81.E3.80.81.E7.9B.B4.E6.92.AD.E5.92.8C.E7.82.B9.E6.92.AD.E5.88.86.E5.88.AB.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
- [What push protocols are supported?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.8E.A8.E6.B5.81.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [What playback protocols are supported?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.92.AD.E6.94.BE.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [What does a playback address consist of?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.92.AD.E6.94.BE.E5.9C.B0.E5.9D.80.E7.94.B1.E4.BB.80.E4.B9.88.E7.BB.84.E6.88.90.EF.BC.9F)
- [How do I splice and generate multiple CSS URLs?](https://intl.cloud.tencent.com/zh/document/product/267/38393)
