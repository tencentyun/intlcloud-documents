After creating an application, you can enable [relay to CDN](#bypass), [on-cloud recording](#record), and [advanced permission control](#purview) for the application in **Function Configuration**. The configuration takes effect in about 5 minutes.

[](id:bypass)
## Relay to CDN

### Notes

- Relay to CDN is the process of TRTC converting UDP-based audio/video streams and pushing them to the [CSS](https://intl.cloud.tencent.com/document/product/267) system.
- Relay to CDN is disabled by default. To enable it, you need to activate CSS first.
- Using the relay to CDN feature to implement CDN relayed live streaming incurs fees from CSS based on the amount of downstream traffic or bandwidth used. For details, see [Bill-by-Traffic/Bandwidth](https://intl.cloud.tencent.com/document/product/267/2818).
- Using the relay to CDN feature to implement [on-cloud recording](https://intl.cloud.tencent.com/document/product/647/35426) will incur recording and storage fees. For details, see [On-Cloud Recording and Playback > Billing](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8).
- If you have bound recording, transcoding, screencapturing & porn detection, or watermarking templates to a relay address (`xxxx.livepush.myqcloud.com`) in the [CSS console](https://console.cloud.tencent.com/live/domainmanage), you will be charged [additional fees](https://intl.cloud.tencent.com/document/product/267/2819).

[](id:open_bypass)
### Enabling relay to CDN
1. Log in to the TRTC console and select [Application Management](https://console.cloud.tencent.com/trtc/app) on the left sidebar.
2. Click **Function Configuration** for the application whose configuration you want to modify.
 ![](https://main.qcloudimg.com/raw/f302931ec709c205bd6c4e2378cd14b3.png)
3. In the **Relay to CDN** area, toggle on **Enable relay to CDN**.
![](https://qcloudimg.tencent-cloud.cn/raw/ee063851a4b9cc6d391552ac3602a685.png)
4. In the dialog box that pops up, **read the risk statement carefully**. If you are sure you want to enable the feature, select the box and click **Enable relay to CDN**.
![](https://qcloudimg.tencent-cloud.cn/raw/f964548ce95c678e72a657e8ee69ac00.png)

[](id:select)
### Choosing the relay mode
After [enabling relay to CDN](#open_bypass), you can choose the relay mode that fits your needs.
![](https://qcloudimg.tencent-cloud.cn/raw/d9d7e36228a8a163b7700d0830af6671.png)

- **Specified-stream relay**: After selecting this mode, if you do not need the On-Cloud MixTranscoding service, call the client-side SDK API [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7cbe48ea2cd3fb05a5b10350b6d81265) to start relayed push; if you need the service, do as instructed in the "On-Cloud MixTranscoding" document to start relay automatically after On-Cloud MixTranscoding.
- **Global relay**: After you select this mode, all upstream audio/video streams of TRTC are automatically pushed to the CSS system.


[](id:close__bypass)
### Disabling relay to CDN
To disable relayed push, follow these steps:
1. Select [Application Management](https://console.cloud.tencent.com/trtc/app) on the left sidebar, and click **Function Configuration** for the application whose configuration you want to modify.
2. In the **Relay to CDN** area, toggle off **Enable relay to CDN**.
![](https://qcloudimg.tencent-cloud.cn/raw/3583a5bf087294810c6898d6a6baeff9.png)
3. In the dialog box that pops up, **read the risk statement carefully**; if you are sure you want to disable the feature, click **Disable relay to CDN**.
![](https://qcloudimg.tencent-cloud.cn/raw/80d988936617936ff82ce23207f93bd0.png)


[](id:record)
## On-Cloud Recording

### Notes
- On-cloud recording relies on the relay to CDN feature and leverages the capabilities of [CSS](https://intl.cloud.tencent.com/document/product/267). Recording files are saved in [VOD](https://intl.cloud.tencent.com/document/product/266).
- The recording feature is provided by CSS and is charged according to the peak number of concurrent recording channels during each month. For details, see [CSS > CSS Recording Billing](https://intl.cloud.tencent.com/document/product/267/39605).
- Recording files are stored in VOD, and fees are based on the amount of storage space used. For details, see [VOD > Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/266/14666).
- If you play or download a recording file, a traffic (video acceleration) fee is charged based on the amount of downstream traffic accelerated. For details, see [VOD > Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/266/14666).
- On-cloud recording is disabled by default. To enable the feature, you need to activate CSS and VOD first.
- To enable on-cloud recording, you need to enable [relay to CDN](#open_bypass) first.


[](id:open_record)
### Enabling on-cloud recording
The on-cloud recording feature of TRTC allows you to record the audio/video streams of each user as separate files. To enable the feature, follow the steps in [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426#open).

[](id:change_record)
### Modifying on-cloud recording configuration
>! Modifying the on-cloud recording configuration may affect your active business. Make sure you understand the risks before the modification.

1. Select [Application Management](https://console.cloud.tencent.com/trtc/app) on the left sidebar, and click **Function Configuration** for the application whose configuration you want to modify.
2. In **On-Cloud Recording Configuration**, click **Edit** to go to the edit page.
![](https://main.qcloudimg.com/raw/1c46c6d6f7d87928536ab576975cdcd3.png)
3. Modify the [configuration information](https://intl.cloud.tencent.com/document/product/647/35426#recordType) as needed, and click **Confirm** to save the modification.


[](id:close_record)
### Disabling on-cloud recording
After you disable on-cloud recording, you will not be able to manually or automatically record streams on the cloud. Please make sure you no longer need the feature before disabling it.

1. Select [Application Management](https://console.cloud.tencent.com/trtc/app) on the left sidebar, and click **Function Configuration** for the application whose configuration you want to modify.
2. In the **On-Cloud Recording Configuration** area, toggle on **Enable On-Cloud Recording**.
![](https://main.qcloudimg.com/raw/72893310f197830b468292b9d0062458.png)
3. If you are sure about disabling the feature after reading the risks, click **Disable On-Cloud Recording**.
![](https://main.qcloudimg.com/raw/b1a41cf54dad0c5cd48f65d2a250e56d.png)



[](id:purview)
## Advanced Permission Control
[Advanced permission control](https://intl.cloud.tencent.com/document/product/647/35157) lets you control which users have permission to enter rooms and turn on their mic without needing to configure permissions on the client, which helps to keep the service protected against attacks and cracking.
![](https://main.qcloudimg.com/raw/78882ea4eac56c347c89a4e8113d706a.png)


### Notes
After you enable advanced permission control for an application (`SDKAppID`), all users using the application must pass the correct `privateMapKey` in `TRTCParams` to enter a room. Therefore, you are not advised to enable the feature for an application if you have users using it.


### Enabling advanced permission control
1. Select **Application Management** on the left sidebar and click **Function Configuration** for the application for which you want to enable advanced permission control.
2. In the **Advanced Permission Control** area, toggle on **Enable**.
![](https://main.qcloudimg.com/raw/d5de4b300cf71969244239d821414db6.png)

### Disabling advanced permission control
1. Select **Application Management** on the left sidebar and click **Function Configuration** for the application for which you want to disable advanced permission control.
2. In the **Advanced Permission Control** area, toggle off **Enable**.
![](https://qcloudimg.tencent-cloud.cn/raw/b05dfb7bb910e39cd77257cc838ad5e3.png)

## Relevant Documentation
- To create an application, see [Creating an Application](https://intl.cloud.tencent.com/document/product/647/39077).
- To search for an application in the application list, see [Searching for Applications](https://intl.cloud.tencent.com/document/product/647/39078).
- To view the basic information of an application, see [Application Info](https://intl.cloud.tencent.com/document/product/647/39079).
- If you want to set an image as the background displayed during on-cloud stream mixing, you can add the image in **Material Management**. 
- To get the demo source code to help you get started quickly, see [Quick Start](https://intl.cloud.tencent.com/document/product/647/39082).



