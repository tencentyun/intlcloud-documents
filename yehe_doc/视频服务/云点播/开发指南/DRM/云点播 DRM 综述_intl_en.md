Copyright infringement has grown alongside the rapid development of the online video industry, making copyright protection a major concern of content owners.

## Established DRM Solutions

Established DRM solutions use playback licenses to offer high-level content protection. Before a device can play a DRM-encrypted video, it must obtain a license (which includes information such as the decryption key, validity period of the key, and device information) to decrypt the video.

The strengths of established DRM solutions are as follows:
- The key can only be read by the content decryption module (CDM).
- Each license can be used for only one device.
- You can set the validity period of a license.
- Support hardware-based TEE and decoding.
- Trusted by top content owners including Disney and Hollywood studios.

Widevine and FairPlay are two mainstream DRM solutions.

| DRM Solution | Adaptive Bitrate Streaming Protocol | Player and Browse                                             |
| ------------------- | -------------------- | ---------------------------------------------------------- |
| Widevine            | HLS, DASH            | Android player, Chrome, Firefox, Edge, Opera |
| FairPlay            | HLS                  | iOS player, Safari                           |

## VOD DRM Overview

Established DRM solutions provide high-level protection for your video content, but may be difficult to use from scratch. VOD offers an easy-to-use DRM scheme that is built on established DRM solutions and integrates a full range of features including DRM encryption, license management, license distribution, decryption, and playback.

Below is the workflow of the VOD DRM scheme:

1. <b>Upload</b>: Videos are uploaded to VOD via the console or using server-side APIs.
2. <b>Start video processing</b>: when the video is uploaded, adaptive bitrate streaming with encryption is specified. After the video is uploaded, the encryption process begins.
3. <b>Get the key</b>: VOD gets the encryption key from the KMS module.
4. <b>Encrypt and save the videos</b>: VOD encodes and encrypts the videos and saves the outputs.
5. <b>Update the information</b>: The information of the encrypted videos is updated to the media asset management module.
6. <b>Get player signatures</b>: The VOD superplayer, which is integrated into your project, requests player signatures from your server.
7. <b>Get the download URLs</b>: The superplayer gets the download URLs of the videos from VOD.
8. <b>Download</b>: The superplayer downloads the content via the URLs.
9. <b>Get playback licenses</b>: The superplayer uses the signatures to request playback licenses.
10. <b>Decrypt and play the videos</b>: The superplayer uses the key to decrypt the content and plays the content.

![](https://qcloudimg.tencent-cloud.cn/raw/cac2fc608c14a604fd8145a8565a159a.png)

## Integration Guide

For directions on how to quickly integrate the VOD DRM scheme, see [Playing DRM-Encrypted Videos](https://intl.cloud.tencent.com/document/product/266/46642).
