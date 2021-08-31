The UDP-based TRTC service can redirect audio and video streams to standard live CDN systems through protocol conversion. This process is called "relayed push streaming" or "relayed live streaming".
After enabling relayed live streaming on the TRTC Console, you can automatically have the access to the audio and video streams in a TRTC room. In addition, you can enable the On-Cloud MixTranscoding feature by calling the **setMixTranscodingConfig** API provided in TRTCCloud to mix multiple streams of video images into one stream.

The following describes how to play the audio/video streams in a TRTC room on Tencent Cloud’s LVB CDN system over the standard **HTTP + FLV** protocol.


## Demo
The relayed live streaming feature has been incorporated into the TRTC [Demo](https://intl.cloud.tencent.com/document/product/647/35076). During a video call, click **More** to locate the feature (download TXLivePlayer from MLVB Demo).

## Sample Code

| Platform | Generate CDN Playback URL | Set On-Cloud MixTranscoding Parameters |
|---------|---------|---------|
| iOS | File: [TRTCMoreViewController.m](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTCDemo/TRTC/TRTCMoreViewController.m) <br>Function: onBtnClick() | File: [TRTCMainViewController.m](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTCDemo/TRTC/TRTCMainViewController.m)<br>Function: updateCloudMixtureParams() |
| Android | File: [CdnPlayManager.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTCDemo/app/src/main/java/com/tencent/liteav/demo/trtc/sdkadapter/cdn/CdnPlayManager.java)<br>Function: initPlayUrl() | File: [TRTCRemoteUserManager.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTCDemo/app/src/main/java/com/tencent/liteav/demo/trtc/sdkadapter/remoteuser/TRTCRemoteUserManager.java)<br>Function: updateCloudMixtureParams() |
| Windows (C++) |  File: [TRTCSettingViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCSettingViewController.cpp)<br>Function: NotifyOtherTab | File: [TRTCCloudCore.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/sdkinterface/TRTCCloudCore.cpp)<br>Function: updateMixTranCodeInfo() |
| Windows (C#) | File: [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs)<br>Function: OnShareUrlLabelClick| File: [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs)<br>Function: UpdateMixTranCodeInfo() |
| Mac | N/A | File: [TRTCMainWindowController.m](https://github.com/tencentyun/TRTCSDK/blob/master/Mac/TRTCDemo/TRTC/TRTCMainWindowController.m)<br>Function: updateCloudMixtureParams() |

## Use Cases
Relayed Live Streaming allows you to implement co-anchoring and PK between anchors on mainstream live broadcasting platforms:

1. An anchor can create a TRTC room via the `enterRoom()` API in TRTCCloud, and initiate co-anchoring and PK with another anchor in another room in real time using the `connectOtherRoom()` API. If Relayed Live Streaming is enabled under the current account, the CDN playback URL of a video stream in the room can be obtained (HTTP-FLV protocol is recommended for better instant broadcasting performance).
2. A viewer can watch the livestream at the CDN playback URL using TXLivePlayer, or enter the TRTC room of the anchor using the `enterRoom()` API in TRTCCloud to interact with the anchor by initiating co-anchoring.
3. After going into the co-anchoring or PK mode, the anchor can enable Cloud MixTranscoding (mix multiple video streams into one stream) using the `setMixTranscodingConfig()` API in TRTCCloud to switch the single-user video stream at the original CDN playback URL to multi-user one by mixing the video streams of multiple users, without the viewers having to switch the LVB CDN playback URL.
4. When co-anchoring ends, the anchor can call the `setMixTranscodingConfig()` API again to disable Cloud MixTranscoding, and switch the stream at the CDN playback URL back to that of a single user.

## Using the Service

### Step 1: Activate the service.

Log in to the [TRTC Console](https://console.cloud.tencent.com/rav), click the target application tab, and then select **Function Configuration** to enable **Auto-Relayed Live Streaming**. Please note that you need to activate Tencent's [LVB](https://console.cloud.tencent.com/live) service before you can enable this feature.

### Step 2: Generate CDN playback URLs for individual streams.

After Relayed Live Streaming is enabled, each video stream in the TRTC room is assigned a playback URL in the following format:
```
http://[bizid].liveplay.myqcloud.com/live/[streamid].flv
```

Fill in `bizid` and `streamid` as follows:

- bizid: This information is related to the LVB service. You can obtain it in **LVB Info** by selecting the created application on the [TRTC Console](https://console.cloud.tencent.com/rav) and clicking **Account Info**.
- stream type: The stream type of camera-captured videos is "main", and that of screen-captured ones is "aux" (since a WebRTC-based client only supports one stream of upstream videos at a time, the stream type of screen-captured videos on a WebRTC-based client is "main" as well).
- `streamid = bizid_MD5 (room ID_userId_stream type)`. This means `streamid` is constructed by concatenating `bizid`, `_`, and the MD5 value calculated from `"room ID_userId_stream type"`.


The following example shows how to generate the CDN playback URL:
```
If bizid = 8888, room ID with relayed live streaming enabled = 12345, userId = userA, and the user is using a camera:

1. Calculate MD5(12345_userA_main) = 8d0261436c375bb0dea901d86d7d70e8
2. The resulting CDN playback URL for userA is:
 FLV protocol: http://8888.liveplay.myqcloud.com/live/8888_8d0261436c375bb0dea901d86d7d70e8.flv
 HLS protocol: http://8888.liveplay.myqcloud.com/live/8888_8d0261436c375bb0dea901d86d7d70e8.m3u8
```

> In the above example, `[bizid].liveplay.myqcloud.com` is the playback domain name. As required by the relevant authorities in China, you must use your own playback domain name to release your apps to an AppStore in China. You can configure your playback domain name simply by adding the domain name in **LVB Console** -> **[Domain Name Management](https://console.cloud.tencent.com/live/domainmanage)**. The domain name `[bizid].liveplay.myqcloud.com` can only be used for debugging. Tencent Cloud will gradually obsolete it and does not guarantee its availability in the future.

### Step 3: Mix streams.

Enable On-Cloud MixTranscoding by calling the `setMixTranscodingConfig` API in TRTCCloud to obtain the mixed video stream. The parameter `TRTCTranscodingConfig` of this API configures:
 - position and size of each subimage;
 - image quality and encoding parameter of the mixed stream.

For more information, please see [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618).
> Instead of mixing streams at the end users, `setMixTranscodingConfig` sends the stream mixing configuration to the cloud for stream mixing and transcoding. Because both involve decoding and re-encoding the original audio/video data, they may take a while. Therefore, a mixed stream has a playback latency 1 or 2 seconds longer than individual streams.

### Step 4: Start playback.

We recommend an **http://~.flv ** address beginning with `http` and ending with `.flv`, which features a short playback latency, good instant broadcasting performance, and high stability. It's recommended to use the TXLivePlayer included in TRTC SDK. 


### Step 5: Optimize the latency.

With Relayed Live Streaming enabled, a live stream on an "http://~.flv" address has a higher playback latency than the calls in the TRTC rooms because the video data needs to be distributed via the LVB CDN. With TXLivePlayer, the following latency could be achieved:

| Image Stream Type | TXLivePlayer Playback Mode | Average Latency |
|:-------:|:-------:|:--------:|
| Individual | Ultrafast mode (recommended) | **2-3 sec** |
| Mixed | Ultrafast mode (recommended) | **4-5 sec** |

If you experience a latency higher than stated above in practice, optimize the latency by following the tips below:

- **Use the TXLivePlayer included in the TRTC SDK**
TXLivePlayer uses a Tencent-developed playback engine that allows for latency control. In contrast, using ijkplayer or ffmpeg to play videos from such URL can cause uncontrollable latency. This is because they are thin wrappers around ffmpeg, which lacks the ability to compensate for latency.

- **Set TXLivePlayer to the ultrafast mode**
Enable the ultrafast mode by configuring three parameters of TXLivePlayerConfig. Taking iOS as an example, the code is as follows:
    ```
    // Set TXLivePlayer to ultrafast mode
    TXLivePlayerConfig * config = [[TXLivePlayerConfig alloc] init];
    config.bAutoAdjustCacheTime = YES;
    config.minAutoAdjustCacheTime = 1; // Min. buffer time 1 sec
    config.maxAutoAdjustCacheTime = 1; // Max. buffer time 1 sec
    [player setConfig:config];
    // Start live stream playback
    ```

## FAQs
**Why is the video images lagged and blurry when there is only one user in the room?**
Please set the parameter TRTCAppScene in `enterRoom` to **TRTCAppSceneLIVE**. In VideoCall mode, video calls are optimized for low bitrate and frame rate to save data usage. This is why the video images are lagged and blurry.
