VOD provides [playback SDKs](https://intl.cloud.tencent.com/document/product/266/7836) for Android, iOS, and web for long video and video encryption scenarios. You can quickly integrate VOD playback capabilities by using the VOD SDK. If the VOD superplayer SDK cannot meet your custom needs, you can also refer to the communication protocol between the SDK and the VOD backend as detailed below to implement a self-built player.

## Protocol
Requests are initiated in HTTP GET, and the URL is `https://playvideo.qcloud.com/{interface}/{version}/{appId}/{fileId}?psign=xxx`.

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
| psign | No | Superlayer signature. For more information on how to enter it, please see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099). |

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
| coverUrl | String | Video cover. |

#### StreamingInfo type

| Parameter | Type | Description |
| -- | -- | -- |
|plainOutput|String| Unencrypted output in the `StreamingOutput` type. |
|drmOutput|Array| Output after the video is DRM encrypted in the `StreamingOutput` type. |
|drmToken|String| The DRM token used when the DRM encrypted output is played back. To play back, you need to add this field to `streamingOutput.url`. |

#### StreamingOutput type

| Parameter | Type | Description |
| -- | -- | -- |
| type | String | Adaptive bitstream protection type. Valid values: plain (no encryption), simpleAES (HLS common encryption). |
| url | String | Playback URL. |
| subStreams | Array | Substream information in the `SubStreamInfo` type. |

#### SubStreamInfo type

| Parameter | Type | Description |
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

### Playback
#### Playing back unencrypted output
If the returned result of the request is an unencrypted video (that is, `streamingOutput.type` is `plain`), it can be directly played back at the `streamingOutput.url` link.

#### Playing back encrypted output
If the returned result of the request is an encrypted video (that is, `streamingOutput.type` is `simpleAES`), you need to add `streamingInfo.drmToken` to the filename of `streamingOutput.url` to generate a link for playback.

**Splicing rule**: new filename = voddrm.token.{token to be added}.{original filename}

For example, if `streamingOutput.url` is `http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.m3u8?t=5c08d9fa&us=someus&sign=xxx` and `drmToken` is `JhbGciOxxxsInR5cCI6Ikp`, then
The playback URL is as follows:
`http://125xxx167.vod2.myqcloud.com/xxx/xxx/voddrm.token.JhbGciOxxxsInR5cCI6Ikp.xx.m3u8?t=5c08d9fa&us=someus&sign=xxx`.

### Business flowchart
#### Flowchart of unencrypted video playback

![](https://main.qcloudimg.com/raw/33e3cdeb424ca34f0ec2cb873a35ff7f.png)

#### Flowchart of encrypted video playback

![](https://main.qcloudimg.com/raw/8533090da512fe2d87b9a6a7d15add6a.png)



## Samples
The following is an example of playing back the encrypted output of a video.

### Request
`https://playvideo.qcloud.com/getplayinfo/v4/125xxx167/52858xxx74597?psign=0eef1a12dxxxf0f48ebf34b4`

### Response
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
            "name":"Animal World",
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
                            "resolutionName":"LD"
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
| Name | Description |
| -- | -- |
| Content key | After using `SimpleAES` to encrypt a video, you can specify the address to get the decryption key (128 bytes of binary data) in the URI in the `EXT-X-KEY` tag of the .m3u8 file, and the player will get the key in real time and then decrypt the video for playback. |


## Debugging Suggestions
We recommend you check the following for debugging:
1. Unencrypted playback
2. Encrypted playback



