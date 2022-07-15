Copyright infringement has grown alongside the rapid development of the online video industry, making copyright protection a major concern of content owners.

Established DRM solutions use playback licenses to offer high-level content protection. Before a device can play a DRM-encrypted video, it must obtain a license (which includes information such as the decryption key, validity period of the key, and device information) to decrypt the video.

The strengths of established DRM solutions are as follows:

<ul>
<li>The key can only be read by the content decryption module (CDM).</li>
<li>Each license can be used for only one device.</li>
<li>You can set the validity period of a license.</li>
<li>Support hardware-based TEE and decoding.</li>
</ul>

Widevine and FairPlay are two mainstream DRM solutions.

| DRM Solution | Adaptive Bitrate Streaming Protocol | Player and Browser                                               |
| ------------ | ---------- | --------------------------------------------- |
| Widevine            | HLS, DASH            | Android player, Chrome, Firefox, Edge, Opera |
| FairPlay            | HLS                  | iOS player, Safari                           |

## VOD DRM Scheme
Established DRM solutions provide high-level protection for your video content, but may be difficult to use from scratch. VOD offers an easy-to-use DRM scheme that is built on established DRM solutions and integrates a full range of features including DRM encryption, license management, license distribution, decryption, and playback.

Below is the workflow of the VOD DRM scheme:
![](https://qcloudimg.tencent-cloud.cn/raw/ae358775adc9711065239394b246ab50.png)

## Using VOD DRM Scheme
If you want to use VOD’s DRM scheme, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). DRM fees will be incurred for using the scheme.

## Billing
The following fees may be incurred for using VOD’s DRM scheme:

- Transcoding fees: Videos are transcoded during DRM encryption, which incurs transcoding fees.
- Storage fees: The videos generated after transcoding take up storage space, which incurs storage fees.
- DRM playback fees: DRM playback fees are charged based on the number of license requests to play DRM-encrypted videos.

For the pricing details, see [Daily Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/266/14666).
