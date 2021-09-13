## Scenario 1: Live Showroom

### Step 1. Update the SDK 
Each new version of the SDK we release features improved beauty filters. For example:
- In 1.9.1, we updated the beauty filter engine, gave a major boost to foreground focus, exposure, the beauty filter algorithm, etc., and improved the performance of the beauty filter module.
- In 1.9.2, we optimized noise reduction, reducing the noise in night pictures while highlighting figures.
- In 2.0.0, we introduced new filters to iOS to fix the yellow screen tint.
- ... ...
  
### Step 2. Set video quality
The local video watched by hosts and the video delivered to audience are of different quality.
- **Host versus Audience**:  
The video watched by a host is video rendered directly on to the host’s phone screen after capturing and is therefore of high quality. The video must be **encoded**, **transmitted over the internet**, and then **decoded** before it reaches audience. Encoding reduces video quality, which is why the video delivered to audience is not as clear as that watched by the host. Improper parameter settings can cause major loss of video quality. A typical example is setting the resolution high and bitrate low, which results in blurry and pixelated video. 
- **setVideoQuality**
In version 1.9.1, we introduced the `setVideoQuality` API to `TXLivePusher` and offered three video quality modes for you to choose from. The **HD** mode is ideal for live showrooms. For details, please see [iOS](https://intl.cloud.tencent.com/document/product/1071/38157) and [Android](https://intl.cloud.tencent.com/document/product/1071/38158).

### Step 3. Set manual exposure on Android
The same beauty filter algorithm may yield different visual effects on different Android phones due to exposure differences.
On iOS, the SDK uses the system’s auto exposure. However, Android devices can vary greatly from each other, and many low-end Android phones have poor auto exposure performance. Given this, we suggest that you add a slider that allows users to adjust exposure themselves to the UI of your Android project.
The TXLivePush::**setExposureCompensation** API in the RTMP SDK for Android can be used to adjust exposure. The parameter can be set to a floating point number from -1 to 1. `0` means to use the system’s auto exposure. `-1` means the lowest exposure level, and `1` the highest.


### Step 4. Add color filters
Filters are also important because different color filters create different atmospheres. Hosts should choose the color filter that matches their clothes or the light in the room.

The SDK has supported color filters since version 1.9.1. The new `setFilter` API in `TXLivePusher` is used to set filters. We offer eight free filters, which have been integrated into the demo.

### Step 5. Fix video pixelation
On Android, the video published by the RTMP SDK may be heavily pixelated, especially when there are moving objects. This is a common problem with hardware encoding on Android, to which there are two solutions.
- **For scenarios sensitive to battery usage**
When the bitrate is set low, the hardware encoder of Android tends to dramatically reduce video quality to ensure bitrate stability. Therefore, to improve video quality, you can increase the bitrate of published video or call `setVideoQuality` to set the resolution to **HD**. This is the solution recommended if you want to keep the battery usage of your application low.
- **For scenarios sensitive to bandwidth usage**
 If you want to keep the bandwidth usage of your application low, instead of increasing the bitrate, we suggest that you disable hardware acceleration. For detailed instructions, please see [setHardwareAcceleration](https://cloud.tencent.com/document/product/454/34771#sethardwareacceleration).

### Step 6. Disable self-adaptation
The **AutoAdjustBitrate** option in **TXLivePushConfig** is used to enable/disable self-adaptation. If self-adaptation is enabled, when a host’s network conditions turn bad, the SDK will reduce video quality to ensure smoothness. This works well for game streaming scenarios because game streaming audience prioritize smoothness over video quality. If a host’s network fluctuates, they would rather sacrifice video quality for smoothness (frame rate). However, the self-adaptation feature **is not suitable** for live showroom scenarios, where clarity matters more than smoothness. Self-adaptation is a common reason why video quality is high in some rooms and low in others.
Therefore, in live showroom scenarios, we suggest that you disable self-adaptation and [inform hosts](https://intl.cloud.tencent.com/document/product/1071/39362#checking-sdk-status-metrics) when their network fluctuates. The latter solves the fundamental issue.

## Scenario 2: Live Game Streaming
### Simple solution
On the starting page of live streaming, provide three video quality options – SD, HD, and FHD – **for hosts to choose from**. Most game streaming hosts have the expertise to determine the video quality that best fits their games. 

| Option | Resolution | Frame Rate (fps) | Bitrate (Kbps) |
|---------|---------|---------|---------|
| SD | VIDEO_RESOLUTION_TYPE_360_640 | 20 | 800 |
| HD | VIDEO_RESOLUTION_TYPE_540_960 | 20 | 1000 |
| FHD | VIDEO_RESOLUTION_TYPE_720_1280 | 20 | 1800 |

>! In live game streaming, you are not advised to set the frame rate to below 20 fps as it can cause severe video stutter for audience.

### Advanced solution
Use different resolutions and bitrates for different games. For example:
- **Clash Royale** - Since the video of the game does not change a lot, we recommend that you set the resolution to **960 × 540** and bitrate to 800-1000 Kbps.
- **Fish Hunter** - Since the video of the game changes a lot, we recommend that you set the resolution to **960 × 540** and bitrate to a level higher than that for Clash Royale, for example, 1200-1500 Kbps.
- **Temple Run** - Since the video of the game changes dramatically, to prevent pixelation, we recommend that you set the resolution to **640 × 360** and bitrate to a rather high level, for example, 2000 Kbps.

## Tips

### 1. Higher resolution does not necessarily mean higher video quality.
If the bitrate is fixed, for example, at 800 Kbps, then **the higher the resolution, the more demanding it will be on the encoder**. To display enough pixels, the encoder may have to reduce color information or pixelate a video. Given this, a 1080p video of 2 GB may not be as clear as a 720p video of the same size.
If audience watch videos on the small screens of mobile phones, they probably won’t see much difference between **a resolution of 960 × 540 px plus a bitrate of 1000 Kbps** and **a resolution of 1280 x 720 px plus a bitrate of 1800 Kbps**. 

>! The difference becomes noticeable if you watch the videos on a 32-inch LCD.

### 2. Keep the frame rate at 24 fps or lower.
If the bitrate is fixed, for example, at 800 Kbps, the higher the frame rate, the more a video will be compressed by the encoder. In other words, to achieve a high frame rate, the encoder has to reduce video quality. For camera-captured videos, a frame rate of 24 fps is already the most the human eye can see. In most cases, a frame rate of 20 fps can yield superior playback experience. 3D game players tend to believe that a higher frame rate (e.g., 60 or 120 fps) brings smoother experience. 
It should be pointed out that it is high **rendering frame rate**, rather than capturing frame rate, that games pursue, the purpose of which is to make 3D rendered videos as realistic as possible. However, when you use, for example, the camera of a mobile phone for streaming, video frames are captured, not simulated, and since objects in real life move continuously instead of frame by frame, a frame rate of 20 fps is enough.
For game streaming, a frame rate of 24 fps may be ideal, but you have to take into account issues such as encoding cost, phone heating, and CPU usage.

