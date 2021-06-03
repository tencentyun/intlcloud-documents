End-to-end call details are the details of data transferred across the sender-receiver link. The preconditions of a smooth audio/video call are good network connections and stable device performance, which are what you should start with when checking the end-to-end details of a call.

## Directions

1. Log in to the TRTC console. In **[Monitoring Dashboard](https://console.cloud.tencent.com/trtc/monitor)**, select the room whose call details you want to view.
2. Click the room ID or **View Call Details** on the right to go to the [Call Details](https://intl.cloud.tencent.com/zh/document/product/647/39070) page.
3. On the receiver/sender page, select the ID of the user whose data you want to view, and go to the end-to-end details page via either of two methods.
	- On the **Receiver** page, click **Select sender to view details** on the right and select a user ID.
	- On the **Sender** page, click **View Details**.

![](https://main.qcloudimg.com/raw/dbd80dcb851766e32acf8020e5f2555d.png)




## Information Displayed

The end-to-end details page shows the data of **Video**, **Audio**, and **Screen Sharing**, which can be viewed from the perspective of the receiver or sender.
![](https://main.qcloudimg.com/raw/8f1a21141b61590e6b7a13a705030900.png)
You can analyze end-to-end data from [network conditions](#internet) and [device status](#equipment).

### Analyzing network conditions<span id="internet"></span>

Ideally, data should be transferred at high bandwidth, with zero packet loss and no delay, but in reality, packet loss, delay, and instability are common, and bandwidth is often limited. Given this, you need to pay special attention to the following points when analyzing network conditions.

#### Packet loss<span id="packet_loss"></span>

In the graph, packet loss is represented by a red line.

| Packet Loss Rate                         | Network Conditions             |
| ------------------------------ | ------------------------ |
| = 0                            | Excellent                     |
| < 2%                           | Good                 |
| &gt; 5%                        | Poor                     |
| &gt; 10%（or constant packet loss） | Serious network congestion |

#### Bitrate<span id="bit_rate"></span>

Normally, the fluctuations of audio/video bitrate should be smaller than 10%. If **the bitrate experiences dramatic fall or fluctuations larger than 30%, it indicates network congestion or jitter**.
> ! Because the GOP duration of screen sharing is relatively long (5-10 seconds), normally, the bitrate follows a regular cycle, represented by a curve which peaks at keyframes.

- Upstream video bitrate and packet loss
  ![](https://main.qcloudimg.com/raw/04dbc42ef897b2d9e462109723d4bd83.png)
- The bitrate curve of screen sharing follows a cycle with regular peaks.
  ![](https://main.qcloudimg.com/raw/536e174c3bc1acf6405fa9b03cb26c19.png)

#### Frame rate<span id="frame_rate"></span>

Normally, video frame rate should stabilize at around 15 FPS or higher (5-10 FPS for screen sharing). **If the frame rate experiences fluctuations larger than 5 FPS or falls and stays below 10 FPS, it indicates network congestion or jitter**. When this happens, users experience lag. Points of excessively low frame rates are marked red in the graph.

- Upstream video frame rate (capture or send)
  ![](https://main.qcloudimg.com/raw/aece9e6339df38b2d043fc070c798543.png)
- Video rendering frame rate. Excessively low frame rates are marked red, with the lag time provided.
  ![](https://main.qcloudimg.com/raw/9d61cf98732bcd972542f2f46ba36aee.png)



### Viewing device status<span id="equipment"></span>

Stable device performance is necessary for a successful audio/video call. Preferably, the device uses a small amount of system resources, does not compete for resources with other devices, and collects data without interference. Pay attention to the following aspects when checking device status.

#### CPU usage<span id="cpu"></span>
Both system CPU usage and application CPU usage are displayed. Normally, system CPU usage should be lower than 50%. The lower, the better. If **system CPU usage exceeds 85%, the program may stop responding or respond slowly. This is marked by red lines in the graph.**
![](https://main.qcloudimg.com/raw/3685883ac4a44d78481359f17648485d.png)

#### Volume<span id="voice"></span>
- Audio **Capturing Volume** is the audio volume of data captured from the sender’s mic. **Fluctuations in audio capturing volume indicate that the mic is capturing audio and functioning normally**.
- Audio **Playback Volume** is the audio volume of data played back by the receiver’s speaker after encoding and rendering. **Fluctuations in audio playback volume indicate that the SDK has sent audio to the speaker and is functioning normally**.

The normal volume range is 40-80 dB. If the volume is lower than 40 dB, and the user cannot hear any audio, check for hardware failure or whether the user’s phone is muted.
![](https://main.qcloudimg.com/raw/5052ae41e76a81580c4dddf67433a2c2.png)

#### Resolution<span id="resolution"></span>
The resolutions of video and screen sharing are additional information used mainly to analyze relayed live streaming and playback of recorded streams. Fluctuations in the resolution indicate that viewers watching relayed live streams via [CDN](https://intl.cloud.tencent.com/zh/product/cdn), especially web users, may be experiencing issues caused by player incompatibility, such as frozen and blurry images.
![](https://main.qcloudimg.com/raw/422e0c787216954deb3b9c5deea97bdd.png)


>? [Resolution](#resolution), [bitrate](#bit_rate), and [frame rate](#frame_rate) are related to each other. Generally, when resolution is fixed, the higher the bitrate, the clearer the image; when bitrate is fixed, the higher the resolution, the blurrier the image. Set resolution, bitrate, and frame rate properly to ensure good video quality.

#### Client events
Client events correspond to the calling of SDK methods by the application and are usually used to help locate software problems, analyze bugs, as well as simulate scenarios by analyzing users’ operations. Pay attention to these client events:

- Entering/Exiting a room
- Enabling/Disabling the camera or mic
- Device change, such as switching cameras, connecting/disconnecting headphones, and connecting Bluetooth headphones.
- Starting/Stopping stream pushing or playback
- Muting/Unmuting audio or video
- Switching networks, for example, from 4G to Wi-Fi

Click **View Detailed Event** to open the event list and view the operations of key client events.
![](https://main.qcloudimg.com/raw/5caf7e8917835e124636327bc67e1d2f.png)
