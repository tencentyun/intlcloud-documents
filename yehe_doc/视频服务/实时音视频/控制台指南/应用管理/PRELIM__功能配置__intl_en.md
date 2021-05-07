After creating an application, you can enable [relayed push](#bypass), [on-cloud recording](#record) and [advanced permission control] for it in **Function Configuration**. The configuration takes effect in about 5 minutes.

[](id:bypass)

## Relayed Push

### Note

- The process of TRTC converting UDP-based audio/video streams and pushing them to the [CSS](https://intl.cloud.tencent.com/document/product/267) system is known as “relayed push”.
- Relayed push is disabled by default. To enable the feature, you need to activate the CSS service first.
- If you use relayed push to implement [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242), CSS will charge you based on the downstream traffic generated or bandwidth used. For details, see [CSS > Bill-by-Traffic/Bandwidth](https://intl.cloud.tencent.com/document/product/267/2818).
- If you use relayed push for [on-cloud recording](https://intl.cloud.tencent.com/document/product/647/35426), you will be charged for recording streams and storing the recording files. For details, see [On-Cloud Recording and Playback > Applicable Fees](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8).
- If you bind templates of paid features such as recording, transcoding, screencapturing & porn detection, and watermarking to the domain name (`xxxx.livepush.myqcloud.com`) used by relayed push in the [CSS console](https://console.cloud.tencent.com/live/domainmanage), you will be charged [value-added fees](https://intl.cloud.tencent.com/document/product/267/2819).

[](id:open_bypass)

### Enabling relayed push
1. Log in to the TRTC console and click **[Application Management](https://console.cloud.tencent.com/trtc/app)**.
2. Select the application whose configuration you want to modify, and click **Function Configuration**.
 ![](https://main.qcloudimg.com/raw/e5b5b5494f2c75a7ea7a48caae32f256.png)
3. In **Relayed Push Configuration**, click the button next to **Enable Relayed Push**.
![](https://main.qcloudimg.com/raw/b9846f4a7f5ce1e39b3450963e872c90.png)
4. In the dialog box that pops up, **read the risk statement carefully**; if you are sure you want to enable the feature, click **Enable Relayed Push**.
![](https://main.qcloudimg.com/raw/d39ff108d2f200cc92a78b42359bff6e.png)

[](id:select)
### Choosing relayed push mode
After [enabling relayed push](#open_bypass), you can choose the push mode that fits your needs.
![](https://main.qcloudimg.com/raw/3fd6fbe8c5837a6d7f78a19f079b477a.png)

- **Specified stream for relayed push**: after selecting this mode, if you do not need the On-Cloud MixTranscoding service, call the client-side SDK API [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) to start relayed push; if you need the service, follow the steps in [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618), and relayed push will start automatically after On-Cloud MixTranscoding.
- **Global auto-relayed push**: after this mode is selected, all upstream audio/video streams of TRTC are automatically pushed to the CSS system.


[](id:close__bypass)
### Disabling relayed push
To disable relayed push, follow these steps:
1. Click **[Application Management](https://console.cloud.tencent.com/trtc/app), select the application whose configuration you want to modify, and click **Function Configuration**.
2. In **Relayed Push Configuration**, click the button next to **Enable Relayed Push**.
![](https://main.qcloudimg.com/raw/0ac618f3fb643a3d5fd1ff11566eef31.png)
3. In the dialog box that pops up, **read the risk statement carefully**; if you are sure you want to disable the feature, click **Disable Relayed Push**.
![](https://main.qcloudimg.com/raw/1306f736ff0b5337f468325cabdfee54.png)


[](id:record)
## On-Cloud Recording

### Note
- The relayed push feature of TRTC allows you to leverage the on-cloud recording capability of CSS](https://intl.cloud.tencent.com/document/product/267) to record entire live streaming sessions and store the recording files in [VOD](https://intl.cloud.tencent.com/zh/document/product/266).
- The recording feature is based on CSS, which charges you by the peak number of concurrent recording channels in a month. For details, see [CSS > CSS Recording Billing](https://intl.cloud.tencent.com/document/product/267/39605).
- Recording files are stored in VOD, which charges you based on the storage space used. For details, see [VOD > Pay-as-You-Go ](https://intl.cloud.tencent.com/document/product/266/14666), or [VOD > Billing of Video Storage Package](https://cloud.tencent.com/document/product/266/14667#storage_page).
- On-cloud recording is disabled by default. To enable the feature, you need to activate CSS and VOD first.
- On-cloud recording relies on [relayed push](#open_bypass), which you need to enable first.


[](id:open_record)
### Enabling on-cloud recording
The on-cloud recording feature of TRTC allows you to record the audio/video streams of each user into a separate file. To enable the feature, follow the steps in [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426#open).

[](id:change_record)
### Modifying on-cloud recording configuration
>! Modifying on-cloud recording configuration may affect your active business. Make sure you understand the risks before modification.

1. Click **[Application Management](https://console.cloud.tencent.com/trtc/app), select the application whose configuration you want to modify, and click **Function Configuration**.
2. In **On-Cloud Recording Configuration**, click **Edit** to go to the edit page.
![](https://main.qcloudimg.com/raw/1e0ac1e9704a5901466ad6ec3ccac89b.png)
3. Modify the [configuration](https://intl.cloud.tencent.com/document/product/647/35426#recordType) as needed, and click **Confirm** to save the modification.


[](id:close_record)
### Disabling on-cloud recording
After you disable on-cloud recording, your active businesses will be unable to record streams in the cloud, whether manually or automatically. Please make sure that your businesses no longer need the feature before disabling.

1. Click **[Application Management](https://console.cloud.tencent.com/trtc/app), select the application whose configuration you want to modify, and click **Function Configuration**.
2. In **On-Cloud Recording Configuration**, click the button next to **Enable On-Cloud Recording**.
![](https://main.qcloudimg.com/raw/93761fae36103906ddbd4e134460be0a.png)
3. If you are sure about disabling the feature after reading the consequences, click **Disable On-Cloud Recording**.
![](https://main.qcloudimg.com/raw/3202cb938030085babc0210283ce9221.png)



[](id:purview)
## Advanced Permission Control
You may consider [enabling advanced permission control](https://intl.cloud.tencent.com/document/product/647/35157) if you want to practice room access and mic-on controls (i.e., allowing only specific users to enter a room and use their mics), but are worried that giving permissions on the client end makes your account vulnerable to attacks and cracking.
![](https://main.qcloudimg.com/raw/8fd4b0d09aeea46a15714c59e5e0419e.png)


### Note
After you enable advanced permission control for an `SDKAppID`, all users using the `SDKAppID` must pass the correct `privateMapKey` in `TRTCParams` to enter a room. Therefore, you are not advised to enable the feature if you have active users using an `SDKAppID`.


### Enabling advanced permission control
1. Click **Application Management**, select the application for which you want to enable advanced permission control, and click **Function Configuration**.
2. In **Function Configuration** > **Advanced Permission Control**, click the button next to *Enable*.
![](https://main.qcloudimg.com/raw/196e32293f8f5c159a3513cbf4b9723a.png)

### Disabling advanced permission control
1. Click **Application Management**, select the application for which you want to disable advanced permission control, and click **Function Configuration**.
2. In **Function Configuration** > **Advanced Permission Control**, click the button next to *Disable*.
![](https://main.qcloudimg.com/raw/b7015cb446cd022d591fda7e22689e44.png)

## Documentation
- To create an application, see [Creating Application](https://intl.cloud.tencent.com/document/product/647/39077).
- To search an application in the application list, see [Searching Application](https://intl.cloud.tencent.com/document/product/647/39078).
- To view the basic information of an application, see [Application Info](https://intl.cloud.tencent.com/document/product/647/39079).
- If you want to set an image as the background displayed during on-cloud stream mixing, you can add the image in **Material Management**. For details, see [Material Management](https://intl.cloud.tencent.com/document/product/647/39081).
- To get the demo source code for a quick start, see [Quick Start](https://intl.cloud.tencent.com/document/product/647/39082).



