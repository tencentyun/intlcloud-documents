
## Overview

This document shows you how to encrypt videos using DRM solutions and use player to play the encrypted videos.

## Prerequisites
Before you start, do the following:

### Activate VOD
Follow the steps below to activate VOD:

1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Purchase VOD services. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838).
3. Go to the [VOD console](https://console.cloud.tencent.com/vod).

At this point, you have activated VOD. 

### Apply for a FairPlay certificate and submit the certificate information
For detailed directions, see [Applying for FairPlay Certificate and Submitting Certificate Information](https://intl.cloud.tencent.com/document/product/266/46643). After submitting the information, view and note the certificate URL in the console for later use.

## Step 1. Enable hotlink protection

The example below shows how to enable key hotlink protection for the default distribution domain under your account:
>? We do not recommend enabling hotlink protection for a domain name already in use, because it may result in playback failure.

1. Log in to the VOD console, select **Distribution and Playback** > **[Domain Name](https://console.cloud.tencent.com/vod/distribute-play/domain)**, find the default distribution domain, and click **Set** on the right.
    <img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />

2. Click **Access Control** and toggle **Key Hotlink Protection** on. In the pop-up window, click **Generate** to generate a random key (testtest). Copy the key, which is needed to generate superplayer signature, and click **Confirm** to save the configuration.

   ![image-KEY](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## Step 2. Encrypt a video

1. In the VOD console, select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**, select the target video (file ID: 387702299667618135), and click **Process Video**.

   ![image-20220426211316803](https://qcloudimg.tencent-cloud.cn/raw/4eab2858c67f4efbf1383a3b03810428.png)

2. On the video processing page:
 - Select **Task Flow** as the **Processing Type**.

 - Select **WidevineFairPlayPreset** as the **Task Flow Template**.

    ![image-20220425192205432](https://qcloudimg.tencent-cloud.cn/raw/cef2c1e79343ea9688654791b6fb6762.png)

>?
>- `WidevineFairPlayPreset` is a preset task flow. It uses the adaptive bitrate streaming template 11 or 13, the time point screenshot template 10 (for thumbnail generation), and the image sprite template 10.
>- The adaptive bitrate streaming template 11 generates multi-bitrate streams encrypted by FairPlay, and the adaptive bitrate streaming template 13 generates multi-bitrate streams encrypted by Widevine.
3. Click **Confirm** and wait until the **Video Status** changes from "Processing" to "Normal", which indicates that video processing is completed.

   <img src="https://main.qcloudimg.com/raw/885b68427d36faefe8f2bb5b489e1e19.png" width="" />

4. Click **Manage** in the **Operation** column of the video to enter the management page:
 - Click the **Basic Info** tab to view the generated thumbnail and outputs of adaptive bitrate streaming (template ID: 11/13).

   ![image-20220426201159056](https://qcloudimg.tencent-cloud.cn/raw/696e894ed0c3665990c12cc57ebf23bf.png)

 - Click the **Screenshot Info** tab to view the generated image sprite (template ID: 10).

   ![image-20220426201309975](https://qcloudimg.tencent-cloud.cn/raw/1a5878fd0286c46ef487bdf81ad8503a.png)


## Step 3. Gernaerate the superplayer signature

The superplayer signature is used to get playback information.For how to generate it, see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099). The payload of the superplayer signature is as follows:

```json
{
  "appId": 1500012416,
  "fileId": "387702299667618135",
  "currentTimeStamp": 1650886156,
  "expireTimeStamp": 1966435200,
  "urlAccessInfo": {
    "t": "75356B80",
    "us": "72d4cd1101"
  },
  "pcfg":"advanceDrmPreset"
}
```

 the key is `testtest`. The superplayer signature(`psign`) generated is as follows:

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg`

## Step 4. Get the playback information

The following example shows how to get the playback information from the URL.

The HTTP GET request method is used, and the URL is `https://playvideo.qcloud.com/getplayinfo/v4/{appId}/{fileId}?psign={psign}`.

Here, the `{appId}` attribute is the application ID (if you use a subapplication, pass in the [subapplication ID](https://intl.cloud.tencent.com/document/product/266/33987)). The `{fileId}` attribute is the ID of the media file, and the `{psign}` attribute is created in Step 3. 

The request URL is as follows:

```url
https://playvideo.qcloud.com/getplayinfo/v4/1500012416/387702299667618135?psign=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg
```

The response will be:

```json
{
  "code": 0,
  "message": "",
  "requestId": "9c7fab8704994c6b96375393e6544b5c",
  ...
  "media": {
	...
    "streamingInfo": {
      "drmOutput": [
        {
          "type": "FairPlay",
          "url": "http://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.11.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b",
          ...
        },
        {
          "type": "Widevine",
          "url": "http://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.13.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b",
          ...
        }
      ],
      "drmToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8",
      "widevineLicenseUrl": "https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2",
      "fairplayLicenseUrl": "https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2"
    },
    ...
  }
}
```

From the above response, you can get the following playback information:

1. The URL of the DRM-encrypted video.

2. The license server URL :

   - The license server URL for `Widevine` encryption is spliced using drmToken and `widevineLicenseUrl`.

   - The license server URL for `FairPlay` encryption is spliced using drmToken and `fairplayLicenseUrl`.

Below is the playback information obtained from the above sample:

Widevine encryption:

- URL of the encrypted video: `https://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.13.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b`
- License server URL: `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8`

FairPlay encryption:

- URL of the encrypted video: `https://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.11.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b`
- License server URL: `https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8`

## Step 5. Play the DRM-encrypted video in a player

The examples below show you how to play videos encrypted using `Widevine` and `FairPlay` respectively.

#### Play videos encrypted using `Widevine`

Go to the [Shaka Player Demo page](https://shaka-player-demo.appspot.com/demo/#audiolang=zh-CN;textlang=zh-CN;uilang=zh-CN;panel=CUSTOM%20CONTENT;build=uncompiled) via `Chrome`.

![image-20220426163418989](https://qcloudimg.tencent-cloud.cn/raw/0b9b5ae58e65c6b3c0789b8d98af57a1.png)

Click the **+** icon, and enter the URL of the encrypted video obtained in Step 4 for `Manifest URL`. Pass in `Widevine` for `Name`.

![image-20220426163853470](https://qcloudimg.tencent-cloud.cn/raw/0846706a160112ccea2712cd9c6b4d4c.png)

Enter the license server URL for `Widevine` obtained in Step 4 and click **Save**.

![image-20220426163939777](https://qcloudimg.tencent-cloud.cn/raw/702199c544c829db6f5d4815dcd4ff48.png)

The `Widevine` playback options will appear in the page.

![image-20220426164129657](https://qcloudimg.tencent-cloud.cn/raw/7d70df750e283d8a5a0d42596e08c14b.png)

Click **Play** to play the encrypted video.

#### Play videos encrypted using `FairPlay`

Go to the [Shaka Player Demo page](https://shaka-player-demo.appspot.com/demo/#audiolang=zh-CN;textlang=zh-CN;uilang=zh-CN;panel=CUSTOM%20CONTENT;build=uncompiled) via `Safari`.

![image-20220426163418989](https://qcloudimg.tencent-cloud.cn/raw/0b9b5ae58e65c6b3c0789b8d98af57a1.png)

Click the **+** icon, and enter the URL of the encrypted video obtained in Step 4 for `Manifest URL`. Pass in `FairPlay` for `Name`.

![image-20220426164907499](https://qcloudimg.tencent-cloud.cn/raw/70f01463b0afdf231dd014ea4782728f.png)

Enter the license server URL for `FairPlay` obtained in Step 4 for `Custom License Server URL`. Enter the `FairPlay` certificate (you can get the certificate in the VOD console) for `Custom License Certificate URL` and click **Save**.

![image-20220426164950762](https://qcloudimg.tencent-cloud.cn/raw/bdd9c3ecd2882537df76d657768855e9.png)

The `FairPlay` playback options will appear in the page.

![image-20220426165137520](https://qcloudimg.tencent-cloud.cn/raw/9da228ea1db9ab54a1631f605e24d806.png)

Click **Play** to play the encrypted video.


## Summary

Now, you have learned how to encrypt videos using DRM solutions and play the encrypted videos in a player.