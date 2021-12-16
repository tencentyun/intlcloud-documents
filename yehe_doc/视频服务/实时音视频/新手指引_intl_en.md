## Quick Introduction to TRTC

- [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/35078)
- [Features](https://intl.cloud.tencent.com/document/product/647/35428)
- [Use Cases](https://intl.cloud.tencent.com/document/product/647/37713)
- [Basic Concepts](https://intl.cloud.tencent.com/document/product/647/37714)

[](id:pay)
## Billing Plans

TRTC offers two types of services: **basic services** and *value-added services*. 

<table>
<tr><th>Service Type</th><th>Use Case</th><th>Billing Details</th></tr >
<tr>
<td rowspan="4">Basic services</td>
<td>Interactive live audio streaming</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/">Billing of interactive live audio streaming</a></td>
</tr><tr>
<td>Interactive live video streaming</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/">Billing of interactive live video streaming</a></td>
</tr><tr>
<td>Audio call</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/">Billing of audio calls</a></td>
</tr><tr>
<td>Video call</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647">Billing of video calls</a></td>
</tr><tr>
<td rowspan="2">Value-added services</td>
<td>On-cloud recording</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38385">Billing of on-cloud recording</a></td>
</tr><tr>
<td>On-Cloud MixTranscoding</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38929">Billing of On-Cloud MixTranscoding</a></td>
</tr>
</table>




## Development Support
[](id:demo)
### Free Demos

TRTC offers free demos for **iOS**, **Android**, **macOS**, **Windows**, **Web**, **Electron**, and **Flutter**. For details, see [Free Demo](https://intl.cloud.tencent.com/document/product/647/35076).

[](id:sdk)
### SDK download

TRTC is one of Tencent Cloud’s LiteAV products. Because all LiteAV products use the same underlying modules, integrating more than one LiteAV SDK into the same project will result in a “duplicate symbol” error. For this, we provide different editions of the SDK, including **Lite (TRTC)**, **Professional**, and **Enterprise**, which come with different capabilities. You can choose the one that fits your needs.

| Edition                                                     | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Lite (TRTC)](https://intl.cloud.tencent.com/document/product/647/34615) | The Lite Edition integrates the TRTC and live playback (TXLivePlayer) features only. It adds the least to the size of the app installation package and is suitable for clients who need TRTC features only. |
| [Professional](https://intl.cloud.tencent.com/document/product/647/34615) | The Professional Edition integrates multiple key video/audio features of Tencent Cloud, including TRTC, [MLVB](https://intl.cloud.tencent.com/product/mlvb), [UGSV](https://intl.cloud.tencent.com/product/ugsv), etc. This integrated edition adds less to the size of the app installation package than two independent SDKs do because many underlying modules are shared among the SDKs. It is also free of the duplicate symbol issue. |
| [Enterprise](https://intl.cloud.tencent.com/document/product/647/34615) | On top of all the features included in the Professional Edition, the Enterprise Edition integrates the AI beauty filter component (value-added service) and supports the use of the eye enlarging and face slimming filters, animated stickers, widgets, etc. |

> ? See [SDK Download](https://intl.cloud.tencent.com/document/product/647/34615) for a comparison of the three editions.


[](id:api)
### API integration

- **Client APIs:** you can implement different features by calling SDK-side APIs on platforms including [iOS](https://intl.cloud.tencent.com/document/product/647/35119), [macOS](https://intl.cloud.tencent.com/document/product/647/35119), [Android](https://intl.cloud.tencent.com/document/product/647/35125), [Windows(C++)](https://intl.cloud.tencent.com/document/product/647/35131), [Unity](https://intl.cloud.tencent.com/document/product/647/40139), [Web](https://intl.cloud.tencent.com/document/product/647/35143), [Electron](https://intl.cloud.tencent.com/document/product/647/35141), and [Flutter](https://intl.cloud.tencent.com/document/product/647/39169).
- **Server APIs:** you can call API 3.0 to implement features including [call quality monitoring](https://intl.cloud.tencent.com/document/product/647/36754), [stream mixing and transcoding](https://intl.cloud.tencent.com/document/product/647/37760), and [room management](https://intl.cloud.tencent.com/document/product/647/34268).



## Getting Started
[](id:demo_guide)
### Demo quick start

The TRTC console offers demo source code for different platforms. See the documents below for how to run the demos.

| Platform       | Document                                                     |
| ---------- | ------------------------------------------------------------ |
| iOS and macOS    | [Demo Quick Start (iOS & macOS)](https://intl.cloud.tencent.com/document/product/647/35086) |
| Android    | [Demo Quick Start (Android)](https://intl.cloud.tencent.com/document/product/647/35084) |
| Windows    | [Demo Quick Start (Windows)](https://intl.cloud.tencent.com/document/product/647/35085) |
|Web | [Demo Quick Start (Web)](https://intl.cloud.tencent.com/document/product/647/35607) |
| Electron   | [Demo Quick Start (Electron)](https://intl.cloud.tencent.com/document/product/647/35089) |
- [Demo Quick Start (Flutter)](https://intl.cloud.tencent.com/document/product/647/39243)

[](id:sdk_guide)
### SDK quick integration

After downloading the TRTC SDK, you can integrate it into your project. For detailed instructions, see the documents below.

| Platform       | Document                                                     |
| ---------- | ------------------------------------------------------------ |
| iOS        | [SDK Quick Integration (iOS)](https://intl.cloud.tencent.com/document/product/647/35092) |
| macOS        | [SDK Quick Integration (macOS)](https://intl.cloud.tencent.com/document/product/647/35094) |
| Android    | [SDK Quick Integration (Android)](https://intl.cloud.tencent.com/document/product/647/35093) |
| Windows    | [SDK Quick Integration (Windows)](https://intl.cloud.tencent.com/document/product/647/35095) |
| Web | [SDK Quick Integration (Web)](https://intl.cloud.tencent.com/document/product/647/35096) |
| Electron   | [SDK Quick Integration (Electron)](https://intl.cloud.tencent.com/document/product/647/35097) |
| Flutter | [SDK Quick Integration (Flutter)](https://intl.cloud.tencent.com/document/product/647/35098) |

[](id:web_guide)
### Quick TWebLive run

TRTC offers an all-inclusive free demo for the TWebLive component. See [WebRTC-based Streaming](https://intl.cloud.tencent.com/document/product/647/38172) for how to integrate the component.

[](id:sence)
##Scenario-specific Practice

TRTC, along with other Tencent Cloud products, offers free demos for a wide range of live streaming scenarios.

<table>
<tr><th width="17%">Scenario</th><th>Supported Features</th><th width="20%">Document</th>
</tr><tr>
<td>Group video call</td>
<td>Co-anchoring, offline call answering, etc. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36065" target="_blank">Real-Time Video Call</a></td>
</tr><tr>
<td>Group audio call</td>
<td>Co-anchoring, offline call answering, etc. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36067" target="_blank">Real-Time Audio Call</a></td>
</tr><tr>
<td>Interactive live streaming</td>
<td>Co-anchoring, anchor competition, low-latency watch, on-screen comments, etc.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36060" target="_blank">Interactive Live Video Streaming</a></td>
</tr><tr>
<td>Real-time interactive teaching</td>
<td>Teaching modes: video, audio, screen sharing, etc.; interactions: asking questions, hand raising, inviting to speak, ending Q&A, etc. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37278" target="_blank">Real-Time Interactive Teaching</a></td>
</tr><tr>
<td>Video conferencing</td>
<td>Screen sharing, beauty filters, low-latency conferencing, etc.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37284" target="_blank">Video Conferencing</a></td>
</tr><tr>
<td>Audio chat room</td>
<td>Mic management, low-latency audio interaction, text chat, etc.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37287" target="_blank">Audio Chat Room</a></td>
</tr></table>

[](id:console)
## Console Guide
| If you want to                                         | Please Read                                                   |
| :--------------------------------------------------------- | :----------------------------------------------------------- |
| View your usage of TRTC’s **audio/video interaction** and **on-cloud recording** services | Usage Statistics |
| View call quality statistics of a TRTC room via the dashboard               | Dashboard |
| Download the demo source code and have a quick run of the demo                       | [Demo Quick Run](https://intl.cloud.tencent.com/document/product/647/39073) |
| Generate a UserSig online or verify an existing UserSig         | [UserSig Generation and Verification](https://intl.cloud.tencent.com/document/product/647/39074)                |
| Create an application |  
| Enable relayed push, on-cloud recording or advanced permission control for an application        | [Function Configuration](https://intl.cloud.tencent.com/document/product/647/39080) |
| Add a custom image to be set as the background displayed during on-cloud stream mixing            | [Material Management](https://intl.cloud.tencent.com/document/product/647/39081) |
| Configure a callback key and address based on your actual needs | [Callback Configuration](https://intl.cloud.tencent.com/document/product/647/39559) |



[](id:faq)
## FAQs

-  [What ports or domain names do I need to add to the allowlist of a native SDK?](https://intl.cloud.tencent.com/document/product/647/35164)
-  [How do I reduce the size of an installation package for iOS/Android?](https://intl.cloud.tencent.com/document/product/647/35165)
- [**How do I get a key?**](https://intl.cloud.tencent.com/document/product/647/35166)
-  [What are the differences among TRTC Lite, Professional, and Enterprise?](https://intl.cloud.tencent.com/document/product/647/36057) 
-  [What is a `RoomID` in TRTC? What is its value range?](https://intl.cloud.tencent.com/document/product/647/36057) 
-  [Can Android and web users call each other?](https://intl.cloud.tencent.com/document/product/647/37341) 
-  [Which browsers support the SDK for desktop browsers?](https://intl.cloud.tencent.com/document/product/647/37340) 

> ? For more Q&As, please see [FAQs](https://intl.cloud.tencent.com/document/product/647/36058).


## Feedback and Suggestion

If you have any questions about TRTC, contact us via the following channels.

- If your question is about documents, for example, the content or a link in the documents, click **Help** at the bottom right and then click **Send Feedback** to provide your feedback.
- If you have questions about the product, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
