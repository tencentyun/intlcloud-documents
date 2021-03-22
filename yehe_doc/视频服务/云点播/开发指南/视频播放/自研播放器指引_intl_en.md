VOD provides [playback SDKs](https://intl.cloud.tencent.com/document/product/266/7836) for Android, iOS, and web for long video and video encryption scenarios. You can quickly integrate VOD playback capabilities by using the VOD SDK. If the VOD superplayer SDK cannot meet your custom needs, you can also refer to the communication protocol between the SDK and the VOD backend as detailed below to implement a self-built player.

## Protocol
A request is initiated in HTTP GET, and the URL is `https://playvideo.qcloud.com/{interface}/{version}/{appId}/{fileId}?psign=xxx&cipheredOverlayKey=xxx&cipheredOverlayIv=xxx&keyId=x`.

### Domain name
* Primary domain name: `playvideo.qcloud.com`
* Secondary domain name: `bkplayvideo.qcloud.com`

### Request fields
#### path field

| Field | Required | Value |
| -- | -- | -- |
| appId | Yes | Enter the `appid` (if a subapplication is used, enter the `subappid`). |
| fileId | Yes | ID of the video file to be played back. |
| version | Yes | Always enter `v4`. |
| interface | Yes | Always enter `getplayinfo`. |

#### querystring field

| Field | Required | Value |
| -- | -- | -- |
| psign | No | Superlayer signature. For the parameters, please see the "Superplayer signature" section below. For the signature algorithm, please see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099). |
|context| No | Passthrough field, which will be returned as-is in the return packet. |
|cipheredOverlayKey| No | Additional encryption key used to encrypt the key, which contains 256 hexadecimal characters, such as `5872bd2fcc76176a2db6fcd1341c04e891643e938bf8901310846de62d6942f49e7393cbaf96fd48bfeb7f50878d5bafe93017670e4483e6ccc3c8908ee2ae42823b875aa171a44781cc417163d19d503dda2ba1e6242f41b49c1de12bed52de310a71ba3d8660a9a086289a54f573f1141c451b6ec88ca917c586b4d7735e20`. |
|cipheredOverlayIv| No | Additional encryption initialization vector used to encrypt the key, which contains 256 hexadecimal characters, such as `5872bd2fcc76176a2db6fcd1341c04e891643e938bf8901310846de62d6942f49e7393cbaf96fd48bfeb7f50878d5bafe93017670e4483e6ccc3c8908ee2ae42823b875aa171a44781cc417163d19d503dda2ba1e6242f41b49c1de12bed52de310a71ba3d8660a9a086289a54f573f1141c451b6ec88ca917c586b4d7735e20`. |
|keyId| No | Key version. Valid values: 0, 1. `0` indicates that `cipheredOverlayKey` and `cipheredOverlayIv` are invalid. `1` indicates that `cipheredOverlayKey` and `cipheredOverlayIv` are valid. |

### Superplayer signature
#### Signature parameters

| Parameter | Required | Type | Description |
| -- | -- | -- | -- |
| appId | Yes | Integer | Account `appId`.|
| fileId | Yes | String | File ID. |
| currentTimeStamp | Yes | Integer | Unix timestamp of distributing a signature. |
| expireTimeStamp | Yes | Integer | Expiration Unix timestamp of the distributed signature. If this parameter is left empty, the signature will expire 1 day after distribution. |
| pcfg | No | String | Name of the superplayer configuration to be used. If you use the `Default` configuration, you can leave this parameter empty. |
| urlAccessInfo | No | Object | Hotlink protection configuration parameter of playback link, which is in `UrlAccessInfo` type. |
| drmLicenseInfo | No | Object | Key configuration parameter of encrypted content, which is in `DrmLicenseInfo` type. |

##### UrlAccessInfo type

| Parameter | Required | Type | Description |
| -- | -- | -- | -- |
| t | No | String | Hexadecimal string indicating the link expiration time. For the specific description and valid values, please see the `t` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986). If this parameter is left empty, the link will expire in 1 day after the signature is generated. |
| exper | No | Integer | Preview duration in decimal seconds. If you want to specify the preview duration, it should be no less than 30 seconds (i.e., half a minute). For the specific description and valid values, please see the `exper` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986). |
| rlimit | No | Integer | Maximum decimal number of clients with different IPs allowed for playback. For the specific description and valid values, please see the `rlimit` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986). |
| us | No | String | Link ID, which uniquely identifies a link. For the specific description and valid values, please see the `us` parameter in [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986). |

##### DrmLicenseInfo type

| Parameter | Required | Type | Description |
| -- | -- | -- | -- |
| expireTimeStamp | No | Integer | Expiration Unix timestamp of key. If this parameter is left empty, the key will expire in 1 day after the signature is distributed. |
| strictMode | No | Integer | Check level. Valid values: 0, 1, 2. `0` indicates that the content key is allowed to be passed through, encrypted with a symmetric key, or encrypted with a symmetric key and an asymmetric key. `1` indicates that the content key is allowed to be encrypted with a symmetric key or encrypted with a symmetric key and an asymmetric key. `2` indicates that the content key is only allowed to be encrypted with a symmetric key and an asymmetric key. If the content key is allowed to be passed through, the content can be played back on any clients. If the content key is encrypted, the client can play back the content only after decrypting the content key. |

### Response field

| Parameter  | Type | Description |
| -- | -- | -- |
| code | Integer | Error code. A value other than 0 indicates an error. |
| message | String | Error message. It has a value when `code` is not 0. |
| version | Integer | Type of the currently returned result version, which is fixed at 4. |
| warning | String | Warning message. If the `psign` parameter is carried but hotlink protection is not enabled, a warning will be returned. |
| media | Object | Media information. The element type is `Media`.

#### Media type

| Parameter  | Type | Description |
| -- | -- | -- |
| basicInfo | Object | Basic video information in the `BasicInfo` type. |
| streamingInfo | Object | Multi-bitrate video information in the `StreamingInfo` type. |
| imageSpriteInfo | Object | Thumbnail information in the `ImageSpriteInfo` type, which is mainly used by the player to preview the video. |
| keyFrameDescInfo | Object | Video timestamp information in `KeyFrameDescInfo` type, which is used by the player to timestamp the video. |

#### BasicInfo type

| Parameter | Type | Description |
| -- | -- | -- |
| name | String | Video name. |
| size | Integer | Video size in bytes. |
| duration | Float | Video duration in seconds. |
| description | String | Video description. |
| coverUrl | String | URL of video thumbnail. |

#### StreamingInfo type

| Parameter  | Type | Description |
| -- | -- | -- |
|plainOutput|String| Unencrypted output in the `StreamingOutput` type. |
|drmOutput|Array| Output after the video is DRM encrypted in the `StreamingOutput` type. |
|drmToken|String| The DRM token used when the DRM encrypted output is played back. To play back, you need to add this field to `streamingOutput.url`. |

#### StreamingOutput type

| Parameter  | Type | Description |
| -- | -- | -- |
| type | String | Adaptive bitstream protection type. Valid values: plain (no encryption), simpleAES (HLS common encryption). |
| url | String | Playback URL. |
| subStreams | Array | Substream information in the `SubStreamInfo` type. |

#### SubStreamInfo type

| Parameter  | Type | Description |
| -- | -- | -- |
| type | String | Substream type. Valid values: video. |
| width | Integer | Substream video width in px. |
| height | Integer | Substream video height in px. |
| resolutionName | String | Specification name of the substream video displayed in the player. |

#### ImageSpriteInfo type

| Parameter  | Type | Description |
| -- | -- | -- |
| imageUrls | Array | Array of thumbnail download URLs in `String` type. |
| webVttUrl | String | Thumbnail VTT file download URL. |

### Encrypted output playback

If the returned result of the request is an encrypted video (that is, `streamingOutput.type` is `simpleAES`), you need to add `streamingInfo.drmToken` to the filename of `streamingOutput.url` to generate a link for playback.

**Splicing rule**: new filename = voddrm.token.{token to be added}.{original filename}

For example, if `streamingOutput.url` is `http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.m3u8?t=5c08d9fa&us=someus&sign=xxx` and `drmToken` is `JhbGciOxxxsInR5cCI6Ikp`, 
the playback URL is as follows:
`http://125xxx167.vod2.myqcloud.com/xxx/xxx/voddrm.token.JhbGciOxxxsInR5cCI6Ikp.xx.m3u8?t=5c08d9fa&us=someus&sign=xxx`.


## Private Encryption Details

HLS common encryption works by specifying the address to get the content key in the URI in the `EXT-X-KEY` tag of the M3U8 file, and the player will get the key in real time and then decrypt the video for playback.
Because the key is transferred in plaintext, the security level is low, and some browser plugins may be able to crack it.
To address this problem, VOD provides a private encryption scheme. It uses the `OverlayKey` and `OverlayIv` you generate in real time to encrypt the content key with the AES-128 CBC algorithm for secondary encryption, and then uses the specified public key on the client side with the RSA algorithm to encrypt `OverlayKey` and `OverlayIv` to prevent the disclosure of the content key.
The specific steps are as follows:
### 1. Get Psign
**Player:**
When your player starts playing, it needs to request `Psign` from the business server first.
**Business server:**
You need to enter different values for the `StrictMode` parameter according to the actual use case to calculate and distribute `Psign`.
### 2. Encrypt the temporary key
**Player:**
The player randomly generates temporary `OverlayKey` and `OverlayIv`, specifies the key version `KeyId` as 1, uses the `PublicKey` corresponding to the `KeyId` of 1 to encrypt `OverlayKey` and `OverlayIv` with RSA to get `CipheredOverlayKey` and `CipheredOverlayIv`, and then enters them together with the `Psign` obtained in step 1 into the `querystring` that requests VOD.

### 3. Use the temporary key to decrypt the key
**Player:**
When an encrypted video is played back, the key obtained by the M3U8 file from the URL specified by `EXT-X-KEY` has been encrypted with `OverlayKey` and `OverlayIV`. At this time, your player needs to use `OverlayKey` and `OverlayIV` to decrypt the key and then use the decrypted key to decrypt the video for playback.

### 4. Overall business flowchart of the upgraded encryption scheme

![](https://main.qcloudimg.com/raw/872e8921a291877be233da67f25138bb.png)


## Sample
The following is an example of playing back the encrypted output of a video.

### Request
`https://playvideo.qcloud.com/getplayinfo/v4/125xxx167/52858xxx74597?psign=0eef1a12dxxxf0f48ebf34b4&cipheredOverlayKey=5872bd2fcc76176a2db6fcd1341c04e891643e938bf8901310846de62d6942f49e7393cbaf96fd48bfeb7f50878d5bafe93017670e4483e6ccc3c8908ee2ae42823b875aa171a44781cc417163d19d503dda2ba1e6242f41b49c1de12bed52de310a71ba3d8660a9a086289a54f573f1141c451b6ec88ca917c586b4d7735e20&cipheredOverlayIv=5872bd2fcc76176a2db6fcd1341c04e891643e938bf8901310846de62d6942f49e7393cbaf96fd48bfeb7f50878d5bafe93017670e4483e6ccc3c8908ee2ae42823b875aa171a44781cc417163d19d503dda2ba1e6242f41b49c1de12bed52de310a71ba3d8660a9a086289a54f573f1141c451b6ec88ca917c586b4d7735e20&keyId=1`

## Response
```json
{
    "code":0,
    "message":"",
    "requestId":"377d94185f0342c5b67b038501f54974",
    "version":4,
    "context":"",
    "warning":"",
    "media":{
        "basicInfo":{
            "Name":"Animal World",
            "size":26246026,
            "duration":30.5,
            "description":"A classic animal program from CCTV",
            "coverUrl":"http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.jpg?t=5c08d9fa&amp;someus&amp;sign=xxx"
        },
        "streamingInfo":{
            "plainOutput":{

            },
            "drmOutput":[
                {
                    "type":"simpleAes",
                    "url":"http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.m3u8?t=5c08d9fa&amp;us=someus&amp;sign=xxx",
                    "subStreams":[
                        {
                            "type":"video",
                            "width":427,
                            "height":240,
                            "resolutionName":"Smooth"
                        },
                        {
                            "type":"video",
                            "width":853,
                            "height":480,
                            "resolutionName":"SD"
                        },
                        {
                            "type":"video",
                            "width":1280,
                            "height":720,
                            "resolutionName":"HD"
                        }
                    ]
                }
            ],
            "drmToken":"JhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9xxx",
        },
        "imageSpriteInfo":{
            "imageUrls":[
                "http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.jpg?t=5c08d9fa&amp;us=someus&amp;sign=xxx"
            ],
            "webVttUrl":"http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.vtt?t=5c08d9fa&amp;us=someus&amp;sign=xxx"
        },
        "keyFrameDescInfo":{
            "keyFrameDescList":[
                {
                    "timeOffset":1.1,
                    "content":"Beginning now..."
                },
                {
                    "timeOffset":100.2,
                    "content":"Ending soon..."
                }
            ]
        }
    }
}
```

## Glossary
| Parameter  | Type | Description |
| -- | -- | -- |
| OverlayKey | String | Secondary client encryption key, which is used to encrypt the content key. It is a string containing 32 bytes and is calculated by hexadecimal encryption of the 128-bit key. |
| OverlayIv | String | Initialization vector for secondary client encryption, which is used to encrypt the content key. It contains 32 characters, where each character represents a hexadecimal digit. |
| cipheredOverlayKey | String | Additional encryption key used to encrypt the key, which contains 256 hexadecimal characters. |
| cipheredOverlayIv | String | Additional encryption initialization vector used to encrypt the key, which contains 256 hexadecimal characters. |



## Debugging Suggestions
We recommend you check the following for debugging:
1. Unencrypted playback
2. Private encrypted playback

## Public Key
 The public key corresponding to `KeyId` of `1` is as follows:
```
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC3pDA7GTxOvNbXRGMi9QSIzQEI
+EMD1HcUPJSQSFuRkZkWo4VQECuPRg/xVjqwX1yUrHUvGQJsBwTS/6LIcQiSwYsO
qf+8TWxGQOJyW46gPPQVzTjNTiUoq435QB0v11lNxvKWBQIZLmacUZ2r1APta7i/
MY4Lx9XlZVMZNUdUywIDAQAB
-----END PUBLIC KEY-----
```
