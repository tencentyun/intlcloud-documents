A player signature is used by the application playback service to authorize a client for playback. If the playback service allows the client to play back, it will distribute a valid signature to the client as shown in step 5 below. The client can play back the video within the validity period of the signature.
<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="700" />

>! The application client needs a player signature to play back a video in the following cases:
>- [Key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986) has been enabled for the domain name.
>- [Player configurations](https://intl.cloud.tencent.com/document/product/266/38296) other than the `default` one has been used.
>- An [encrypted](https://intl.cloud.tencent.com/document/product/266/38294) video needs to be played back.

The player signature parameters and generation rule are as detailed below:

## Signature Parameters

| Parameter | Required | Type | Description |
| -- | -- | -- | -- |
| appId | Yes | Integer | The account `appId`. |
| fileId | Yes | String | The file ID. |
| currentTimeStamp | Yes | Integer | Current Unix timestamp of the distributed signature. |
| expireTimeStamp | No | Integer | Expiration Unix timestamp of the distributed signature. If this parameter is left empty, the signature will never expire. |
| pcfg | No | String | The name of the player configuration to be used. If you use the `default` configuration, you can leave this parameter empty. |
| urlAccessInfo | No | Object | Hotlink protection configuration parameter of playback URL, which is in [UrlAccessInfo type](#p1). |
| drmLicenseInfo | No | Object | Key configuration parameter of encrypted content, which is in [DrmLicenseInfo type](#p2). |

#### `UrlAccessInfo` type[](id:p1)

| Parameter | Required | Type | Description |
| -- | -- | -- | -- |
| t | No | String | <ul style="margin:0;"><li>A hexadecimal string indicating the URL expiration time</li><li>For the specific description and valid values, see the `t` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).</li><li>If this parameter is left empty, the URL will never expire.</li>|
| exper | No | Integer | <ul style="margin:0;"> <li>The preview duration in decimal seconds</li><li>If you want to specify the preview duration, it should be no less than 30 seconds.</li><li>For the specific description and valid values, see the `exper` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).</li> |
| rlimit | No | Integer | <ul style="margin:0;"><li>The maximum decimal number of clients with different IPs allowed for playback</li><li>For the specific description and valid values, see the `rlimit` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).</li> |
| us | No | String | <ul style="margin:0;"><li>The URL ID, which can uniquely identify a link</li><li>For the specific description and valid values, see the `us` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).</li> |
| uid | No | String | <ul style="margin:0;"><li>The ID of the user playing back the video, which must contain eight hexadecimal digits. This parameter is used for the [digital watermark](https://intl.cloud.tencent.com/document/product/266/47920) feature.</li><li>For the specific description and value range, see the `uid` parameter in [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).</li> |

#### `DrmLicenseInfo` type[](id:p2)

| Parameter | Required | Type | Description |
| -- | -- | -- | -- |
| expireTimeStamp | No | Integer | Expiration Unix timestamp of the key. If this parameter is left empty, the key will never expire. |

>?
>- If you use a subapplication as described in [Subapplication System](https://intl.cloud.tencent.com/document/product/266/33987), set the `AppId` of the subapplication as the value of the `appId` parameter.
>- The description and valid values of `t`, `exper`, `rlimit`, `us`, and `uid` in signature parameters are the same as those in hotlink protection parameters as described in [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).

## Signature Calculation

The VOD Player uses [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519), which is a digital token calculated and formed based on `Header`, `PayLoad`, and `Key`.

### Header

`Header` is in JSON format and indicates the information of the algorithm used by JWT. Its content is fixed as follows:

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### PayLoad

`PayLoad` is in JSON format and indicates the player signature parameters; for example:

```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546300,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101",
    "uid": "1234abcd"
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
The `Token` is the VOD Player signature.

>?For more information on `HMACSHA256`, please see [RFC 4868 - Using HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-512 with IPsec](https://tools.ietf.org/html/rfc4868#page-3). For more information on `base64UrlEncode`, please see [Base 64 Encoding with URL and Filename Safe Alphabet](https://tools.ietf.org/html/rfc4648#page-7).

To help you calculate and verify the signature, VOD provides the following tools:
* [Player SDK signature generation tool](https://vods.cloud.tencent.com/signature/super-player-sign.html): Allows you to quickly generate a signature.
* [Player SDK signature verification tool](https://vods.cloud.tencent.com/signature/super-player-check-sign.html): Allows you to quickly verify a signature.

### Billing examples

For example, a player signature is generated for a video whose `fileId` is `4564972818519602447`, which belongs to a user whose `appId` is `1255566655` and has the following attributes:

* The enabled hotlink protection `KEY` is `24FEQmTzro4V5u3D5epW`.
* A custom player configuration is used, and its name is `MyCfg`.
* The distribution time of the player signature is 19:00:00 on January 1, 2019, corresponding to Unix time `1546300`.
* The expiration time of the player signature is 20:00:00 on January 1, 2019, corresponding to Unix time `1546344000`.
* The expiration time of hotlink protection is 20:00:00 on January 1, 2019, corresponding to Unix time `5c2b5640`.
* Up to three different IPs are allowed to play back the video at the URL.
* The generated random string is `72d4cd1101`.

Calculate the signature as follows:
1. Determine the content of `Header`:
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```
The result after processing through `base64UrlEncode` will be:
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.
2. Determine the content of `Payload`:
```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546300,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101",
    "uid": "1234abcd"
  }
}
```
The result after processing through `base64UrlEncode` will be:
`eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSIsInVpZCI6IjEyMzRhYmNkIn19`.
3. Perform HMAC calculation by using `24FEQmTzro4V5u3D5epW` as `KEY`, and the `Signature` will be:
`j3WJ9W3V4ve_N_Z157_B9AKkT0GhSmGAEdhv6YtoZSY`.
4. The `Token` will be:
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSIsInVpZCI6IjEyMzRhYmNkIn19.j3WJ9W3V4ve_N_Z157_B9AKkT0GhSmGAEdhv6YtoZSY`.

## Sample Code

VOD provides sample code for calculating a player signature for Python, Java, Go, C#, PHP, and Node.js. For more information, see [Sample Player Signature](https://intl.cloud.tencent.com/document/product/266/38096).
