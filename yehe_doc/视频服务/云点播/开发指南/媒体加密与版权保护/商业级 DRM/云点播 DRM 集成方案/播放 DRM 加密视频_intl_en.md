## Overview

This document shows you how to encrypt videos using DRM solutions and play the encrypted videos with a player.

## Prerequisites
Before you start, do the following:

### Activating VOD
Follow the steps below to activate VOD:

1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Purchase VOD services. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838).
3. Go to the [VOD console](https://console.cloud.tencent.com/vod).

At this point, you have activated VOD. 

### Obtaining FairPlay certificate information

See [Obtaining FairPlay Certificate Information](https://intl.cloud.tencent.com/document/product/266/46643).

### Submitting the certificate information

See [Submitting FairPlay Certificate Information to VOD](https://intl.cloud.tencent.com/document/product/266/49668).


## Step 1. Enable Hotlink Protection

The example below shows how to enable key hotlink protection for the default distribution domain under your account:
>? We do not recommend enabling hotlink protection for a domain name already in use. Doing so may cause failure to play existing videos.

1. Log in to the VOD console, select **Distribution and Playback** > [Domain Name](https://console.cloud.tencent.com/vod/distribute-play/domain) on the left sidebar. Find the default distribution domain, click **Set** on the right, and select the **Access Control** tab.
   <img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. Toggle on **Key Hotlink Protection**. In the pop-up window, click **Generate** to generate a random key (suppose it is `vodtestkey`). Copy the key and click **Confirm**. You will use the key later to generate playback signatures.
   ![image-KEY](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## Step 2. Encrypt a Video

1. In the VOD console, select **Media Assets** > [Video/Audio Management](https://console.cloud.tencent.com/vod/media) on the left sidebar, select the target video (in this example, the file ID of the video encrypted is `387702304941991610`), and click **Process**.

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
4. Click **Manage** in the **Operation** column of the video.
 - Under the **Basic Info** tab, you can view the thumbnail generated and outputs of adaptive bitrate streaming (template ID: 11 & 13).

   ![image-20220426201159056](https://qcloudimg.tencent-cloud.cn/raw/696e894ed0c3665990c12cc57ebf23bf.png)

 - Under the **Screenshot Info** tab, you can view the image sprite generated (template ID: 10).

   ![image-20220426201309975](https://qcloudimg.tencent-cloud.cn/raw/1a5878fd0286c46ef487bdf81ad8503a.png)

## Step 3. Generate a Player Signature

You will need the player signature to query past playback information. For directions on how to generate a player signature, see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099). For the example in this document, the payload for signature generation is as follows:

```json
{
  "appId": 1500014561,
  "fileId": "387702304941991610",
  "currentTimeStamp": 1661163373,
  "expireTimeStamp": 2648557919,
  "pcfg":"advanceDrmPreset"
}
```

The key generated for the example in this document is `vodtestkey`, and the player signature (`psign`) generated is as follows:

`eyJhbGciOiJIUzI1NiJ9.eyJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA0OTQxOTkxNjEwIiwiY3VycmVudFRpbWVTdGFtcCI6MTY2MTE2MzM3MywiZXhwaXJlVGltZVN0YW1wIjoyNjQ4NTU3OTE5LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.rEZLhjgsoLc2htIUI_HckxvhVmdBhQyf5d-2Kku1JeA`

## Step 4. Play the DRM-encrypted video

### Web

#### Using the VOD player

To play the DRM-encrypted video using the VOD player, just pass in the file ID of the video and your VOD account’s AppID when initializing the player.


#### Step 1. Import files

Import the player’s style file and script files into the webpage.

```
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/tcplayer.min.css" rel="stylesheet"/>
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/TXLivePlayer-1.2.3.min.js"></script>

 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/hls.min.1.1.5.js"></script>

 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/flv.min.1.6.3.js"></script>
  
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/dash.all.min.4.4.1.js"></script>
 
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/tcplayer.v4.5.4.min.js"></script>
```

#### Step 2. Add a player container

Add a player container to wherever you want to display the player:

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>? You can customize the container ID as well as the height and width of the container.

#### Step 3. Add the initialization code

Add the following script to your page initialization code and pass in the required initialization parameters (including the Player Signature `psign` generated in Step 3):

```
var player = TCPlayer('player-container-id', {
    appID: '1500014561' // The appID of your VOD account (required).
    fileID: '387702304941991610', // The file ID of the video to play (required).
    psign: 'eyJhbGciOiJIUzI1NiJ9.eyJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA0OTQxOTkxNjEwIiwiY3VycmVudFRpbWVTdGFtcCI6MTY2MTE2MzM3MywiZXhwaXJlVGltZVN0YW1wIjoyNjQ4NTU3OTE5LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.rEZLhjgsoLc2htIUI_HckxvhVmdBhQyf5d-2Kku1JeA',
    // For other parameters, see https://intl.cloud.tencent.com/document/product/266/39105
});
```

### iOS

To play the DRM-encrypted video on iOS, refer to Integration Guide (Through `FileId`). You need to use the player signature (`psign`)  generated in Step 3 (Generate a Player Signature).

>? Please  [submit a ticket](https://console.cloud.tencent.com/workorder/category) for the player SDK that supports DRM.

![](https://qcloudimg.tencent-cloud.cn/raw/1cba8f5fffad9827a267314ced65d078.png)

### Android

To play the DRM-encrypted video on Android, refer to [Integration Guide](https://intl.cloud.tencent.com/document/product/266/49670#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E5.90.AF.E5.8A.A8.E6.92.AD.E6.94.BE) (Through `FileId`). You need to use the player signature (`psign`)  generated in Step 3 (Generate a Player Signature).

>? Please  [submit a ticket](https://console.cloud.tencent.com/workorder/category) for the player SDK that supports DRM.

![](https://qcloudimg.tencent-cloud.cn/raw/77ec9a38fc9530305affa447df8f9e14.png)

## Summary

Now, you have learned how to encrypt videos using DRM solutions and play the encrypted videos in a player.

>? If you have any questions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
