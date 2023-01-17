A player signature is used to authorize a playback device to play videos. If your application playback service issues a valid signature to a device (step 6 in the figure below), the device will be able to play the video within the signature’s validity period.
<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="700" />

This document describes the parameters of a player signature and how to generate a signature.

## Signature Parameters[](id:p0)

| Parameter         | Required | Type    | Description                                                         |
| ---------------- | ---- | ------- | ------------------------------------------------------------ |
| appId            | Yes   | Integer | The VOD AppID.                                             |
| fileId           | Yes   | String  | The file ID.                                                |
| contentInfo | Yes | Object | The content of the specified file ID. For the structure of this parameter, see [ContentInfo](#p1). Three types of content are supported: <li> [Adaptive bitrate](https://intl.cloud.tencent.com/document/product/266/33942) audio/video, which may or may not be encrypted</li><li>[Transcoded](https://intl.cloud.tencent.com/document/product/266/33938) audio/video</li><li>[Uploaded](https://intl.cloud.tencent.com/document/product/266/9760) original audio/video </li>|
| currentTimeStamp | Yes   | Integer | The current time (Unix timestamp).                                   |
| expireTimeStamp | No | Integer | The expiration time (Unix timestamp) of the distributed signature. If this parameter is left empty, the signature will never expire. |
| urlAccessInfo | No | Object | The playback URL access parameters, including [key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986) parameters, the playback domain, and the protocol. For the structure of this parameter, see [UrlAccessInfo](#p4). |
| drmLicenseInfo | No | Object | The DRM configuration. For the structure of this parameter, see [DrmLicenseInfo](#p5). |

#### ContentInfo[](id:p1)

| Parameter              | Required | Type            | Description                                                         |
| --------------------- | ---- | --------------- | ------------------------------------------------------------ |
| audioVideoType | Yes | String | The type of audio/video played. Valid values: <li>`RawAdaptive`: Unencrypted [adaptive bitrate](https://intl.cloud.tencent.com/document/product/266/33942) output</li><li>`ProtectedAdaptive`: Private protocol- or DRM-encrypted [adaptive bitrate](https://intl.cloud.tencent.com/document/product/266/33942) output<li>`Transcode`: [Transcoding](https://intl.cloud.tencent.com/document/product/266/33938) output</li><li>`Original`: [Uploaded](https://intl.cloud.tencent.com/document/product/266/9760) original audio/video</li> |
| rawAdaptiveDefinition | No | Integer | The ID of the unencrypted [adaptive bitrate](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF) template allowed. This parameter is valid and required if `audioVideoType` is `RawAdaptive`. |
| drmAdaptiveInfo | No | Object | The ID of the encrypted [adaptive bitrate](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF) template allowed. This parameter is valid and required if `audioVideoType` is `ProtectedAdaptive`. For its structure, see [DRMAdaptiveInfo](#p2). |
| transcodeDefinition | No | Integer | The ID of the [transcoding](https://intl.cloud.tencent.com/document/product/266/33938#.3Ca-id.3D.22zm.22.3E.3C.2Fa.3E.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF) template allowed. This parameter is valid and required if `audioVideoType` is `Transcode`. |
| imageSpriteDefinition | No | Integer | The ID of the [image sprite](https://intl.cloud.tencent.com/document/product/266/33940) template, which is used to generate thumbnail previews. |
| resolutionNames | No | Array of Object | The names of different streams (different resolutions) displayed in the player. For its structure, see [ResolutionNameInfo](#p3). If you do not specify this parameter or leave it empty, the following will be used:</br>`MinEdgeLength`: 240, `Name`: 240P</br>`MinEdgeLength`: 480, `Name`: 480P</br>`MinEdgeLength`: 720, `Name`: 720P</br>`MinEdgeLength`: 1080, `Name`: 1080P</br>`MinEdgeLength`: 1440, `Name`: 2K</br>`MinEdgeLength`: 2160, `Name`: 4K</br>`MinEdgeLength`: 4320, `Name`: 8K|


#### DRMAdaptiveInfo[](id:p2)

| Parameter              | Required | Type            | Description                                                         |
| --------------------------- | ---- | ------- | ------------------------------------------------------------ |
| privateEncryptionDefinition | No | Integer | The ID of the [adaptive bitrate template](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF) used when [DrmType](https://www.tencentcloud.com/document/product/266/34187#AdaptiveDynamicStreamingTemplate) is `SimpleAES`. |
| widevineDefinition | No | Integer | The ID of the [adaptive bitrate template](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF) used when [DrmType](https://www.tencentcloud.com/document/product/266/34187#AdaptiveDynamicStreamingTemplate) is `Widevine`. |
| fairPlayDefinition | No | Integer | The ID of the [adaptive bitrate template](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF) used when [DrmType](https://www.tencentcloud.com/document/product/266/34187#AdaptiveDynamicStreamingTemplate) is `FairPlay`. |

#### ResolutionNameInfo[](id:p3)

| Parameter         | Required | Type    | Description                                                         |
| ------------- | ---- | ------- | -------------------------- |
| MinEdgeLength | Yes | Integer | The video short side (px).|
| Name          | Yes   | String  | The stream name.                 |

#### UrlAccessInfo[](id:p4)

| Parameter         | Required | Type    | Description                                                         |
| -------- | ---- | ------- | ------------------------------------------------------------ |
| t | No | String | <ul style="margin:0;"><li>A hexadecimal string indicating the URL expiration time</li><li>For the valid values and other information, see the `t` parameter of [hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).</li><li>If this parameter is left empty, the URL will never expire.</li></ul>|
| exper | No | Integer | <ul style="margin:0;"> <li>The preview duration in decimal seconds.</li><li>The preview duration cannot be shorter than 30 seconds.</li><li>For its valid values and other information, see the `exper` parameter of [hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).</li></ul> |
| rlimit | No | Integer | <ul style="margin:0;"><li>The maximum number (decimal) of IP addresses allowed for playback.</li><li>For its valid values and other information, see the `rlimit` parameter of [hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).</li></ul> |
| us | No | String | <ul style="margin:0;"><li>The URL ID, which can uniquely identify a link.</li><li>For its valid values and other information, see the `us` parameter of [hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).</li></ul> |
| domain | No | String | The playback domain. If this is not specified or `Default` is passed in, the [default distribution domain](https://intl.cloud.tencent.com/document/product/266/35768) will be used. |
| scheme | No | String | The playback scheme. If this is not specified or `Default` is passed in, the [default distribution configuration](https://intl.cloud.tencent.com/document/product/266/35768) will be used. Other valid values:<ul style="margin:0;"><li>HTTP</li><li>HTTPS</li></ul>|

#### DrmLicenseInfo[](id:p5)

| Parameter              | Required | Type            | Description                                                         |
| ----------------- | ---- | --------------- | ------------------------------------------------------------ |
| persistent        | No   | String          | Whether to allow persistent storage of DRM playback licenses by playback devices. Valid values:<ul style="margin:0;"><li>`ON`: Allow;</li><li>`OFF` : Do not allow</li></ul>The default value is `OFF`. |
| rentalDuration    | No   | Integer         | The allowed storage time (seconds) of DRM playback licenses when `persistent` is `ON`. If this is not specified, there will be no limit on the storage time. |
| forceL1TrackTypes | No   | Array of String | The track type that must use the L1 security level when Widevine is used. For other track types, Widevine L3 will be used. Valid values: <ul style="margin:0;"><li>`AUDIO`: Audio tracks;</li><li>`SD`: Video tracks whose short side is smaller than 720 px;</li><li>`HD`: Video tracks whose short side is equal to or larger than 720 px and smaller than 2160 px;</li><li>`UHD1`: Video tracks whose short side is equal to or larger than 2160 px and smaller than 4320 px; </li><li>`UHD2`: Video tracks whose short side is equal to or larger than 4320 px.</li></ul> |

>?

- If you use a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987), set `appId` to the ID of the subapplication.
- The meanings and valid values of the signature parameters `t`, `exper`, `rlimit`, and `us` are the same as those of the [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).

## Signature Calculation

The VOD player signature is a [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519), which consists of a header, a payload, and a key.

### Header

The header is in JSON format and indicates the algorithm information used. Its content is fixed as follows:

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### Payload

The payload is in JSON format and includes the player signature parameters. Below is an example:

```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "contentInfo": {
    "audioVideoType": "RawAdaptive",
    "rawAdaptiveDefinition": 10,
    "imageSpriteDefinition": 10
  },
  "currentTimeStamp": 1663064276,
  "expireTimeStamp": 1663294210,
  "urlAccessInfo": {
    "t": "6323e6b0",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```

### Key[](id:p6)

The key is what’s used to calculate the signature. In the example below, the [default playback key](https://intl.cloud.tencent.com/document/product/266/35768) is used.

### Calculation formula

1. Calculate the signature:
   `Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), Key)`
2. Calculate the token:
   `Token = base64UrlEncode(Header) + '.' + base64UrlEncode(Payload) + '.' + base64UrlEncode(Signature)`
   The token generated is the VOD player signature.

>?For more information about the HMACSHA256 algorithm, see [RFC 4868 - Using HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-512 with IPsec](https://tools.ietf.org/html/rfc4868#page-3). For more information about `base64UrlEncode`, see [Base 64 Encoding with URL and Filename Safe Alphabet](https://tools.ietf.org/html/rfc4648#page-7).

VOD offers a signature generation tool and a signature verification tool:

* [Player signature tools](https://console.cloud.tencent.com/vod/distribute-play/signature)

### Calculation example

Suppose your `appId` is `1255566655` and you want to generate a player signature for a video whose file ID is `4564972818519602447`. The other parameters are as follows:

* The playback key is `TxtyhLlgo7J3iOADIron`.
* The distribution time of the player signature is 18:17:56 on September 13, 2022, which converted to Unix timestamp is `1663064276`.
* The expiration time of the player signature is 10:10:10 on September 16, 2022, which converted to Unix timestamp is `1663294210`.
* The expiration time of hotlink protection is 11:00:00 on September 16, 2022, which converted to Unix timestamp is `6323e6b0`.
* Up to three IP addresses are allowed to play the video using the playback URL.
* The random string generated for the URL ID is `72d4cd1101`.

Calculate the signature as follows:

1. Determine the content of the header:

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

The result generated after `base64UrlEncode` is:
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.

2. Determine the content of the payload:

```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "contentInfo": {
    "audioVideoType": "RawAdaptive",
    "rawAdaptiveDefinition": 10,
    "imageSpriteDefinition": 10
  },
  "currentTimeStamp": 1663064276,
  "expireTimeStamp": 1663294210,
  "urlAccessInfo": {
    "t": "6323e6b0",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```

The result generated after `base64UrlEncode` is:
`eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImNvbnRlbnRJbmZvMSI6eyJhdWRpb1ZpZGVvVHlwZSI6IlJhd0FkYXB0aXZlIiwicmF3QWRhcHRpdmVEZWZpbml0aW9uIjoxMCwiaW1hZ2VTcHJpdGVEZWZpbml0aW9uIjoxMH0sImN1cnJlbnRUaW1lU3RhbXAiOjE2NjMwNjQyNzYsImV4cGlyZVRpbWVTdGFtcCI6MTY2MzI5NDIxMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNjMyM2U2YjAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ`。

3. Use the playback key (`TxtyhLlgo7J3iOADIron`) to generate an HMAC signature:
    `QFcBX9830ysTzJIyZxoOlRmNb2Gqy2fns9yOfriaDI8`.
4. The token generated is:
    `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImNvbnRlbnRJbmZvMSI6eyJhdWRpb1ZpZGVvVHlwZSI6IlJhd0FkYXB0aXZlIiwicmF3QWRhcHRpdmVEZWZpbml0aW9uIjoxMCwiaW1hZ2VTcHJpdGVEZWZpbml0aW9uIjoxMH0sImN1cnJlbnRUaW1lU3RhbXAiOjE2NjMwNjQyNzYsImV4cGlyZVRpbWVTdGFtcCI6MTY2MzI5NDIxMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNjMyM2U2YjAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ.QFcBX9830ysTzJIyZxoOlRmNb2Gqy2fns9yOfriaDI8`。

## Sample Code

VOD provides Python, Java, Go, C#, PHP, and Node.js sample code for calculating player signatures. For details, see [Sample Player Signature](https://intl.cloud.tencent.com/document/product/266/38096).

## Common Errors

If you use the player signature and the player SDK returns an error code, common causes include:

- **Incorrect signature calculation [key](#p6)**. The **playback key** in the [default distribution configuration](https://intl.cloud.tencent.com/document/product/266/35768) rather than the `KEY` parameter in the [key hotlink protection configuration](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) should be used.
- **Incorrect [signature parameters](#p0)**:
 - **Incorrect parameter type**. For example, `appId` must be an integer, but the value entered is `appId:"125000123"` (string); the transcoding template parameter in `contentInfo` must be an integer, but the value entered is `transcodeDefinition: "14011"` (string).
 - **Incorrect parameter value**. For example, the `audioVideoType` parameter in `contentInfo` is set to `Transocde` (typo).
