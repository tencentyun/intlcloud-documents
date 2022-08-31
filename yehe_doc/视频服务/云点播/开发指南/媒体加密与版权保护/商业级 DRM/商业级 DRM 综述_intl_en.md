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

Currently, VOD supports two DRM licensing schemes:

- VOD DRM: The licensing service is provided by Tencent Cloud VOD.
- Third-party DRM: The licensing service is provided by SMDC.

You can choose the scheme that fits your needs.

## VOD DRM Scheme

Established DRM solutions provide high-level protection for your video content, but may be difficult to implement from scratch. VOD offers an easy-to-use DRM scheme that is built on established DRM solutions and integrates a full range of features including DRM encryption, license management, license distribution, decryption, and playback.

The encryption and decryption process is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/ae358775adc9711065239394b246ab50.png)

We offer a [tutorial]() that uses an example to show you how to quickly implement the scheme.

## Third-Party DRM Scheme

If you use this scheme, VOD will offer services including transcoding, encryption, storage, and CDNs, while the third-party DRM service provider [SDMC](https://www.xmediacloud.com/product-drm/) will offer certificate management and license distribution services.

The encryption and decryption process is as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/92759b5011065b2685c8b70d60593d9d.png)


We offer a [tutorial](https://intl.cloud.tencent.com/document/product/266/46642) that uses an example to show you how to quickly implement the scheme.

## Billing
The following fees may be incurred for using the DRM feature:

- Transcoding fees: Videos are transcoded during DRM encryption, which incurs transcoding fees.
- Storage fees: The videos generated after transcoding take up storage space, which incurs storage fees.
- DRM licensing fee: For a device to play a DRM-encrypted video, you must supply it with a license. This will incur DRM licensing fees. If you use the third-party DRM scheme, this fee will be charged by the third-party DRM service provider.

For the pricing details, see [Daily Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/266/14666).
