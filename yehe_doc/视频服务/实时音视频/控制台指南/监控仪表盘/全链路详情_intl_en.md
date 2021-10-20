End-to-end call details are the details of data transferred across the sender-receiver link. The preconditions of a smooth audio/video call are good network connections and stable device performance, which are what you should start with when checking the end-to-end details of a call.

## Directions

1. Log in to the TRTC console, click **[Monitoring Dashboard](https://console.cloud.tencent.com/trtc/monitor)**, and find the room whose call details you want to view.
2. Click the room ID or **View Call Details** on the right to go to the [Call Details](https://intl.cloud.tencent.com/document/product/647/39070) page.
3. On the receiver/sender page, select the ID of the user whose data you want to view, and go to the end-to-end details page via either of two methods.
	- On the **Receiver** page, click **Select sender to view details** on the right and select a user ID.
	- On the **Sender** page, click **View Details**.




## Information Displayed

The end-to-end details page shows the data of **Video**, **Audio**, and **Screen Sharing**, which can be viewed from the perspective of the receiver or sender.

You can analyze end-to-end data from [network conditions](#internet) and [device status](#equipment).

[](id:internet)
### Analyzing network conditions
Ideally, data should be transferred at high bandwidth, with zero packet loss and no delay, but in reality, packet loss, delay, and instability are common, and bandwidth is often limited. Given this, you need to pay special attention to the following points when analyzing network conditions.

[](id:packet_loss)
#### Packet loss
In the graph, packet loss is represented by a red line.

| Packet Loss Rate                         | Network Conditions             |
| ------------------------------ | ------------------------ |
| = 0                            | Excellent                     |
| < 2%                           | Good                 |
| &gt; 5%                        | Poor                     |
| &gt; 10% (or constant packet loss) | Serious network congestion |

[](id:bit_rate)
#### Bitrate
Normally, the fluctuations of audio/video bitrate should be smaller than 10%. **If the bitrate experiences dramatic fall or fluctuations larger than 30%, it indicates network congestion or jitter**.
> ! Because the GOP duration of screen sharing is relatively long (5-10 seconds), normally, the bitrate follows a regular cycle, represented by a curve which peaks at keyframes.

- Upstream bitrate and packet loss for screen sharing
- The bitrate curve of screen sharing follows a cycle with regular peaks.
  

[](id:frame_rate)
#### Frame rate
Normally, video frame rate should stabilize at around 15 fps or higher (5-10 fps for screen sharing). **If the frame rate experiences fluctuations larger than 5 fps or falls and stays below 10 fps, it indicates network congestion or jitter**. When this happens, users experience stutter. Periods of excessively low frame rates are marked red in the graph.

- Upstream video frame rate (capture or send)
- Video rendering frame rate. Excessively low frame rates are marked red, and the stutter time is provided.
  


[](id:equipment)
### View device status

Stable device performance is necessary for a successful audio/video call. Preferably, the device uses a small amount of system resources, does not compete for resources with other devices, and collects data without interference. Pay attention to the following aspects when checking device status.

[](id:cpu)
#### CPU usage
Both system CPU usage and application CPU usage are displayed. Normally, system CPU usage should be lower than 50%. The lower, the better. If **system CPU usage exceeds 85%, the application may stop responding or respond slowly. This is marked by red lines in the graph.**


[](id:voice)
#### Volume
- **Capturing volume** is the volume of audio captured from the sender's mic. **If it changes, it indicates that the SDK is capturing audio, i.e., the device functions properly.**
- **Playback volume** is the volume of decoded and rendered audio sent to the receiver’s speaker. **If it changes, it indicates that the SDK has sent audio to the speaker, i.e., the SDK functions properly.**

The normal volume range is 40-80 dB. If the volume is lower than 40 dB, and the user cannot hear any audio, check for hardware failure or whether the user’s phone is muted.


[](id:resolution)
#### Resolution
The resolutions of video and screen sharing are additional information used mainly to analyze relayed live streaming and the replay of recorded streams. Fluctuations in resolutions indicate that audience watching relayed live streams via [CDN](https://intl.cloud.tencent.com/product/cdn) or replaying recorded videos, especially web users, may be experiencing player compatibility issues such as stuttering or pixelated video.



>? [Resolution](#resolution), [bitrate](#bit_rate), and [frame rate](#frame_rate) are related to each other. Generally, when resolution is fixed, the higher the bitrate, the clearer the image; when bitrate is fixed, the higher the resolution, the blurrier the image. Set resolution, bitrate, and frame rate properly to ensure good video quality.

#### Client events
Client events correspond to the calling of SDK APIs by the application and are usually used to help locate software problems, analyze bugs, as well as simulate scenarios by analyzing users’ operations. Pay attention to these client events:

- Entering/Exiting a room
- Enabling/Disabling the camera or mic
- Device change, such as switching cameras, connecting/disconnecting headphones, and connecting Bluetooth headphones.
- Starting/Stopping stream pushing or playback
- Disabling/Enabling audio or video
- Switching networks, for example, from 4G to Wi-Fi

Click **View Detailed Event** to open the event list and view the operations of key client events.
