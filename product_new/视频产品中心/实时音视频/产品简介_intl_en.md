Built on Tencent's more than a decade of expertise in QQ audio/video call technologies, Tencent Real-Time Communication (TRTC) is a product developed by Tencent Cloud that leverages the WebRTC capabilities of Tencent Browsing Service (TBS) and TRTC SDK. It provides customers with cross-terminal and cross-platform real-time audio and video communication that features low cost, high quality, and customization.

## Product Architecture
The TRTC architecture is shown below:
![](https://main.qcloudimg.com/raw/994580a65420c260395034a544f63868.png)

## Supported Platforms
TRTC **supports a wide range of platforms**. The following lists how it is compatible with various platforms:

| Platform | SDK and Compatibility | Demo | Demo Source Code Download |
|------|------|------|------|
| iOS | iPhone and iPad on iOS 9.0 or above | Yes | Yes |
| Android | Android 4.1 (SDK API Level 16) at minimum; Android 5.0 (SDK API Level 21) or above is recommended. | Yes | Yes |
| Windows | Windows 7 or above | Yes | Yes |
| Mac OS | Mac machines on Mac OS X10.10 or above | Yes | Yes |
| Web | see [Quick Integration (Web)](https://intl.cloud.tencent.com/document/product/647/35096). | Yes | Yes |
| WeChat Mini Program | Mini Program Base Library 1.7.0 or above; WeChat on iOS 6.5.21 or above, or on Android 6.5.19 or above. | Yes | Yes |

>?
- To download TRTC SDK for various platforms, see [Downloading SDK](https://intl.cloud.tencent.com/document/product/647/34615).
- To try out Demos for various platforms, please see [Trying Out Demos](https://intl.cloud.tencent.com/document/product/647/35076).
- To download Demo source code for various platforms, log in to the [TRTC Console](https://console.cloud.tencent.com/rav), select a created application tab on the **Application List** page to go to the **Application Details** page, and then click **Getting Started**.

## Benefits

#### Low latency
TRTC offers a highly connected, reliable, and secure network across the globe. Leveraging our proprietary multi-addressing algorithms, TRTC has the ability to stream users' audio/video data to optimal nodes across the entire network. When a user logs in outside Mainland China, TRTC SDK connects the user to the nearest access point or edge server. With abundant high-bandwidth resources and globally-distributed edge servers, it can ensure **an average end-to-end latency of below 300 ms ** between countries/regions.

#### Low lag
TRTC reduces lags through intelligent QoS and optimized encoding, and is resilient against **a packet loss rate of over 40%** and **network jitter of over 1,000 ms*. Even with poor network condition, it can ensure a high-quality and stable audio/video communication.

#### High quality
TRTC **eliminates echoes and howling to deliver lossless audio quality, with a FHD video quality of up to 1920×1080**. Powered by Tencent Cloud's video processing algorithms and TBS's high compatibility based on X5 Blink kernel, TRTC enhances video definition and reduces mosaics, providing users on HTML5 webpages with an experience comparable to that on native apps.

#### Compatibility with multiple platforms
TRTC supports more than 5,000 types of devices on a wide range of platforms. With TRTC, you can initiate, receive, or disconnect from audio/video calls through HTML5 pages or Mini Programs on WeChat, mobile QQ, or QQ Browser. It also supports audio/video calls through web pages or SDK-integrated apps on PC, Mac, and mobile phones. 
