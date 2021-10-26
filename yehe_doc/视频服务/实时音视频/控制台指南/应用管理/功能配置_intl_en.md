After creating an application, you can enable [relayed push](#bypass), [on-cloud recording](#record), and [advanced permission control](#purview) for it in **Function Configuration**. The configuration takes effect in about 5 minutes.

[](id:bypass)

## Relayed Push

### Notes

- The process of TRTC converting UDP-based audio/video streams and pushing them to the [CSS](https://intl.cloud.tencent.com/document/product/267) system is known as “relayed push”.
- Relayed push is disabled by default. To enable the feature, you need to activate the CSS service first.
- If you use relayed push to implement [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242), CSS will charge you based on the downstream traffic generated or bandwidth used. For details, see [CSS > Bill-by-Traffic/Bandwidth](https://intl.cloud.tencent.com/document/product/267/2818).
- If you use relayed push for [on-cloud recording](https://intl.cloud.tencent.com/document/product/647/35426), you will be charged for recording streams and storing the recording files. For details, see [On-Cloud Recording and Playback > Billing](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8).
- If you bind templates of paid features such as recording, transcoding, screencapturing & porn detection, and watermarking to the domain name (`xxxx.livepush.myqcloud.com`) used for relayed push in the [CSS console](https://console.cloud.tencent.com/live/domainmanage), you will be charged [value-added fees](https://intl.cloud.tencent.com/document/product/267/2819).

[](id:open_bypass)
### Enabling relayed push
1. Log in to the TRTC console and click **[Application Management](https://console.cloud.tencent.com/trtc/app)**.
2. Click **Function Configuration** for the application whose configuration you want to modify.
 ![](https://main.qcloudimg.com/raw/f302931ec709c205bd6c4e2378cd14b3.png)
3. In **Relayed Push Configuration**, click the button next to **Enable Relayed Push**.
![](https://main.qcloudimg.com/raw/19050dd982abfe75080843148f3abbc4.png)
4. In the dialog box that pops up, **read the risk statement carefully**; if you are sure you want to enable the feature, check the box and click **Enable Relayed Push**.
![](https://main.qcloudimg.com/raw/0c81b0ef96e7e07f9fba0d7f8827c7f8.png)

[](id:select)
### Choosing relayed push mode
After [enabling relayed push](#open_bypass), you can choose the relayed push mode that fits your needs.
![](https://main.qcloudimg.com/raw/98b5a33c06846dc755a1e1b6a2853048.png)

- **Specified stream for relayed push**: After selecting this mode, if you do not need the On-Cloud MixTranscoding service, call the client-side SDK API [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a7cbe48ea2cd3fb05a5b10350b6d81265) to start relayed push; if you need the service, follow the steps in [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618), and relayed push will start automatically after On-Cloud MixTranscoding.
- **Global auto-relayed push**: After you select this mode, all upstream audio/video streams of TRTC are automatically pushed to the CSS system.


[](id:close__bypass)
### Disabling relayed push
To disable relayed push, follow these steps:
1. Click **[Application Management](https://console.cloud.tencent.com/trtc/app)**, and click **Function Configuration** for the application whose configuration you want to modify.
2. In **Relayed Push Configuration**, click the button next to **Enable Relayed Push**.
![](https://main.qcloudimg.com/raw/8abcab1e53ca628b274576c597e6fcb6.png)
3. In the dialog box that pops up, **read the risk statement carefully**; if you are sure you want to disable the feature, check the box and click **Disable Relayed Push**.
![](https://main.qcloudimg.com/raw/42501fc7a48d9384fa271280fad9fb50.png)


[](id:record)
## On-Cloud Recording

### Notes
- The relayed push feature of TRTC leverages the on-cloud recording capability of [CSS](https://intl.cloud.tencent.com/document/product/267) to record entire live streaming sessions and store the recording files in [VOD](https://intl.cloud.tencent.com/document/product/266).
- The recording feature is based on CSS, which charges you by the peak number of concurrent recording channels in a month. For details, see [CSS > CSS Recording Billing](https://intl.cloud.tencent.com/document/product/267/39605).
- Recording files are stored in VOD, which charges you based on the storage space used. For details, see [VOD > Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/266/14666).
- If you play or download a recording file, you will be charged a traffic (video acceleration) fee based on the amount of downstream traffic accelerated. For details, see [VOD > Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/266/14666).
- On-cloud recording is disabled by default. To enable the feature, you need to activate CSS and VOD first.
- On-cloud recording relies on [relayed push](#open_bypass), which you need to enable first.


[](id:open_record)
### Enabling on-cloud recording
The on-cloud recording feature of TRTC allows you to record the audio/video streams of each user as a separate file. To enable the feature, follow the steps in [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426#open).

[](id:change_record)
### Modifying on-cloud recording configuration
>! Modifying on-cloud recording configuration may affect your active business. Make sure you understand the risks before the modification.

1. Click **[Application Management](https://console.cloud.tencent.com/trtc/app)**, and click **Function Configuration** for the application whose configuration you want to modify.
2. In **On-Cloud Recording Configuration**, click **Edit** to go to the edit page.
![](https://main.qcloudimg.com/raw/1c46c6d6f7d87928536ab576975cdcd3.png)
3. Modify the [configuration information](https://intl.cloud.tencent.com/document/product/647/35426#recordType) as needed, and click **Confirm** to save the modification.


[](id:close_record)
### Disabling on-cloud recording
After you disable on-cloud recording, your active business will be unable to record streams on the cloud, whether manually or automatically. Please make sure that your business no longer needs the feature before disabling it.

1. Click **[Application Management](https://console.cloud.tencent.com/trtc/app)**, and click **Function Configuration** for the application whose configuration you want to modify.
2. In **On-Cloud Recording Configuration**, click the button next to **Enable On-Cloud Recording**.
![](https://main.qcloudimg.com/raw/72893310f197830b468292b9d0062458.png)
3. If you are sure about disabling the feature after reading the risks, click **Disable On-Cloud Recording**.
![](https://main.qcloudimg.com/raw/b1a41cf54dad0c5cd48f65d2a250e56d.png)



[](id:purview)
## Advanced Permission Control
You may consider [enabling advanced permission control](https://intl.cloud.tencent.com/document/product/647/35157) if you want to control room entry and mic-on permissions (i.e., allowing only specific users to enter a room or use their mics), but are worried that giving permissions on the client makes the service vulnerable to attacks and cracking.
![](https://main.qcloudimg.com/raw/78882ea4eac56c347c89a4e8113d706a.png)


### Notes
After you enable advanced permission control for an SDKAppID, all users using the SDKAppID must pass the correct `privateMapKey` in `TRTCParams` to enter a room. Therefore, you are not advised to enable the feature if a user is using the SDKAppID.


### Enabling advanced permission control
1. Click **Application Management**, select the application for which you want to enable advanced permission control, and click **Function Configuration**.
2. In **Function Configuration** > **Advanced Permission Control**, click the button next to **Enable**.
![](https://main.qcloudimg.com/raw/d5de4b300cf71969244239d821414db6.png)

### Disabling advanced permission control
1. Click **Application Management**, select the application for which you want to disable advanced permission control, and click **Function Configuration**.
2. In **Function Configuration** > **Advanced Permission Control**, click the button next to **Enable**.
![](https://main.qcloudimg.com/raw/b1a41cf54dad0c5cd48f65d2a250e56d.png)

## Documentation
- To create an application, see [Creating Application](https://intl.cloud.tencent.com/document/product/647/39077).
- To search for an application in the application list, see [Searching Application](https://intl.cloud.tencent.com/document/product/647/39078).
- To view the basic information of an application, see [Application Info](https://intl.cloud.tencent.com/document/product/647/39079).
- If you want to set an image as the background displayed during on-cloud stream mixing, you can add the image in **Material Management**. For details, see [Material Management](https://intl.cloud.tencent.com/document/product/647/39081).
- To get the demo source code for a quick start, see [Quick Start](https://intl.cloud.tencent.com/document/product/647/39082).



