Copyright infringement has grown alongside the rapid development of the online video industry, making copyright protection a major concern of content owners.

## Commercial DRM Solutions

Commercial DRM solutions use playback licenses to offer high-level content protection. Before a device can play a DRM-encrypted video, it must obtain a license (which includes information such as the decryption key, validity period of the key, and device information) to decrypt the video.

The strengths of commercialDRM solutions are as follows:
- The key can only be read by the content decryption module (CDM).
- Each license can be used for only one device.
- You can set the validity period of a license.
- Support hardware-based TEE and decoding.
- Trusted by top content owners including Disney and Hollywood studios.

Widevine and FairPlay are two mainstream DRM solutions.

| DRM Solution | Adaptive Bitrate Streaming Protocol | Player and Browser                                            |
| ------------------- | -------------------- | ---------------------------------------------------------- |
| Widevine            | HLS, DASH            | Android player, Chrome, Firefox, Edge, Opera |
| FairPlay            | HLS                  | iOS player, Safari                           |

## VOD DRM Overview

Commercial DRM solutions provide high-level protection for your video content, but may be difficult to use from scratch. VOD offers an easy-to-use DRM scheme that is built on commercial DRM solutions and integrates a full range of features including DRM encryption, license management, license distribution, decryption, and playback.

Below is the workflow of the VOD DRM scheme:

![](https://qcloudimg.tencent-cloud.cn/raw/ae358775adc9711065239394b246ab50.png)

## Integration Guide

For directions on how to quickly integrate the VOD DRM scheme, see [Playing DRM-Encrypted Videos](https://intl.cloud.tencent.com/document/product/266/46642).

