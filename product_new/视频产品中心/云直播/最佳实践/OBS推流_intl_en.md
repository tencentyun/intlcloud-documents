## Solution Background
Open Broadcaster Software (OBS) is an easy-to-use third-party open-source software program for producing live streaming content free of charge. It can run on OS X, Windows, and Linux to meet the needs of various live broadcasting scenarios. You can go to the [OBS official website](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8) to download the latest version.
This document describes how to configure a stream on a PC in OBS Studio.

## Preparations
 - Log in to the [CSS console](https://console.cloud.tencent.com/live) and generate a push address. For more information, see [Push Configuration](https://intl.cloud.tencent.com/document/product/267/31059).
 - Install [OBS Studio](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8).

## Directions

### How to Use OBS Studio for Push
 1. **<span id="step1">Set a push address</span>**
Open OBS Studio and click **Controls** > **Settings** at the bottom to enter the Settings page.
![](https://main.qcloudimg.com/raw/493a19e0f2bbea80983c341dd742a044.png)
Click **Stream** on the left sidebar and select "Custom" as the service type. Take the push address below as an example.
![](https://main.qcloudimg.com/raw/55512ddf58bf32014424fa33b6f3d31f.png)
Divide the push address into two parts to enter the URL and stream name respectively. Enter the former part of the address before Path for the URL and the latter part after StreamName for the stream name. Thus, the parameter is set as below:
```
URL: rtmp://push.livetest.myqcloud.com/live/
Stream name: StreamName?txSecret=xxxxx&txTime=5C1E5F7F
```
For more information on how to get the push address, see [Getting Push Address Quickly](https://intl.cloud.tencent.com/document/product/267/31056#step-3.-view-and-configure-information).

 2. **<span id="step2">Configure a push</span>**
Click the **+** icon under the "Sources" box and select the input source. If you do not need to configure bitrate, recording, and others items, click **Controls** > **Start Streaming** to push the video to the set push address.
![](https://main.qcloudimg.com/raw/f8136fdb794595c8c491c995a74cdfcc.png)
Otherwise, click **Tools** > **Auto-Configuration Wizard** at the top, configure the push as prompted, and click **Controls** > **Start Streaming**.

 3. **Configure other push-related items**
 - Video broadcasting delay
Click **Controls** > **Settings** > **Output**, select **Advanced** for **Output Mode**, and then you can configure **Keyframe Interval** and other items as shown below:
![](https://main.qcloudimg.com/raw/5f48205da162f1230723729c36369f65.png)
Select **Advanced** on the left sidebar to configure **Stream Delay**:
![](https://main.qcloudimg.com/raw/c3ec9a71a014548eb680009d9798b1ac.png)
 - Local live recording
 If you need local live recording, you can record live streams for local backup. The configuration is as shown below:
![](https://main.qcloudimg.com/raw/a3c90994ef7447766914dc41605623c3.png)
Click **Controls** > **Settings** > **Output** and then click the **Recording** tab to configure recording. You can save recording files locally.
Resolution determines the clarity of video shown to viewers. The higher the resolution, the clearer the video. FPS (frames per second) determines how smooth a video look. The FPS value for ordinary videos ranges from 24 to 30, and lags would appear if it is lower than 16. Video games have a higher requirement for frame rate and would often smear if the value is below 30. The resolution and frame rate settings are as shown below:
![](https://main.qcloudimg.com/raw/f736ef195b26a81f46d1e26d7935a763.png)


## Related Operations
### Common Operations
1. **Common input sources**
 - **Image**: Live broadcasts a single image.
 - **Image Slide Show**: Plays back multiple images in a loop or sequentially.
 - **Scene**: Achieves various fascinating effects for live broadcasting. In this case, another scene, in part or in its entirety, can be embedded into the current scene as a source.
 - **Media Source**: Uploads and plays back local on-demand videos to be processed for live broadcasting.
 - **Text**: Adds text to the live broadcasting window in real time.
 - **Display Capture**: Dynamically captures operations on the desktop in real time. All operations are displayed during live broadcasting.
 - **Game Capture**: Live broadcasts games from the specified source. It is suitable for live game broadcasting at different scales.
 - **Window Capture**: Captures the selected window in real time. Only the current window is displayed during live broadcasting, while other windows will not be captured.
 - **Color Source**: Adds a solid color to the scene as background color. Transparency of the color can be adjusted to even make the screen transparent.
 - **Video Capture Device**: Dynamically captures the video being recorded by a camera for live broadcasting.
 - **Audio Input Capture**: Live broadcasts audio (from an audio input device).
 - **Audio Output Capture**: Live broadcasts audio (to an audio output device).

2. **Studio mode**
In Studio Mode, you can edit the content of the current live broadcast in real time and perform scene transitions during editing, minimizing the impact on user experience.
Click **Controls** > **Studio Mode** to enter the interface as shown below and configure **Scenes**, **Sources**, and **Scene Transitions**. Then, you can directly edit the live broadcast in the Preview pane on the left and click **Transition** to switch it to the live broadcasting pane on the right.
![](https://main.qcloudimg.com/raw/80e9e902e0e02902d78779ca5505b2f8.png)

### Pure Audio Push
According to the discussions in the OBS forum, OBS Studio 23.2.1 and earlier versions do not support pure audio push.
To implement a similar feature, you can follow the steps below. This method works by replacing a video with a static canvas (blank screen or image). If you need to reduce bandwidth usage, you can lower video frame rate and bitrate to get closer to pure audio push, but there will still be video data in the live stream.
1. As instructed in [OBS push configuration](#step2), select **Audio Input Capture** as input source. Do not select a video or image as video source.
![](https://main.qcloudimg.com/raw/c74e3e5058c69356095c761e1e572da6.png)
2. Go to **Controls** > **Settings** > **Video**, set **Output (Scaled) Resolution** and **Common FPS Values** to the minimum value, and click **OK** to save the configuration.
![](https://main.qcloudimg.com/raw/cb77c3deb8d3e9831aaa1421b5b13412.png)
3. Click **Output**, configure streaming as shown below, and set **Bitrate** to the minimum value. Click **OK** or **Apply** to save the configuration.
![](https://main.qcloudimg.com/raw/008e1ab02e2d08ee42f3a64e2e09d473.png)
4. As instructed in **Push** in [OBS push configuration](#step1), start the push, which will amount to pure audio push as the video content is shown as a blank screen or image. With video bitrate set to minimum, bandwidth usage is reduced significantly.

### Video Looping
**To loop a single video**
1. Click the **+** icon under the **Sources** box, select **Media Source** and in the pop-up window, select the video file to be looped in **Local File**, select **Loop**, and then click **OK**.
![](https://main.qcloudimg.com/raw/b41371c6674d4d8a2cd84fe37e3fbab4.png)
2. As instructed in [OBS push settings](#step1), click **Stream** on the left sidebar, and enter **Server** and **Stream Key** to start streaming, so the single video will be looped.

**To loop multiple videos**
OBS Studio does not support looping multiple videos itself, but you can use the loop feature of third-party video players and the Window Capture feature in OBS Studio to this end.
