
## Overview
To facilitate your integration of TRTC, we have supported publishing over the standard protocol RTMP. You can install [OBS](https://obsproject.com/download) or FFmpeg to publish streams with TRTC, without the need for additional plugins. OBS is a third-party open-source tool for live streaming. It’s easy to use and free of charge, and it supports OS X, Windows, and Linux, making it applicable to a wide range of scenarios and capable of meeting most live streaming needs. You can download its latest version at the [OBS website](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8).

This feature is currently in beta (we will notify you in advance if we are to charge it). However, an RTMP stream is considered a user in a TRTC room, which is subject to TRTC’s billing rules. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/647/34610). If you want to try this feature, contact us at xunchenliu@tencent.com to add your account to our allowlist (you need to provide your `SDKAppID`).

>! You cannot play streams from TRTC over RTMP. To relay streams to CDNs for playback, see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).

## Use Cases
<table>
<thead><tr><th width=22%>Use Case</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Online education</td>
<td>Using the desktop edition of OBS or FFmpeg, a teacher can publish a video of teaching materials (the majority of media formats are supported) over RTMP to a TRTC room. Students in the room can play the video via the TRTC SDK and see the same image as the teacher as the latter adjusts the playback progress/speed or switches between chapters. Excellent synchronization across multiple devices ensures better teaching quality. </td>
</tr><tr>
<td>Watching sports events</td>
<td>Sports event organizers provide content in the form of RTMP streams. You can publish the streams to TRTC rooms to allow audience to watch the events with ultra-low latency. With TRTC’s interaction capability, audience can also audio/video chat with each other throughout the process.</td>
</tr><tr>
<td>Others</td>
<td>You can also use the RTMP publishing feature to implement other real-time interactive applications based on streaming.</td>
</tr></tbody></table>


## Configuring OBS for Publishing
### Prerequisites[](id:ready)
You have installed [OBS](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8).

### Selecting source[](id:step1)
In the **Sources** panel at the bottom, click **+**, and select a source based on your needs. Common sources include:

| Source         | Description                                                         |
| :------------- | :----------------------------------------------------------- |
| Image           | Publishing a single image                                         |
| Image Slide Show |  Publishing multiple images (you can determine the order of playback and whether to loop the playback)                                 |
| Scene           | Insertion of an entire scene as the source to enable various streaming effects  |
| Media Source         | Publishing a local file           |
| Text           | Adding real-time text to your stream                                   |
| Window Capture       | Capturing and publishing the window you select in real time |
| Video Capture Device   | Capturing and publishing the images captured by a camera in real time             |
| Audio Input Capture   | Audio live streaming (audio input device)                           |
| Audio Output Capture   | Audio live streaming (audio output device)                           |


![](https://qcloudimg.tencent-cloud.cn/raw/cd227431216391302e50a3ed4e794de2.png)


### Setting publishing parameters[](id:step2)
1. In the **Controls** panel at the bottom, click **Settings**.
![img](https://qcloudimg.tencent-cloud.cn/raw/26404eda70b80a654f3119683ae3ca46.png)
2. Click **Stream** and select **Custom** for **Service**.
3. Enter `rtmp://rtmp.rtc.qq.com/push/` for **Server**.
4. Enter a stream key in the following format:
```
Room ID?sdkappid=Application&userid=User ID&usersig=Signature
```
Replace “Room ID”, “Application”, “User ID”, and “Signature” with the actual values, for example:
```
22998?sdkappid=140*****66&userid=******rtmp2&usersig=eJw1jdE***************ZLgi5UAgOzoMhrayt*cjbmiCJ699T09juc833IMT94Ld7I0iHZqVDzvVAqkZsG-IKlzLiXOnEhswHu1iUyTc9pv*****D8MQwoA496Ke6U1ip4EAH4UMc5H9pSmv6MeTBWLamhwFnWRBZ8qKGRj8Yp-wVbv*mGMVZqS7w-mMDQL
```
	- To simplify the parameters, TRTC supports only string-type room IDs. A room ID cannot exceed 64 characters and can contain only digits, letters, and underscores. To play an RTMP stream via TRTC, users must **use a string-type room ID to enter the room the stream is published to**.
	- For how UserSig is generated, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). **Make sure your signature is within the validity period**.
	- The URL made up of the above server address and stream key can also be used for publishing with FFmpeg or other RTMP libraries.
![](https://qcloudimg.tencent-cloud.cn/raw/c3b309db1312f19abb3ca147c1ecea32.png)

### Configuring output[](id:step3)
Since RTMP does not support B-frames, you can set the video encoding parameters of OBS as follows to remove B-frames.
1. Go to **Controls** > **Settings** > **Output**.
2. Select **Advanced** for **Output Mode**, enter **1** or **2** for **Keyframe Interval**, and click **OK**.

![](https://qcloudimg.tencent-cloud.cn/raw/072b2fbaf9a3bf6674a48943223de22c.png)  


### Setting video parameters[](id:step4)
You can set video resolution and frame rate under the **Video** section of **Settings**. Resolution determines the clarity of video shown to audience. The higher the resolution, the clearer the video. Frame rate (frames per second) determines playback smoothness. Typical frame rate falls in the range of 24 fps to 30 fps. Playback may stutter if frame rate is lower than 16 fps. Video games require higher frame rate and tend to stutter at a frame rate lower than 30 fps.
![](https://qcloudimg.tencent-cloud.cn/raw/81e9e716bf76a8a1a20a1badcf7dfcd9.png)


### Advanced[](id:step5)
- To reduce end-to-end delay, you are not advised to enable **Stream Delay**.
- Keep **Automatically Reconnect** enabled and make **Retry Delay** as short as possible so that the publisher can be reconnected quickly after disconnection due to network jitter.
![](https://qcloudimg.tencent-cloud.cn/raw/7a25a1cb3e2a6daf07508bcb2fdabeb6.png)


### Publishing[](id:step6)
1. In the **Controls** panel at the bottom, click **Start Streaming**.
![](https://qcloudimg.tencent-cloud.cn/raw/8709c618536109bfb02e860b47581e45.png)
2. If streaming is successful, the bottom bar will show streaming statistics, and the entry of a user will be recorded by the monitoring dashboard of the TRTC console.
![](https://qcloudimg.tencent-cloud.cn/raw/15c0d1b5df33c4a738050f1f532a990c.png)

### Playback from other devices[](id:step7)
As mentioned in [Setting publishing parameters](#step2), to play an RTMP stream, other users must use a string-type room ID to enter the TRTC room the stream is published to. Playback from web looks like this:
![](https://qcloudimg.tencent-cloud.cn/raw/787178aa5dc550a592f5455d9f2ffb8e.png)

## Configuring FFmpeg[](id:FFmpeg)
To publish streams using the command line or other RTMP libraries, you can use the RTMP publishing URL made up of the server address and stream key in [Setting publishing parameters](#step2). Use H.264 for video encoding, AAC for audio encoding, and FLV for the container format, and we recommend 2s or 1s for GOP.
The configuration of FFmpeg parameters varies with scenarios, so you need to have some knowledge of FFmpeg in order to publish using the software. The table below lists some common commands for FFmpeg. For more options, see [FFmpeg documentation](https://ffmpeg.org/ffmpeg.html).

### FFmpeg command line[](id:order)
```
ffmpeg [global_options] {[input_file_options] -i input_url} ... {[output_file_options] output_url} 
```

### Common FFmpeg options[](id:set)
<table>
<thead><tr><th>Option</th><th>Description</th></tr></thead>
<tbody><tr>
<td>-re</td><td>Read input at native frame rate. This is usually used to read local files.</td>
</tr></tr></tbody></table>

Options for **output_file_options** include:

<table>
<thead><tr><th>Option</th><th>Description</th></tr></thead>
<tbody><tr>
<td>-c:v</td><td>Video encoding library. <code>libx264</code></td> is recommended.
</tr><tr>
<td>-b:v</td><td>Video bitrate. For example, <code>1500k</code> means 1500 Kbps.</td>
</tr><tr>
<td>-r</td><td>Video frame rate</td>
</tr><tr>
<td>-profile:v</td><td>Video profile. Set it to <code>baseline</code>, which means not to encode B-frames. The TRTC backend does not support B-frames.</td>
</tr><tr>
<td>-g</td><td>GOP (keyframe interval)</td>
</tr><tr>
<td>-c:a</td><td>Audio encoding library. <code>libfdk_aac</code> is recommended.</td>
</tr><tr>
<td>-ac</td><td>Number of sound channels. Valid values: 1, 2</td>
</tr><tr>
<td>-b:a</td><td>Audio bitrate</td>
</tr><tr>
<td>-f</td><td>Container format. Set it to <code>flv</code>. The FLV container format is required to publish to TRTC.</td>
</tr></tbody></table>
Below is an example of reading a local file and publishing it to TRTC.

```
ffmpeg -loglevel info -re -i sample.flv -c:v libx264 -preset fast -profile:v baseline -g 30 -sc_threshold 0 -b:v 1500k -c:a libfdk_aac -ac 2 -b:a 128k -f flv 'rtmp://rtmp.rtc.qq.com/push/hello-string-room?userid=rtmpForFfmpeg&sdkappid=140xxxxxx&usersig=xxxxxxxxxx'
```

### Demo: playback from web[](id:view)
![](https://qcloudimg.tencent-cloud.cn/raw/3ba672af6154d1998b4e5ede78296d9d.png)


