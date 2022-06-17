CSS provides LVB as a professional, stable, and fast cloud streaming service for common use cases. You can integrate the MLVB SDK to apps, web, and other platforms to quickly enable live streaming.

[](id:app)

## Apps	
You can integrate the MLVB SDK with apps on iOS or Android clients for live push and playback.

- **Live push on apps**: support capturing camera or mobile phone screens and then pushing the content to the CSS platform using the RTMP protocol.
- **Live playback on apps**: support playback protocols including RTMP, HTTP-FLV, and HLS. You can integrate the MLVB SDK with LVB to quickly build live streaming apps. 

>? The MLVB SDK uses CSS, IM, TRTC and other services for low-latency audiovisual communication for multiple parties. It offers co-anchoring for interaction between viewers, and other viewers who don’t join co-anchoring can also watch the live streaming.


[](id:web)

## Web
You can use the following ways to achieve live push and playback on your websites:
- **Live push on web**: you can use the standard WebRTC protocol to design and mux streams, and insert code snippets to websites to enable live push. For details, please see [WebRTC Push](https://intl.cloud.tencent.com/document/product/267/41620).
> ! WebRTC push uses the Opus audio codec. If you use a standard live streaming protocol (RTMP, HTTP-FLV, or HLS) for playback, the CSS backend will automatically convert the audio streams to AAC format to ensure normal playback, which will incur audio transcoding fees. For details, please see [Live Transcoding > Audio Transcoding](https://intl.cloud.tencent.com/document/product/267/39604).


