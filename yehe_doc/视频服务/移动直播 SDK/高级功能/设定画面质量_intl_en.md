## Sample Code
Regarding frequently asked questions among developers, Tencent Cloud offers an easy-to-understand API example project, which you can use to quickly learn how to use different APIs.

| Platform |                         GitHub Address                          |
| :------: | :----------------------------------------------------------: |
| iOS| [GitHub]((https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC)) |
| Android  | [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |

## Features
LiveAVSDK uses the `setVideoQuality` API provided by `V2TXLivePusher` to set video quality.

### API definition
You can use `setVideoQuality` to set the resolution and resolution mode (landscape/portrait) of published video.
```
int setVideoQuality(V2TXLiveVideoResolution resolution, V2TXLiveVideoResolutionMode resolutionMode);
```
#### Parameters
| Parameter | Type | Description |
|-----|-----|-----|
| resolution | [V2TXLiveVideoResolution](#V2TXLiveVideoResolution) | Video resolution |
| resolutionMode | [V2TXLiveVideoResolutionMode](#V2TXLiveVideoResolutionMode) | Resolution mode (landscape/portrait) |

- **Enumerated values of V2TXLiveVideoResolution:**[](id:V2TXLiveVideoResolution)
<table>
<tr><th>Value</th><th>Description</th>
</tr><tr>
<td>V2TXLiveVideoResolution160x160</td>
<td>Resolution: 160 × 160; bitrate: 100-150 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution270x270</td>
<td>Resolution: 270 × 270; bitrate: 200-300 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution480x480</td>
<td>Resolution: 480 × 480; bitrate: 350-525 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution320x240</td>
<td>Resolution: 320 × 240; bitrate: 250-375 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution480x360</td>
<td>Resolution: 480 × 360; bitrate: 400-600 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution640x480</td>
<td>Resolution: 640 × 480; bitrate: 600-900 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution320x180</td>
<td>Resolution: 320 × 180; bitrate: 250-400 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution480x270</td>
<td>Resolution: 480 × 270; bitrate: 350-550 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution640x360</td>
<td>Resolution: 640 × 360; bitrate: 500-900 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution960x540</td>
<td>Resolution: 960 × 540; bitrate: 800-1500 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution1280x720</td>
<td>Resolution: 1280 × 720; bitrate: 1000-1800 Kbps; frame rate: 15 fps</td>
</tr><tr>
<td>V2TXLiveVideoResolution1920x1080</td>
<td>Resolution: 1920 × 1080; bitrate: 2500-3000 Kbps; frame rate: 15 fps</td>
</tr></table>

- **Enumerated values of V2TXLiveVideoResolutionMode:**[](id:V2TXLiveVideoResolutionMode)
<table>
<tr><th>Value</th><th>Description</th>
</tr><tr>
<td>V2TXLiveVideoResolutionModeLandscape</td>
<td>Resolution in landscape mode: V2TXLiveVideoResolution640_360 + V2TXLiveVideoResolutionModeLandscape = 640 × 360</td>
</tr><tr>
<td>V2TXLiveVideoResolutionModePortrait</td>
<td>Resolution in portrait mode: V2TXLiveVideoResolution640_360 + V2TXLiveVideoResolutionModePortrait = 360 x 640</td>
</tr></table>

### Recommended settings

|    Application Scenario    |                           resolution                            | resolutionMode |
| :------------: | :----------------------------------------------------------: | :-----------: |
|    Live showroom    |<li/>V2TXLiveVideoResolution960x540<li/>V2TXLiveVideoResolution1280x720 |      Landscape or portrait       |
|    Live game streaming    |                V2TXLiveVideoResolution1280x720                |      Landscape or portrait      |
| Mic connect (primary-stream image) |             V2TXLiveVideoResolution640x360             |      Landscape or portrait      |
| Mic connect (small image) |             V2TXLiveVideoResolution480x360              |      Landscape or portrait       |
|    Blu-ray streaming    |                V2TXLiveVideoResolution1920x1080                |      Landscape or portrait       |


## Note

For smoother mic connect experience, after mic connect starts, please call `setVideoQuality()` to set the host’s resolution to `V2TXLiveVideoResolution640x360` and the mic-connecting audience’s resolution to `V2TXLiveVideoResolution480x360`. After mic connect ends, you can call `setVideoQuality()` again to set the resolutions to previous values.

## FAQs

### 1. Why is the video delivered to audience not as clear as that watched by the host?
The video watched by the host is the raw data captured by the camera after pre-processing (beauty filter application, mirroring, clipping, etc.) and therefore is of high quality. However, the video watched by audience has been compressed and then decoded by the codec. Encoding compromises video quality (the lower the target resolution, the more the video is compressed), which is why the video delivered to audience is not as clear as that watched by the host.

### 2. Why does `V2TXLivePusher` sometimes publish video at a resolution of 368 × 640 or 544 × 960?
If you enable hardware acceleration, the video published may have atypical resolutions such as 368 × 640 or 544 × 960. This is because some hardware encoders do not allow resolutions that aren’t a multiple of 16. You can change the fill mode of the player to get rid of black bars.
