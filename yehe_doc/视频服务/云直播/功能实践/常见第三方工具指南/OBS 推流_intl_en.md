## Solution Background
Open Broadcaster Software (OBS) is an easy-to-use third-party open-source software program for producing live streaming content free of charge. It can run on OS X, Windows, and Linux to meet the needs of various live broadcasting scenarios. You can go to the [OBS official website](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8) to download the latest version.
Preparations

- Install [OBS Studio](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8).




1. Log in to the CSS console, and the click **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**.
   1. Select the type, such as **push domain** or **playback domain**.
   2. Select a domain name you have already added on the domain management page.
   3. `AppName` is the address path used to differentiate multiple applications under the same domain name, which is `live` by default.
   4. Enter a custom `StreamName`, such as `liveteststream`.
   5. Select the expiration time of the address, such as `2019-11-30 23:59:59`.


![](https://main.qcloudimg.com/raw/64c3815306c68daebb5fc7d53bb43164.png)



Open OBS Studio and click **Controls** > **Settings** at the bottom to enter the Settings page.
![](https://main.qcloudimg.com/raw/56e4c19f24d08df7b8f8815f1ffb6857.png)


    
    Stream name: StreamName?txSecret=xxxxx&txTime=5C1E5F7F
![](https://main.qcloudimg.com/raw/c6cd899e29c9256102444bf20d1889d3.png)
4. Click **OK** to save the configuration.





![](https://main.qcloudimg.com/raw/d370f4fbf0f9a57116eee0543ea6a59e.png)

 ![](https://main.qcloudimg.com/raw/c59eff44ffd2ac4c785fe4e4e3bd79b8.png)
1. **Common input sources**
<table>
<thead><tr><th width="15%">Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>





- **Scene**: Achieves various fascinating effects for live broadcasting. In this case, another scene, in part or in its entirety, can be embedded into the current scene as a source.





- **Display Capture**: Dynamically captures operations on the desktop in real time. All operations are displayed during live broadcasting.



- **Window Capture**: Captures the selected window in real time. Only the current window is displayed during live broadcasting, while other windows will not be captured.

- **Color Source**: Adds a solid color to the scene as background color. Transparency of the color can be adjusted to even make the screen transparent.






</tr>
</tbody></table>


In Studio Mode, you can edit the content of the current live broadcast in real time and perform scene transitions during editing, minimizing the impact on user experience.


![](https://main.qcloudimg.com/raw/1fe0d66ff608a438fc8e2e49436a5ff9.png)




![](https://main.qcloudimg.com/raw/ce27c9985d6531c07b2b166ad54ea3b9.png)

>? 




- Video broadcasting delay


![](https://main.qcloudimg.com/raw/216b6ec15a5ef1abe8a64d6000d669d7.png)
Select **Advanced** on the left sidebar to configure **Stream Delay**:
![](https://main.qcloudimg.com/raw/e1cd9e4c9e813a5706e1ef23f332c7d1.png)

- Local LVB recording
If you need local LVB recording, you can record live streams for local backup. The configuration is as shown below:


![](https://main.qcloudimg.com/raw/d269d04ed1f74f5478d9efe6550229bd.png)

Resolution determines the clarity of video shown to viewers. The higher the resolution, the clearer the video. FPS (frames per second) determines how smooth a video look. The FPS value for ordinary videos ranges from 24 to 30, and lags would appear if it is lower than 16. Video games have a higher requirement for frame rate and would often smear if the value is below 30. The resolution and frame rate settings are as shown below:
>
![](https://main.qcloudimg.com/raw/4a3ce8f1a47572dd214f104ef3086398.png)






![](https://main.qcloudimg.com/raw/3cbeecf4eb6517563f5a6ee5ff879498.png)





### Pure Audio Push
According to the discussions in the OBS forum, OBS Studio 23.2.1 and earlier versions do not support pure audio push.
To implement a similar feature, you can follow the steps below. This method works by replacing a video with a static canvas (blank screen or image). If you need to reduce bandwidth usage, you can lower video frame rate and bitrate to get closer to pure audio push, but there will still be video data in the live stream.
1. As instructed in [OBS push configuration](#step2), select **Audio Input Capture** as input source. Do not select a video or image as video source.
![](https://main.qcloudimg.com/raw/93048a70d6fd953c3c7d390580dd159d.png)

2. Go to **Controls** > **Settings** > **Video**, set **Output (Scaled) Resolution** and **Common FPS Values** to the minimum value, and click **OK** to save the configuration.
![](https://main.qcloudimg.com/raw/0e564c4d21b30a088cc81d138c72238f.png)
3. Click **Output**, configure streaming as shown below, and set **Bitrate** to the minimum value. Click **OK** or **Apply** to save the configuration.
![](https://main.qcloudimg.com/raw/f873ce1ee65d909d80ebe325171d28db.png)
4. As instructed in **Push** in [OBS push configuration](#step1), start the push, which will amount to pure audio push as the video content is shown as a blank screen or image. With video bitrate set to minimum, bandwidth usage is reduced significantly.

### Video Looping
**To loop a single video**
    1. Click the **+** icon under the **Sources** box, select **Media Source** and in the pop-up window, select the video file to be looped in **Local File**, select **Loop**, and then click **OK**.
    ![](https://main.qcloudimg.com/raw/08f3d93083fe55c31e510d6069cf33d7.png)
    2. As instructed in [OBS push settings](#step1), click **Stream** on the left sidebar, and enter **Server** and **Stream Key** to start streaming, so the single video will be looped.

- 


3. For more information, see [VLC Player](https://cloud.tencent.com/document/product/267/32727).
2. Download the [MLVB SDK](https://cloud.tencent.com/document/product/454/7873).







