# Introduction

This document shows you how to use a third-party player to play encrypted (Widevine, FairPlay) videos of VOD.

# Overview

To decrypt and play an encrypted video using a third-party player, you need to obtain the playback information.

You will need the following playback information:

- Widevine
  - DrmToken (which is used to get the playback license)
  - The URL of the video content
  - The URL of the playback license
- FairPlay
  - DrmToken (which is used to get the playback license)
  - The URL of the video content
  - The URL of the playback license
  - The URL of the certificate

## Workflow

### Commercial-grade DRM (Widevine and FairPlay)

![](https://qcloudimg.tencent-cloud.cn/raw/c77d070232e66d1eef6a6a91b5e8561e.jpg)

- Get the playback information and signature
  After successful authentication, your application server sends the playback information and signature (`DrmToken`) to the client.

- Download the video and certificate and request a license

  When the player tries to play the video, a request for the license and certificate will be sent automatically.

- Decrypt and play the video

  The player uses the license obtained to decrypt and play the video.

# Generating `DrmToken`

`DrmToken` is essentially a variant of [JSON Web Token (JWT)](https://jwt.io/introduction). It also consists of three parts: the header, the payload, and the signature. However, unlike JWT, VOD connects the three parts with `~`.

### Header

The header is in JSON format and indicates the algorithm information used by JWT. Its content is fixed as follows:

```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

### Payload

The payload is in JSON format and includes the player signature parameters. Below is an example:

```json
{
  "type": "DrmToken",
  "appId": 1500014561,
  "fileId": "387702307091793695",
  "currentTimeStamp": 1650964374,
  "expireTimeStamp": 2147483647,
  "random": 4220003655,
  "issuer": "client"
}
```

#### Payload parameters

| **Parameter**       | **Type**   | **Required** | **Description**                                                     |
| ---------------- | ---------- | ------------ | ------------------------------------------------------------ |
| type             | string     | Yes           | The signature type, which should be set to `DrmToken`.                               |
| appId            | int64      | Yes           | The `AppId`.                                                      |
| fileId           | string     | Yes           | The file ID.                                                    |
| issuer       | string | Yes       | The issuer, which should be set to `client`.                                |
| currentTimeStamp | int64      | Yes           | The current time (Unix timestamp).                                           |
| expireTimeStamp  | int64      | No           | The expiration time (Unix timestamp). If you do not specify this, the signature will not expire.      |
| random           | int64      | No           | A random number.                                                     |


### Signature

#### Calculation method

`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), pkey)`

>? For more information about the HMACSHA256 algorithm, see [RFC 4868 - Using HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-512 with IPsec](https://tools.ietf.org/html/rfc4868#page-3). For more information about `base64UrlEncode`, see [Base 64 Encoding with URL and Filename Safe Alphabet](https://tools.ietf.org/html/rfc4648#page-7).

You can view the playback key (`pkey`) in the VOD console:

Select **Distribution and Playback > Default Distribution Domain** on the left sidebar.

![](https://qcloudimg.tencent-cloud.cn/raw/d3bebcb860f8c9900fca9a645a0879be.png)

### `DrmToken` example

- Header:

```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

Encoded (base64UrlEncode): `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`

- Payload:

```json
{
  "type": "DrmToken",
  "appId": 1500014561,
  "fileId": "387702307091793695",
  "currentTimeStamp": 1650964374,
  "expireTimeStamp": 2147483647,
  "random": 4220003655,
  "issuer": "client"
}
```

Encoded (base64UrlEncode): `eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9`

- Signature: `muHWnxX9dXsUAkCzw4uXGcvwKDoA19BkR-hCJVrXyvY`. It is generated using `pkey` (whose value is `JduzsUuRvGVPRHvIYwLv`).

Connect the header, payload, and signature with `~` and you will get the `DrmToken`, which is `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`.

# Generating a Playback URL

- Call [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181) to get the URL of the video content (the value of `MediaInfoSet.AdaptiveDynamicStreamingInfo.AdaptiveDynamicStreamingSet.Url`).

- If you have enabled key hotlink protection, refer to [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986) to generate a URL that includes the hotlink protection signature.


# Generating a License URL

In case of commercial-grade DRM, a license is needed for a player to play encrypted videos.

## Request

Request URL:

- Widevine: `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2`
- FairPlay: `https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2`

Request method: POST

Request parameters:

| **Parameter**        | **Description**                                                     |
| ---------------- | ------------------------------------------------------------ |
| drmToken     | The authentication token. |

>? Include in the request body the license request data generated by the DRM client module.

## Response

- If the request is successful, the status code will be 200, and the binary data of the license will be returned.

- If the request fails, the status code will be a value other than 200.

### Status codes
| **Status Code**        | **Description**                                                     |
| ---------------- | ------------------------------------------------------------ |
| 200     | Request successful. |
| 400     | Parameter error. |
| 403 | Authentication failed. |
| 500     | Internal error. |

## License request example

A license request URL for Widevine: `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`

# Getting the License URL

To play a FairPlay-encrypted video, you need to [apply for](https://www.tencentcloud.com/document/product/266/46643) a FairPlay certificate and [submit](https://www.tencentcloud.com/document/product/266/49668) the certificate information to VOD. License URLs are not required for Widevine.

After submitting the information, you can view the license URL in the VOD console. Each subapplication has only one license URL.

# Playing the Video Using a Third-Party Player

Once you have the playback URL, license URL, and certificate URL, you can use a third-party player to play the DRM-encrypted video.

# Summary

Now, you should know how to play encrypted videos of VOD using a third-party player.