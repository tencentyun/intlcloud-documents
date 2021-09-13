## What Is "Instant Streaming"?

**Instant streaming** means keeping the time it takes for the first video frame to reach audience after playback starts to a few hundred milliseconds.

This is mainly achieved through the optimization of cloud services and the adaptation of the player. If you use LiteAVSDK together with Tencent Video Cloud to implement live streaming, the video loading time can be cut to around **200 ms** or even lower in case of excellent downstream network conditions.

## How to Achieve Instant Streaming? 
### App
You can use the [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38150) plus the FLV playback protocol to achieve instant streaming.
- **HTTP-FLV playback protocol**
HTTP-FLV is currently the most widely used playback protocol in the streaming industry. Because it organizes data in simple formats, audio and video data can be obtained the moment server connection is set up. In contrast, with RTMP, due to the several handshakes required for connection, its streaming speed is slower than FLV.
- **Tencent Cloud LiteAVSDK**
The way instant streaming is achieved on the cloud side is quite simple. With a GOP (containing at least one keyframe) always cached on the server, the player can obtain a keyframe (I frame) right after it connects to the server, and can then decode and play the frame. However, there’s a downside to caching GOPs in the cloud. The player may be overwhelmed with audio and video data of a few seconds upon connection, resulting in marked playback latency.
In addition to instant streaming, a good player should be capable of **latency control**, that is, automatically adjusting playback latency to an acceptable level (e.g., within 1s) without compromising playback experience. Tencent Cloud’s LiteAVSDK performs well in this respect. It even allows you to choose a latency control mode based on your needs. For details, please see [iOS](https://intl.cloud.tencent.com/document/product/1071/38159#Delay) and [Android](https://intl.cloud.tencent.com/document/product/1071/38160#Delay).

### Desktop browser
Most desktop browsers use Flash Player for video playback (Chrome supports MSE now, but it does not have a notable advantage against Flash Player). The playback policy of Flash Player involves **forced caching**, making it difficult for it to keep the video loading time within 1s. This is evident from the performance of mainstream video websites and live streaming platforms on desktop browsers.

### Mobile browser
- **iPhone**
Safari works well with HLS (M3U8). It uses iPhone's decoding chip to facilitate video playback. Usually, you do not have to worry about the video loading speed as long as DNS caches are available, but this is limited to the iOS platform.
- **Android**
There is great uncertainty to streaming performance on Android, which varies with browser and browser version. For example, QQ Browser and WeChat’s built-in browser use Tencent’s proprietary X5 engine and therefore differ significantly from other browsers in terms of instant streaming.

