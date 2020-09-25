A superplayer signature is used by the application playback service to authorize a client for playback. If the playback service allows the client to play back, it will distribute a valid signature to the client as shown in step 5 below. The client can play back the video within the validity period of the signature.
<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="700" />

>! In the following cases, the application client needs a superplayer signature to play back the video:
* [Key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986) is enabled for the domain name.
* Another superplayer configuration rather than `default` is used.
* An encrypted video is to be played back.

The superplayer signature parameters and generation rule are as detailed below:

## Signature Parameters

| Parameter Name | Required | Type | Description |
| -- | -- | -- | -- |
| appId | Yes | Integer | Account `appId` |
| fileId | Yes | String | File ID |
| currentTimeStamp | Yes | Integer | Current Unix timestamp of distributed signature |
| expireTimeStamp | No | Integer | Expiration Unix timestamp of distributed signature. If this parameter is left empty, the signature will never expire |
| pcfg | No | String | Name of the superplayer configuration to be used. If you use the `default` configuration, you can leave this parameter empty |
| urlAccessInfo | No | Object | Hotlink protection configuration parameter of playback link, which is in [UrlAccessInfo type](#p1) |
| drmLicenseInfo | No | Object | Key configuration parameter of encrypted content, which is in [DrmLicenseInfo type](#p2) |

<span id = "p1"></span>
#### UrlAccessInfo type

| Parameter Name | Required | Type | Description |
| -- | -- | -- | -- |
| t | No | String | <ul style="margin:0;"><li>Hexadecimal string indicating the link expiration time</li><li>For the specific description and valid values, please see the `t` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)</li><li>If this parameter is left empty, the link will never expire</li>|
| exper | No | Integer | <ul style="margin:0;"> <li>Preview duration in decimal seconds</li><li>If you want to specify the preview duration, it should be no less than 30 seconds</li><li>For the specific description and valid values, please see the `exper` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)</li> |
| rlimit | No | Integer | <ul style="margin:0;"><li>Maximum decimal number of clients with different IPs allowed for playback</li><li>For the specific description and valid values, please see the `rlimit` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)</li> |
| us | No | String | <ul style="margin:0;"><li>Link ID, which can uniquely identify a link</li><li>For the specific description and valid values, please see the `us` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)</li> |

<span id = "p2"></span>
#### DrmLicenseInfo type

| Parameter Name | Required | Type | Description |
| -- | -- | -- | -- |
| expireTimeStamp | No | Integer | Expiration Unix timestamp of key. If this parameter is left empty, the signature will never expire |

>?
- If you use a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987), set the `AppId` of the subapplication as the `appId` parameter.
- The description and valid values of `t`, `exper`, `rlimit`, and `us` in signature parameters are the same as those in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).

## Signature Calculation

The VOD superplayer uses [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519), which is a digital token calculated and formed based on `Header`, `PayLoad`, and `Key`.

### Header

`Header` is in JSON format and indicates the information of the algorithm used by JWT. Its content is fixed as follows:

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### PayLoad

`PayLoad` is in JSON format and indicates the superplayer signature parameters; for example:

```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546340400,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```

### Key

`Key` is the key used during signature calculation, which is the same as the `KEY` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).

### Calculation formula

1. Calculate the `Signature`:
`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), KEY)`
2. Calculate the `Token`:
`Token = base64UrlEncode(Header) + '.' + base64UrlEncode(Payload) + '.' + base64UrlEncode(Signature)`
The final `Token` is the VOD superplayer signature.

>?For more information on `HMACSHA256`, please see [RFC 4868 - Using HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-512 with IPsec](https://tools.ietf.org/html/rfc4868#page-3). For more information on `base64UrlEncode`, please see [5. Base 64 Encoding with URL and Filename Safe Alphabet](https://tools.ietf.org/html/rfc4648#page-7).

To help you calculate and verify the signature, VOD provides online signature generation and verification tools:
* Use the [superplayer signature generation tool](https://vods.cloud.tencent.com/signature/super-player-sign.html) to quickly generate a signature.
* Use the [superplayer signature verification tool](https://vods.cloud.tencent.com/signature/super-player-check-sign.html) to quickly verify a signature.

### Calculation example

For example, a superplayer signature is generated for a video whose `fileId` is `4564972818519602447`, which belongs to a user whose `appId` is `1255566655` and has the following attributes:

* The enabled hotlink protection `KEY` is `24FEQmTzro4V5u3D5epW`.
* A custom superplayer configuration is used, and its name is `MyCfg`.
* The distribution time of the player signature is 19:00:00, January 1, 2019, and the corresponding Unix time is `1546340400`.
* The expiration time of the player signature is 20:00:00, January 1, 2019, and the corresponding Unix time is `1546344000`.
* The expiration time of hotlink protection is 20:00:00, January 1, 2019, and the corresponding Unix time is `5c2b5640`.
* Up to three different IPs are allowed to play back the video at the URL.
* The generated random string is `72d4cd1101`.

The signature will be generated as follows:
1. The following is the content of `Header`:
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```
The result after processing through `base64UrlEncode` will be:
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.
2. The following is the content of `Payload`:
```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546340400,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```
The result after processing through `base64UrlEncode` will be:
```
eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ
```
3. Perform HMAC calculation by using `24FEQmTzro4V5u3D5epW` as `KEY`, and the `Signature` will be:
`TRdfy-ctQFRDJzknfKsT0di5tEaweAVumOgxsA8Qd-8`.
4. The final `Token` will be:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ.TRdfy-ctQFRDJzknfKsT0di5tEaweAVumOgxsA8Qd-8
```

## Sample Code

VOD provides code samples of superplayer signature for various programming languages such as Python, Java, Go, C#, PHP, and Node.js. For more information, please see [Superplayer Signature - Sample Signature](https://intl.cloud.tencent.com/document/product/266/38096).
