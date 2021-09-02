As a lower-latency version of LVB, LEB provides superb **live streaming** experience with millisecond playback latency, far lower than that of live stream playback using traditional protocols.

> ! LEB uses the WebRTC protocol to ensure low latency. It adopts the Opus codec and does not support B-frames. If the original stream contains B-frames or the codec is not Opus, CSS backend will remove the B-frames and transcode the stream to Opus format, which will incur [standard transcoding fees](https://intl.cloud.tencent.com/document/product/267/39604).



[](id:app)

## Apps

You can integrate the MLVB SDK with apps on iOS and Android clients for live push and playback.

- **Live push on apps**: support capturing camera or mobile phone screens and then pushing the content to the CSS platform using the RTMP protocol. For details, please see [Publishing (Camera)](https://intl.cloud.tencent.com/document/product/1071) and [Publishing (Screen Recording)](https://intl.cloud.tencent.com/document/product/1071/39888).
- **Live playback on apps**: support WebRTC playback protocol. You can integrate the MLVB SDK with LEB to quickly achieve live streaming with low latency. For details, please see [Playback](https://intl.cloud.tencent.com/document/product/1071/38567).

>? The MLVB SDK uses CSS, IM, TRTC and other services for low-latency audiovisual communication for multiple parties. It offers co-anchoring for interaction between viewers, and other viewers who don’t join co-anchoring can also watch the live streaming. For details, please see [Co-anchoring](https://intl.cloud.tencent.com/document/product/1071/39888).



[](id:web)

## Web

You can use the following ways to achieve live push and playback on your websites:

- **Live push on web**: you can use the standard WebRTC protocol to design and mux streams, and insert code snippets to websites to enable live push. For details, please see [WebRTC Push](https://intl.cloud.tencent.com/zh/document/product/267/41620).
> ! WebRTC push uses the Opus audio codec. If you use a standard live streaming protocol (RTMP, HTTP-FLV, or HLS) for playback, the CSS backend will automatically convert the audio streams to AAC format to ensure normal playback, which will incur audio transcoding fees. For details, please see [Live Transcoding > Audio Transcoding](https://intl.cloud.tencent.com/document/product/267/39604). Audio transcoding will not be initiated when only LEB service is used.
- **Live playback on web**: we recommend you use the player SDK [TCPlayerLite](https://intl.cloud.tencent.com/document/product/266/7836) which supports playing back **LEB streams using the WebRTC protocol** on mobile and desktop browsers. Such playback delivers a superb streaming experience with millisecond latency, far lower than that of playback using traditional live streaming protocols.
> ! On a browser which does not support WebRTC, a WebRTC URL passed into the player will be converted to ensure normal playback. By default, WebRTC URLs are converted to HLS URLs on mobile browsers and HTTP-FLV URLs on desktop browsers.
