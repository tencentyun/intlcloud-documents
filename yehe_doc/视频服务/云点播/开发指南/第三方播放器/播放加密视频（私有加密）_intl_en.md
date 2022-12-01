# Introduction

This document shows you how to use a third-party player to play encrypted (SimpleAES) videos of VOD.

# Overview

To decrypt and play an encrypted video using a third-party player, you need to obtain the playback information.

You will need the following information:

- `DrmToken` (which is used to get the decryption key)
- The URL of the video content

## Workflow

### Private encryption

![](https://qcloudimg.tencent-cloud.cn/raw/0869fb5666a8d93a57ae0202f7468c97.jpg)

- Get the playback information and signature
  After successful authentication, your application server sends the playback information and signature (`DrmToken`) to the client.

- Download the video and get the key

  A playback URL is generated based on the playback information obtained (DrmToken and content URL). When the player tries to play the video, a request to get the key will be sent automatically.

  If key protection is enabled, VOD’s key distribution service will encrypt the content key. For example, if the protection mode is `sha256`, the key distribution service will use a symmetric key to encrypt the content key.
  
  If key protection is disabled, the key distribution service will send the content key directly.

- Decrypt and play the video

  If key protection is enabled, the application client needs to decrypt the content key received. For example, if the protection mode is `sha256`, the client will need to use a symmetric key to decrypt the key information obtained before it can decrypt and play the video.

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
  "protectSchema": "sha256",
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
| protectSchema    | string     | No           | The protection mode. This parameter is valid only if the encryption scheme is `SimpleAES`. If you set this parameter to `sha256`, `sha256(pkey)` will be used as the symmetric key to encrypt the content key (`pkey` is the playback key, and `sha256` indicates the SHA-256 algorithm). |

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
  "protectSchema": "sha256",
  "issuer": "client"
}
```

Encoded (base64UrlEncode): `eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ`

- Signature: `dK42jB0KP4sXCd7Dunng9AcQ2WlnANuB87PwxmTc3_g`. It is generated using `pkey` (whose value is `JduzsUuRvGVPRHvIYwLv`).

Connect the header, payload, and signature with `~` and you will get the `DrmToken`, which is `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ~JZ0sAV214-7vNckjb-llSntnqsIr-qF5oD4Lv7L1qGQ`.

# Generating a Playback URL

- Call [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181) to get the URL of the video content (the value of `MediaInfoSet.AdaptiveDynamicStreamingInfo.AdaptiveDynamicStreamingSet.Url`).

- If you have enabled key hotlink protection, refer to [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986) to generate a URL that includes the hotlink protection signature.

- For SimpleAES-encrypted videos, the format of playback URLs is as follows:

  Suppose the original video URL is `http(s)://xxx.com/xxx/xxx/test.m3u8`.

  The playback URL would be `http(s)://xxx.com/xxx/xxx/voddrm.token.<DrmToken>.test.m3u8`.

  The prefix `voddrm.token.` is added to the filename, and the value of `<DrmToken>` is the `DrmToken` generated above.
  
### Playback URL example

Suppose the URL of the video content is `https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff`.

The `DrmToken` is `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ~JZ0sAV214-7vNckjb-llSntnqsIr-qF5oD4Lv7L1qGQ`.

The playback URL would be `https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/voddrm.token.eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ~JZ0sAV214-7vNckjb-llSntnqsIr-qF5oD4Lv7L1qGQ.adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff`.

# Playing the Video Using a Third-Party Player

Once you have the playback URL, you can use a third-party player to play the video, but you will need to encrypt the content key obtained from VOD’s key distribution service.

The player will send a request for the content key (`CipherContentKey`) when it tries to play the video. The request URL is specified by `#EXT-X-KEY` in the M3U8 file. Below is an example:

```text
#EXT-X-KEY:METHOD=AES-128,URI="https://drm.vod2.myqcloud.com/getlicense/v1?drmType=SimpleAES&token=<DrmToken>"
```

How to decrypt the key:

- Generate the symmetric key (`SymmetricKey`):

  `SymmetricKey=SHA256(pkey)`

  `SHA256` indicates the SHA-256 algorithm, and `pkey` is the playback key/

- Decrypt the content key (`ContentKey`):

  `ContentKey=AES-CBC-Descrypt(CipherContentKey, SymmetricKey, IV)`

  `CipherContentKey` is the encrypted content key, which is returned by VOD’s key distribution service and does not include IV data. `AES-CBC-Descrypt` indicates the AES-CBC algorithm. `IV` is the initialization vector, which is `0x00000000000000000000000000000000`.

## Decryption example

Suppose:

- The playback key (`pkey`) is `JduzsUuRvGVPRHvIYwLv`, and the symmetric key (`SymmetricKey`) is `0xece0bae38fbbd66f79c62acefb9ea994dc834d79b45cc4556962d9f00508b9b3 `(32 bytes).
- The encrypted content key (`CipherContentKey`) is `0x68addf7984478a3e4797d3a13ecbb6fb` (16 bytes).
- The IV is always ` 0x00000000000000000000000000000000` (16 bytes).

The decrypted content key (`ContentKey`) would be `0xbed3747b8510b040826163c04956a4c1` (16 bytes).

# Summary

Now, you should know how to play encrypted videos of VOD using a third-party player.