## Push from Web

- You can push streams through **CSS Toolkit** > **[Web Push](https://intl.cloud.tencent.com/login)** in the CSS console. For details, please see [CSS Push > Web push](https://intl.cloud.tencent.com/document/product/267/31558).
- You can also use the `TXLivePusher` SDK to push streams. For details, please see [WebRTC Push](https://intl.cloud.tencent.com/document/product/267).

>? WebRTC push uses the Opus audio codec. If you use a standard live streaming protocol (RTMP, HTTP-FLV, or HLS) for playback, the system will automatically convert the streams to AAC, which will incur transcoding fees. For details, please see [Live Transcoding > Audio Transcoding](https://intl.cloud.tencent.com/document/product/267/39604).



## Playback on Web

We recommend that you use [TCPlayerLite](https://cloud.tencent.com/document/product/881/20207) of Tencent Cloud’s Player SDK for playback. Backed by Tencent Cloud’s strong backend capabilities and AI technologies, the powerful superplayer can play videos live or on demand. It integrates well with CSS and VOD, offers smooth and stable playback experience, and supports ad insertion and data monitoring, among others.

>? Currently, most mobile browsers on the market do not support HTTP-FLV playback. Given this, we recommend that you use HTTP-FLV for playback on desktop browsers and HLS for playback on mobile browsers.





