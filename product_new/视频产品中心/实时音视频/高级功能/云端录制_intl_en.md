To cater to users' needs for recording in scenarios such as evidence collection, quality inspection, audit, and archiving, TRTC offers the on-cloud recording feature based on [LVB](https://intl.cloud.tencent.com/document/product/267). You can obtain the recorded files on the [VOD](https://intl.cloud.tencent.com/document/product/266) platform.

![](https://main.qcloudimg.com/raw/9768ef2cb4f6df10be8c654c0a9c8f4d.gif)

>?
>- The on-cloud recording feature is disabled by default. To enable it, you need to activate [LVB](https://console.cloud.tencent.com/live) and [VOD](https://console.cloud.tencent.com/vod) services.
>- Using Cloud Recording involves a recording fee for LVB and storage fee for VOD. If you play or download the recorded video files, you will be charged the data usage fee (video acceleration) for VOD. For more information on the billing rules, please see [On-Cloud Recording Billing](https://intl.cloud.tencent.com/document/product/647/34614#.E4.BA.91.E7.AB.AF.E5.BD.95.E5.88.B6.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8). 

## Supported Platforms

| iOS | Android | Mac OS | Windows | WeChat Mini Program | Chrome |
| :------: | :------: | :------: | :------: | :--------: | :----------: |
| &#10003; | &#10003; | &#10003; | &#10003; |  &#10003;  |   &#10003;   |

## Enabling On-Cloud Recording

1. Activate both the [LVB](https://console.cloud.tencent.com/live) and [VOD](https://console.cloud.tencent.com/vod) services.
2. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc) to enter the **Application Management** page, and enable **Relayed Live Streaming**. If **Relayed Live Streaming** is disabled, click **Feature Configuration** on the right of the application list to enable it in the configuration page.
3. On the **Application Management** page, click **Global On-Cloud Recording Configuration** to enable **Global On-Cloud Auto-Recording** and set the format of recorded files.
   ![](https://main.qcloudimg.com/raw/d12676d282b1890dd39cd2de743dda7d.png)
    After global on-cloud auto-recording is enabled, all videos recorded automatically by the TRTC applications under the current Tencent Cloud account are stored in the format you configured.

## Mixing Streams

MixTranscoding is disabled by default in a TRTC room. After on-cloud recording is enabled, only upstream videos of individual streams (mainstream and substream) are recorded by default in the TRTC room. To record a mixed video stream, enable [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) by calling the `setMixTranscodingConfig` API of TRTCCloud to mixing multiple streams into one and record it into a single file.

## Obtaining Video Files


### Option 1: Searching on Console

Locate the recorded video files on the [Video Management](https://console.cloud.tencent.com/vod/media) page of the VOD Console. Taking the [Demo](https://intl.cloud.tencent.com/document/product/647/35076) as an example, locate a recorded file by following the steps below:

1. Find the LVB bizid 3891 of the Demo account by logging in to the [TRTC Console](https://console.cloud.tencent.com/rav) and then clicking **Application Management** -> **Application Info** -> **Relayed Live Streaming Info**.
2. Create a TRTC room using the Demo with ID `12345` and user name `userA`. The live stream ID for the room is `MD5(12345_userA_main)` (calculated as `3891_8d0261436c375bb0dea901d86d7d70e8`). 
3. Exit the room, and find the file on the [Video Management](https://console.cloud.tencent.com/vod/media) page of the VOD Console or using the prefix of the live stream ID, as shown below:
   ![](https://main.qcloudimg.com/raw/c3a528e622bea92da8aa1f58ca7d57cc.png)



### Option 2: Searching via REST API

Call the REST API [SearchMedia API](https://intl.cloud.tencent.com/document/product/266/34179) provided by the VOD service and specify its StreamId parameter to search for the recorded file. 
