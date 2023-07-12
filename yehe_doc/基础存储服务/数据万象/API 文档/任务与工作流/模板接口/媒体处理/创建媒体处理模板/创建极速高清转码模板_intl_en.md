## Feature Description

This API is used to create a top speed codec transcoding template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateAnimationTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```shell
POST /template HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```


>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>HighSpeedHd</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Fps>30</Fps>
        <Bufsize>0</Bufsize>
        <Maxrate>0</Maxrate>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
    </Audio>
    <TransConfig>
        <IsCheckReso>false</IsCheckReso>
        <ResoAdjMethod>1</ResoAdjMethod>
    </TransConfig>
    <TimeInterval>
        <Start>0</Start>
        <Duration>60</Duration>
    </TimeInterval>
</Request>

```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | -------------------------------------------- | --------- | -------- | ---- |
| Tag                | Request | Template tag: HighSpeedHd                                | String    | Yes   | None |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| Container          | Request | Container format                                    | Container | Yes       | None                             |
| Video              | Request | Video information                                                 | Container | Yes   | None   |
| TimeInterval       | Request | Time interval                                    | Container | No       | None                             |
| Audio              | Request | Audio information                                                 | Container | No   | None   |
| TransConfig        | Request | Transcoding configuration                                    | Container | No       | None                             |

<span id="Container"></span>
`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ----------------------- | ------ | -------- |
| Format             | Request.Container | Container format. Valid values: `mp4`, `flv`, `hls`. | String | Yes       |
| ClipConfig         | Request.Container | Segment configuration. This node will take effect only when `Format` is `hls`.    | Container    | No  |

`ClipConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| -------------------| ------- | ------------------------------------| --------- | ---- |
| Duration     | Request.Container.ClipConfig | Segment duration. Default value: 5s   | String    | No   |


Audio/Video formats supported by different container formats are as follows:

| Container | Audio Codecs | Video Codecs |
| --------- | ------------ | ------------ |
| mp4/hls/mkv | AAC, MP3     | H.264, H.265 |
| flv       | AAC, MP3     | H.264        |

<span id="Video"></span>
`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | ------------------ | ------ | -------- | ----------------- | ------------------------------------------------------------ |
| Codec                      | Request.Video | Codec format             | String | No   |   H.264 | H.264, H.265  |
| Width              | Request.Video | Width                 | String | No       | Original video width | 1. Value range: [128, 4096]<br/>2.Unit: px<br/>3.If only `Width` is set, `Height` is calculated according to the original video aspect ratio.<br/>4.This parameter must be an even number. |
| Height             | Request.Video | Height                 | String | No   | Original video height | 1. Value range: [128, 4096]<br/>2.Unit: px<br/>3. If only `Height` is set, `Width` is calculated according to the original video aspect ratio.<br/>4. This parameter must be an even number. |
| Fps                        | Request.Video | Frame rate                  | String | No   | None           | 1. Value range: (0, 60]<br>2. Unit: fps |
| Profile                    | Request.Video | Encoding level              | String | No   | high         | 1. Valid values: `baseline`, `main`, `high`. <br/>2. baseline: Suitable for mobile devices<br/>3. main: Suitable for standard resolution devices <br/>4. high: Suitable for high resolution devices <br/>5. Only H.264 supports this parameter. |
| Bitrate            | Request.Video | Bitrate of the video output file | String | No       | None           | 1. Value range: [10, 50000]<br/>2. Unit: Kbps                  |
| Crf                | Request.Video | Bitrate, which is a quality control factor  | String | No       | None           | 1. Value range: (0, 51]<br/>2. If `Crf` is set, the setting of `Bitrate` will become invalid.<br/>3. If `Bitrate` is empty, `25` is used for this parameter by default. |
| Gop                | Request.Video | Maximum number of frames between two keyframes   | String | No       | None           | Value range: [0, 100000]                                       |
| Preset                     | Request.Video | Video algorithm preset        | String | No   | medium       |  1. Only H.264 supports this parameter.<br/>2. Valid values: `veryfast`, `fast`, `medium`, `slow`, `slower`. |
| Bufsize                    | Request.Video | Buffer size            | String | No   | None           | 1. Value range: [1000, 128000]<br/>2. Unit: Kb<br/> |
| Maxrate                    | Request.Video | Peak video bitrate          | String | No   | None           | 1. Value range: [10, 50000]<br/>2. Unit: Kbps<br/> |
| Pixfmt             | Request.Video | Video color format       | String | No       | None                | 1. Valid values for H.264: `yuv420p`, `auto`. <br/>2. Valid values for H.265: `yuv420p`, `yuv420p10le`, `auto`. |
| Rotate              | Request.Video | Rotation angle           | String | No   | None        | 1. Value range: [0, 360)<br/>2. Unit: Degree |

<span id="TimeInterval"></span>
`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | -------------------- | -------- | ------ | -------- | ------ | ------------------------------------------------------------ |
| Start              | Request.TimeInterval | Start time | String    | No   | None     | 1. Value range: [0, video duration] <br/> 2. Unit: Second <br/> 3. The `float` format is supported, accurate to the millisecond. |
| Duration           | Request.TimeInterval | Duration | String    | No   | None     | 1. Value range: [0, video duration] <br/> 2. Unit: Second <br/> 3. The `float` format is supported, accurate to the millisecond. |

<span id="Audio"></span>
`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | ------------ | ------ | -------- | ------ | ------------------------------------------------------------ |
| Codec              | Request.Audio | Codec format     | String | No   | aac    | Valid values: `aac`, `mp3`. |
| Samplerate         | Request.Audio | Sample rate         | String | No   | 44100  | 1. Unit: Hz<br/>2. Valid values: `11025`, `22050`, `32000`, `44100`, `48000`, `96000`.<br/>3. Different container formats support different MP3 sample rates, as shown in the table below.|
| Bitrate            | Request.Audio | Original audio bitrate   | String | No   | None     | 1. Unit: Kbps<br/>2. Value range: [8, 1000]|
| Channels           | Request.Audio | Number of sound channels         | String | No   |  None      | 1. If `Codec` is `aac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.<br/>2. If `Codec` is `mp3`, the value can be `1` or `2`. |
| Remove             | Request.Audio | Whether to delete the source audio stream | String | No   | false    | Valid values: `true`, `false`.                                             |

>? Y indicates supported, and N indicates unsupported.

| Container Format/Audio Sample Rate | 11025 | 22050 | 32000 | 44100 | 48000 | 96000 |
| ------------------- | ----- | ----- | ----- | ----- | ----- | ----- |
| flv                 | N     | Y     | N     | Y     | N     | N     |
| mp4                 | N     | Y     | Y     | Y     | Y     | N     |
| hls/mkv             | Y     | Y     | Y     | Y     | Y     | N     |

<span id="TransConfig"></span>
`TransConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------------- | ------------------- | ------ | -------- | ------ | ------------------------------------------------------------ |
| AdjDarMethod          | Request.TransConfig                        | Resolution adjustment method               | String    | No       | none   | <li>Valid values: `scale`, `crop`, `pad`, `none`.<br/><li>If the aspect ratio of the output video is different from that of the original video, the resolution is adjusted according to this parameter.<br/> |
| IsCheckReso           | Request.TransConfig                        | Whether to check the resolution               | String    | No       | false  | 1. Valid values: `true`, `false`. <br/> 2. If the value is `false`, transcoding is performed based on settings.      |
| ResoAdjMethod         | Request.TransConfig                        | Resolution adjustment method               | String    | No       | 0      | 1. Valid values: `0`, `1`. `0` indicates to use the original video resolution, and `1` indicates to return the transcoding failure message.<br/>2. This parameter will take effect only when `IsCheckReso` is `true`. |
| IsCheckVideoBitrate   | Request.TransConfig | Whether to check the video bitrate | String | No   | false  | <li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings. </li> |
| VideoBitrateAdjMethod | Request.TransConfig                        | Video bitrate adjustment method             | String    | No       | 0      | <li>Valid values: `0`, `1`. When the output video has a higher bitrate than the input video, `0` indicates to use the original video bitrate, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckVideoBitrate` is `true`.<br/> |
| IsCheckAudioBitrate   | Request.TransConfig                        | Whether to check the audio bitrate | String | No   | false  | <li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings. </li> |
| AudioBitrateAdjMethod | Request.TransConfig                        | Audio bitrate adjustment method | String | No   | 0      | <li>Valid values: `0`, `1`. When the output audio has a higher bitrate than the input audio, `0` indicates to use the original audio bitrate, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckAudioBitrate` is `true`.</li> |
| IsCheckVideoFps       | Request.TransConfig | Whether to check the video frame rate | String | No   | false  | <li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings. </li> |
| VideoFpsAdjMethod     | Request.TransConfig | Video frame rate adjustment method             | String    | No       | 0      | <li>Valid values: `0`, `1`. When the output video has a higher frame rate than the input video, `0` indicates to use the original video frame rate, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckVideoFps` is `true`.<br/> |
| DeleteMetadata        | Request.TransConfig                         | Whether to delete metadata from the file | String    | No       | false  | 1.Valid values: `true`, `false`. <br/> 2. If the value is `false`, the source file information is retained. |
| IsHdr2Sdr             | Request.TransConfig                        | Whether to enable HDR-to-SDR conversion             | String    | No       | false  | true/false                                                   |
| HlsEncrypt            | Request.TransConfig                        | HLS encryption configuration                  | Container | No       | None     | None                                                           |

The `AdjDarMethod` parameter is illustrated as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/e2eb1d7346df8f51756fdab7bdce2ca0.png)

`HlsEncrypt` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| --------------------- | ------------------- | ---------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| IsHlsEncrypt       | Request.TransConfig.HlsEncrypt | Whether to enable HLS encryption | String | No   | false  | 1. Valid values: `true`, `false`. <br/>2. Encryption is supported only when `Container.Format` is `hls`. |
| UriKey             | Request.TransConfig.HlsEncrypt | HLS encryption key    | String | No   | None     | This parameter will take effect only when `IsHlsEncrypt` is `true`.                       |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>HighSpeedHd</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <HighSpeedHd>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Fps>30</Fps>
                <Bufsize>0</Bufsize>
                <Maxrate>0</Maxrate>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </HighSpeedHd>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

<span id="Response"></span>
`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------- | :----------------------------- | :-------- |
| TemplateId         | Response.Template | Template ID                        | String    |
| Name               | Response.Template | Template name                       | String    |
| BucketId           | Response.Template | Template bucket                 | String    |
| Category           | Response.Template | Template category: Custom or Official | String    |
| Tag                | Response.Template | Template tag: HighSpeedHd                                       | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| HighSpeedHd        | Response.Template     | Template parameters                                                | Container |


`HighSpeedHd` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :-------------------------------- | :-------- |
| TimeInterval       | Response.Template.HighSpeedHd | Same as `Request.TimeInterval` in the request body.  | Container |
| Container          | Response.Template.HighSpeedHd | Same as `Request.Container` in the request body.     | Container |
| Video              | Response.Template.HighSpeedHd | Same as `Request.Video` in the request body.         | Container |
| Audio              | Response.Template.HighSpeedHd | Same as `Request.Audio` in the request body.         | Container |
| TransConfig        | Response.Template.HighSpeedHd | Same as `Request.TransConfig` in the request body.   | Container |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>HighSpeedHd</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Fps>30</Fps>
        <Bufsize>0</Bufsize>
        <Maxrate>0</Maxrate>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
    </Audio>
    <TransConfig>
        <IsCheckReso>false</IsCheckReso>
        <ResoAdjMethod>1</ResoAdjMethod>
    </TransConfig>
    <TimeInterval>
        <Start>0</Start>
        <Duration>60</Duration>
    </TimeInterval>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <Template>
        <Tag>HighSpeedHd</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <HighSpeedHd>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Fps>30</Fps>
                <Bufsize>0</Bufsize>
                <Maxrate>0</Maxrate>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </HighSpeedHd>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
