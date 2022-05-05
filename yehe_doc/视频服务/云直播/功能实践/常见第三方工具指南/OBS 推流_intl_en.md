## Overview
Open Broadcaster Software (OBS) is a third-party open-source tool for live streaming. It’s easy to use and free of charge, and it supports OS X, Windows, and Linux. OBS can be used in a wide range of scenarios to meet most live streaming needs without requiring additional plugins. You can download its latest version at the [OBS website](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8).

## Prerequisites
- You have installed [OBS Studio](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8).
- You have activated [CSS](https://console.cloud.tencent.com/live) and [added a playback domain](https://intl.cloud.tencent.com/document/product/267/35970) with an ICP filing number in the console (for push, you can use the default domain we provide or add your own).

[](id:step0)
## Getting a Push URL
1. Log in to the CSS console, click **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** in the left sidebar, and follow the steps below:
   1. Select *Push Domain** for **Domain Type**.
   2. Select the domain name you have added in **Domain Management**.
   3. Enter an application name (`AppName`), which is used to distinguish applications under the same domain. The default value is `live`.
   4. Enter a custom stream name (`StreamName`), such as `live`.
   5. Select the expiration time of the address, such as `2020-06-09 23:59:59`.
2. Click **Generate Address** to get an OBS push URL.


[](id:normal)
## Configuring OBS for Push
### Step 1. Configure the push URL[](id:step1)
1. Open OBS and click **Controls** > **Settings** at the bottom to enter the settings page.
![](https://main.qcloudimg.com/raw/493a19e0f2bbea80983c341dd742a044.png)
2. Click **Stream** and select **Custom** for **Service**.
3. Fill in the **Server** and **Stream Key** fields with the information obtained in [Getting a Push URL](#step0).
    - Server: Enter the OBS push address (`rtmp://domain/AppName/`).
    - Stream key: Enter the OBS push name (`StreamName?txSecret=xxxxx&txTime=5C1E5F7F`).
![](https://main.qcloudimg.com/raw/55512ddf58bf32014424fa33b6f3d31f.png)
4. Click **OK** to save the information.

### Step 2. Configure the source[](id:step2)
>? For bitrate, recording, and other settings, click **Tools > Auto-Configuration Wizard** in the top menu bar, and follow the instructions provided by OBS to complete the settings.

1. Find **Sources** in the menu bar at the bottom.
![](https://main.qcloudimg.com/raw/f8136fdb794595c8c491c995a74cdfcc.png)
2. Click **+** and select a source that fits your needs, for example, **Display Capture**.
 ![](https://main.qcloudimg.com/raw/f8136fdb794595c8c491c995a74cdfcc.png)
**Common live streaming sources**
<table>
<thead><tr><th width="20%">Source</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Image</td>
<td>Publishing a single image</td>
</tr><tr><td>Image Slide Show</td>
<td>Publishing multiple images (you can determine the order of playback and whether to loop the playback)</td>
</tr><tr><td>Scene</td>
<td>Insertion of an entire scene as the source to enable various streaming effects</td>
</tr><tr><td>Media Source</td>
<td>Publishing a local file</td>
</tr><tr><td>Text</td>
<td>Adding real-time text to your stream</td>
</tr><tr><td>Display Capture</td>
<td>Capturing and publishing your monitor in real time</td>
</tr><tr><td>Game Capture</td>
<td>Streaming a game from a specified source in real time</td>
</tr><tr><td>Window Capture</td>
<td>Capturing and publishing the window you select in real time</td>
</tr><tr><td>Color Source</td>
<td>Adding a solid color to your scene. You can use this source for background colors or a global color tint by using the alpha channel.</td>
</tr><tr><td>Video Capture Device</td>
<td>Capturing and publishing the images captured by a camera in real time</td>
</tr><tr><td>Audio Input Capture</td>
<td>Audio live streaming (audio input device)</td>
</tr><tr><td>Audio Output Capture</td>
<td>Audio live streaming (audio output device)</td>
</tr>
</tbody></table>

### Step 3. Use the studio mode[](id:step3)
In studio mode, you can edit your current live stream in real time and configure transitions for scene swapping, minimizing the impact on user experience.
1. Click **Controls > Studio Mode** in the menu bar at the bottom.
2. After editing, click **Transition** to swap the edit and live views.
![](https://main.qcloudimg.com/raw/80e9e902e0e02902d78779ca5505b2f8.png)

### Step 4. Start streaming[](id:step4)
1. Find **Controls** in the menu bar at the bottom.
2. Click **Start Streaming** to push your video to the configured push URL.
![](https://main.qcloudimg.com/raw/80e9e902e0e02902d78779ca5505b2f8.png)

>? 
>- If you see ![](https://main.qcloudimg.com/raw/a10bafc9eb0895dc4c6b542b61217253.png) at the bottom, the push is successful.
>- To stop streaming, click **Stop Streaming**.

## Other Push Settings
### Streaming latency
1. Go to **Controls > Settings > Output**.
2. Select **Advanced** for **Output Mode** to set parameters including **Keyframe Interval**.
![](https://main.qcloudimg.com/raw/5f48205da162f1230723729c36369f65.png)
3. Click **Advanced** in the left sidebar to set **Stream Delay**:
![](https://main.qcloudimg.com/raw/c3ec9a71a014548eb680009d9798b1ac.png)

### Local live recording
To record live streams to your local storage, follow the steps below:
1. Go to **Controls > Settings > Output**.
2. Complete the settings under **Recording** and click **OK**.
![](https://main.qcloudimg.com/raw/008e1ab02e2d08ee42f3a64e2e09d473.png)
3. Click **Video** in the left sidebar to set the resolution and frame rate.
>? Resolution determines the clarity of video shown to viewers. The higher the resolution, the clearer the video. Frame rate (frames per second) determines playback smoothness. Typical frame rate falls in the range of 24 fps to 30 fps. Playback may stutter if frame rate is lower than 16 fps. Video games require higher frame rate and tend to stutter at a frame rate lower than 30 fps.

![](https://main.qcloudimg.com/raw/f736ef195b26a81f46d1e26d7935a763.png)

### Transcoding
To change the video bitrate during streaming, follow the steps below:
1. Click **Controls > Settings** in the menu bar at the bottom.
2. Click **Output** in the left sidebar and select **Simple** for **Output Mode**.
3. Enter the bitrate you want to use and click **OK**.
![](https://main.qcloudimg.com/raw/008e1ab02e2d08ee42f3a64e2e09d473.png)




## More
### Audio-only push
According to OBS Forums, OBS Studio 23.2.1 and earlier versions do not support audio-only streaming.
You can follow the steps below to implement a similar feature. The method uses a static canvas (blank screen or image) for video content. This means there will still be video data in the live stream. To reduce bandwidth usage, you can set the video frame rate and bitrate to the minimum values.
1. As instructed in [Configure the source](#step2), select **Audio Input Capture** as the source. Do not use a video or image source.

2. Go to **Controls > Settings > Video**.
3. Set **Base (Canvas) Resolution** and **Common FPS Values** to the minimum values and click **OK**.
    ![](https://main.qcloudimg.com/raw/cb77c3deb8d3e9831aaa1421b5b13412.png)
4. Click **Output** in the left sidebar, configure the output as shown below (set **Bitrate** to the minimum value), and click **OK**.
    ![](https://main.qcloudimg.com/raw/008e1ab02e2d08ee42f3a64e2e09d473.png)
5. Start streaming as instructed in [Configuring OBS for Push](#normal). The audience will hear audio, while the video will be a blank screen or an image. Because the video bitrate is set to the minimum value, the bandwidth usage is significantly lower than that of video push.

### Video looping
- **Loop a single file**
    1. Click **+** in **Sources** and select **Media Source**. In the pop-up window, choose a local file to stream, select **Loop**, and click **OK**.
    ![](https://main.qcloudimg.com/raw/b41371c6674d4d8a2cd84fe37e3fbab4.png)
    2. Set the **Server** and **Stream Key** as instructed in [Configure the push URL](#step1).


You can use the following methods to check whether the push is successful:
- PC: Use [VLC](https://intl.cloud.tencent.com/document/product/267/32483) to play the stream.
- Mobile: Use the [MLVB](https://intl.cloud.tencent.com/zh/document/product/1071) SDK to play the stream.
>? Mobile Live Video Broadcasting (MLVB) extends the services of CSS to mobile devices. It offers not only an RTMP SDK that allows quick integration, but also a one-stop, multi-cloud solution that integrates Tencent Cloud services including LVB, LEB, VOD, IM, and COS.
[Live Event Broadcasting (LEB)](https://intl.cloud.tencent.com/document/product/1071/41875) is the ultra-low-latency version of LVB. It delivers superior playback experience with millisecond latency and is suitable for scenarios with high requirements on latency, such as online education, sports streaming, and online quizzes.





