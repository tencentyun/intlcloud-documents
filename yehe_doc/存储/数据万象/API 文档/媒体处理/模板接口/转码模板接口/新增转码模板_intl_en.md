## Feature Description

This API (`CreateMediaTemplate`) is used to create a transcoding template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateTranscodeTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
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

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>Transcode</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Profile>high</Profile>
        <Bitrate>1000</Bitrate>
        <Crf></Crf>
        <Width>1280</Width>
        <Height></Height>
        <Fps>30</Fps>
        <Gop></Gop>
        <Preset>medium</Preset>
        <ScanMode></ScanMode>
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
        <AdjDarMethod>scale</AdjDarMethod>
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


`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------------------------------------------- | --------- | -------- | ------------------------------ |
| Tag                | Request | Task type: Transcode                         | String    | Yes       | None                             |
| Name               | Request | Template name. The value can contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| Container          | Request | Container format                                    | Container | Yes       | None                             |
| Video              | Request | Video information                                    | Container | No       | If `Video` is not passed in, the video information will be deleted. |
| TimeInterval       | Request | Time interval                                    | Container | No       | None                             |
| Audio              | Request | Audio information                                    | Container | No       | If `Audio` is not passed in, the audio information will be deleted. |
| TransConfig        | Request | Transcoding configuration                                    | Container | No       | None                             |


`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------- | ------ | -------- |
| Format             | Request.Container | Container format: mp4, flv, hls, ts, mp3, aac, WebM | String | Yes       |

Audio/Video formats supported by different container formats are as follows:

| Container | Audio Codecs | Video Codecs |
| --------- | ------------ | ------------ |
| MP4/HLS   | AAC, MP3     | H.264, H.265 |
| TS/MKV    | AAC, MP3     | H.264        |
| FLV       | AAC, MP3     | H.264        |
| AAC       | AAC          | Not supported       |
| MP3       | MP3          | Not supported       |
| FLAC      | FLAC         | Not supported       |
| AMR       | AMR          | Not supported       |
| WebM      | Vorbis, Opus | VP8         |


`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | ------------------ | ------ | -------- | ------------ | ------------------------------------------------------------ |
| Codec              | Request.Video | Codec format         | String | No       | `H.264`. If `format` is `WebM`, the default value is `VP8`.        | 1. H.264<br/>2. H.265<br/>3. VP8                                        |
| Width              | Request.Video | Width                 | String | No       | Original video width | 1. Value range: [128, 4096]<br/>2. Unit: px<br/>3. If only `Width` is set, `Height` is calculated according to the original video proportion.<br/>4. The value must be an even number. |
| Height             | Request.Video | Height                 | String | No       | Original video height | 1. Value range: [128, 4096]<br/>2. Unit: px<br/>3. If only `Height` is set, `Width` is calculated according to the original video proportion.<br/>4. The value must be an even number. |
| Fps                | Request.Video | Frame rate               | String | No       | None           | 1. Value range: (0, 60]<br>2. Unit: fps                           |
| Remove             | Request.Video | Whether to delete the video stream     | String | No       | false        |  Valid values: `true`, `false`                                               |
| Profile            | Request.Video | Encoding format           | String | No       | high         | 1. Valid values: `baseline`, `main`, `high` <br/>2. baseline: suitable for mobile devices<br/>3. main: suitable for standard resolution devices <br/>4. high: suitable for high resolution devices <br/>5. Only H.264 supports this parameter.<br/>6. If `Codec` is `VP8`, this parameter is not supported. |
| Bitrate            | Request.Video | Bitrate of the video output file | String | No       | None           | 1. Value range: [10, 50000]<br/>2. Unit: Kbps                     |
| Crf                | Request.Video | Bit rate, which is a quality control factor  | String | No       | None           | 1. Value range: (0, 51]<br/>2. If `Crf` is set, the setting of `Bitrate` becomes invalid. <br/>3. If `Bitrate` is empty, `25` is used for this parameter by default. |
| Gop                | Request.Video | Maximum number of frames between two key frames   | String | No       | None           | Value range: [0, 100000]                                       |
| Preset             | Request.Video | Video algorithm preset     | String | No       | medium. If `Codec` is `VP8`, the value is `good`.       | 1. H.264 supports: veryfast, fast, medium, slow, slower<br/>2. VP8 supports: good, realtime |
| Bufsize            | Request.Video | Buffer size         | String | No       | None           | 1. Value range: [1000, 128000]<br/>2. Unit: Kb<br/>3. If `Codec` is `VP8`, this parameter is not supported.               |
| Maxrate            | Request.Video | Peak video bitrate       | String | No       | None           | 1. Value range: [10, 50000]<br/>2. Unit: Kbps<br/>3. If `Codec` is `VP8`, this parameter is not supported.                |
| HlsTsTime          | Request.Video | HLS segment time        | String | No       | 5            | 1. (0, Video duration] <br/> 2. Unit: second<br/>3. If `Codec` is `VP8`, this parameter is not supported.                            |
| Pixfmt             | Request.Video | Video color format       | String | No       | None           | 1. H.264 supports: yuv420p, yuv422p, yuv444p, yuvj420p, yuvj422p, yuvj444p<br/>2. H.265 supports: yuv420p<br/>3. If `Codec` is `VP8`, this parameter is not supported. |
| LongShortMode              | Request.Video | Long and short sides adaptive          | String | No   | false        | 1. true, false<br/>2. If `Codec` is `VP8`, this parameter is not supported. |  

`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | -------------------- | -------- | ------ | -------- | ------------ | ------------------------------------------------------------ |
| Start              | Request.TimeInterval | Start time | String | No       | 0            | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds. |
| Duration           | Request.TimeInterval | Duration | String | No       | Original video duration | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds. |


`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | ------------ | ------ | -------- | ------ | ------------------------------------------------------------ |
| Codec              | Request.Audio | Codec format   | String | No       | `aac`. If `format` is `WebM`, the default value is `Vorbis`.    | Valid values: `aac`, `mp3`, `flac`, `amr`, `Vorbis`, `opus`                                     |
| Samplerate         | Request.Audio | Sample rate       | String | No       | `44100`. If `Codec` is `opus`, the default value is `48000`.  | <li>Unit: Hz<br/><li> Valid values: `8000`, `11025`, `12000`, `16000`, `22050`, `24000`, `32000`, `44100`, `48000`, `88200`, `96000`<br/><li>Different container formats support different MP3 sample rates, as shown in the table below.<br/><li>If `Codec` is `amr`, the value can only be `8000`.<br/><li>If `Codec` is `opus`, the value can be `8000`, `16000`, `24000`, or `48000`. |
| Bitrate            | Request.Audio | Original audio bitrate | String | No       | None     | <li>Unit: Kbps<br/><li>Value range: [8, 1000]                     |
| Channels           | Request.Audio | Number of sound channels       | String | No       | None     | <li>If `Codec` is `aac` or `flac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.<br/><li>If `Codec` is `mp3` or opus`, the value can only be `1` or `2`.<br/><li>If `Codec` is `Vorbis`, the value can only be `2`.<br/><li>If `Codec` is `amr`, the value can only be `1`. |
| Remove             | Request.Audio | Whether to delete the source audio stream | String | No   | false    | Valid values: `true`, `false`. If `Video.Codec` is `H.265`, this parameter is invalid.      
| KeepTwoTracks      | Request.Audio | Keep two tracks | String | No   | false    | Valid values: `true`, `false`. If `Video.Codec` is `H.265`, this parameter is invalid.
| SwitchTrack        | Request.Audio | Switch the track | String | No   | false    | Valid values: `true`, `false`. If `Video.Codec` is `H.265`, this parameter is invalid.                                       |
| SampleFormat       | Request.Audio | Sampling bit width  | String | No   | None      | 1. If `Codec` is `aac`, the value can only be `fltp`.<br/>2. If `Codec` is `mp3`, the value can be `fltp`, `s16p`, or `s32p`.<br/>3. If `Codec` is `flac, the value can only be `s16` or `s32`.<br/>4. If `Codec` is `amr`, the value can only be `s16`.<br/>5. If `Video.Codec` is `H.265`, this parameter is invalid.|

>? Y indicates supported, and N indicates unsupported.
>


`Audio.Codec` supports sample rates as follows:

<table>
   <tr>
      <th>Audio.Codec</td>
      <th>aac</td>
      <th>amr</td>
      <th>flac</td>
      <th>opus</td>
      <th>Vorbis</td>
      <th>mp3</td>
   </tr>
   <tr>
      <td>8000</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td rowspan=11>Different sample rates are supported for different container formats.</td>
   </tr>
   <tr>
      <td>11025</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>12000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>16000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>22050</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>24000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>32000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>44100</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>48000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>88200</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>96000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
   </tr>
</table>

If `Audio.Codec` is `mp3`, `Container.Format` supports sample rates as follows:

| Container Format/Audio Sample Rate | 8000 | 11025 | 12000 | 16000 | 22050 | 24000 | 32000 | 44100 | 48000 | 88200 | 96000 |
| ------------------- | ---- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| flv              | N    | Y     | N     | N     | Y     | N     | N     | Y     | N     | N     | N     |
| mp4                 | N    | N     | N     | Y     | Y     | Y     | Y     | Y     | Y     | N     | N     |
| hls/ts/mp3/mkv      | N    | Y     | Y     | Y     | Y     | Y     | Y     | Y     | Y     | N     | N     |



`TransConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| --------------------- | ------------------------------------------ | ---------------------------- | --------- | -------- | ------ | ------------------------------------------------------------ |
| AdjDarMethod          | Request.TransConfig                        | Resolution adjustment mode               | String    | No       | none   | <li>Valid values: `scale`, `crop`, `pad`, `none`<br/><li>If the aspect ratio of the output video is different from that of the original video, the resolution is adjusted according to this parameter.<br/><li>If `Video.Codec` is `H.265`, this parameter is invalid. |
| IsCheckReso           | Request.TransConfig                        | Whether to check the resolution               | String    | No       | false  | <li>true, false <br/><li>If the value is `false`, transcoding is performed based on settings.      |
| ResoAdjMethod         | Request.TransConfig                        | Resolution adjustment mode               | String    | No       | 0      | <li>Valid values: `0`, `1`. `0` indicates to use the original video resolution.<br/>`1` indicates to return the transcoding failure message.<br/><li>This parameter is valid only when `IsCheckReso` is `true`. |
| IsCheckVideoBitrate   | Request.TransConfig                        | Whether to check the video bitrate             | String    | No       | false  | <li>true, false <br/><li>If the value is `false`, transcoding is performed based on settings. <br/><li>If `Video.Codec` is `H.265`, this parameter is invalid. |
| VideoBitrateAdjMethod | Request.TransConfig                        | Video bitrate adjustment mode             | String    | No       | 0      | <li>Valid values: `0`, `1`. `0` indicates to use the original video bitrate. `1` indicates to return the transcoding failure message.<br/><li>This parameter is valid only when `IsCheckVideoBitrate` is `true`.<br/><li>If `Video.Codec` is `H.265`, this parameter is invalid. |
| IsCheckAudioBitrate   | Request.TransConfig                        | Whether to check the audio bitrate             | String    | No       | false  | <li>true, false <br/><li>If the value is `false`, transcoding is performed based on settings.<br/><li>If `Video.Codec` is `H.265`, this parameter is invalid. |
| AudioBitrateAdjMethod | Request.TransConfig                        | Audio bitrate adjustment mode             | String    | No       | 0      | <li>Valid values: `0`, `1`; `0` indicates to use the original audio bitrate. `1` indicates to return the transcoding failure message. <br/><li>This parameter is valid only when `IsCheckAudioBitrate` is `true`. <br/><li>If `Video.Codec` is `H.265`, this parameter is invalid. |
| DeleteMetadata        | Request.TransConfig                         | Whether to delete metadata from the file | String    | No       | false  | 1. true, false <br/>2. If the value is `false`, the source file information is retained. <br/>3. If `Video.Codec` is `H.265`, this parameter is invalid. |
| IsHdr2Sdr             | Request.TransConfig                        | Whether to enable HDR-to-SDR conversion             | String    | No       | false  | Valid values: `true`, `false`                                                   |
| HlsEncrypt            | Request.TransConfig                        | HLS encryption configuration                  | Container | No       | None     | None                                                           |

The `AdjDarMethod` parameter is illustrated as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/0bc73f058dcfc8ba34572fd1bcadb997.png)


`HlsEncrypt` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------------------------ | --------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| IsHlsEncrypt       | Request.TransConfig.HlsEncrypt | Whether to enable HLS encryption | String | No   | false  | 1. Valid values: `true`, `false`<br/>2. Encryption is supported only when `Container.Format` is `hls`. |
| UriKey             | Request.TransConfig.HlsEncrypt | HLS encryption key    | String | No   | None     | This parameter is valid only when `IsHlsEncrypt` is `true`.                       |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>Transcode</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <Container>
            <Format>mp4</Format>
        </Container>
        <Video>
            <Codec>H.264</Codec>
            <Profile>high</Profile>
            <Bitrate>1000</Bitrate>
            <Crf></Crf>
            <Width>1280</Width>
            <Height></Height>
            <Fps>30</Fps>
            <Gop></Gop>
            <Preset>medium</Preset>
            <ScanMode></ScanMode>
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
            <AdjDarMethod>scale</AdjDarMethod>
            <IsCheckReso>false</IsCheckReso>
            <ResoAdjMethod>1</ResoAdjMethod>
        </TransConfig>
        <TimeInterval>
            <Start>0</Start>
            <Duration>60</Duration>
        </TimeInterval>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |


`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------- | :----------------------------- | :-------- |
| TemplateId         | Response.Template | Template ID                        | String    |
| Name               | Response.Template | Template name                       | String    |
| BucketId           | Response.Template | Template bucket                 | String    |
| Category           | Response.Template | Template category: Custom or Official | String    |
| Tag                | Response.Template | Task type: Transcode            | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| TransTpl           | Response.Template | Template parameters                 | Container |


`TransTpl` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :------------------------------------- | :-------- |
| TimeInterval       | Response.Template.TransTpl | Same as `Request.TimeInterval` in the request body. | Container |
| Container          | Response.Template.TransTpl | Same as `Request.Container` in the request body.    | Container |
| Video              | Response.Template.TransTpl | Same as `Request.Video` in the request body.        | Container |
| Audio              | Response.Template.TransTpl | Same as `Request.Audio` in the request body.        | Container |
| TransConfig        | Response.Template.TransTpl | Same as `Request.TransConfig` in the request body.  | Container |


#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Examples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>Transcode</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Profile>high</Profile>
        <Bitrate>1000</Bitrate>
        <Crf></Crf>
        <Width>1280</Width>
        <Height></Height>
        <Fps>30</Fps>
        <Gop></Gop>
        <Preset>medium</Preset>
        <ScanMode></ScanMode>
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
        <AdjDarMethod>scale</AdjDarMethod>
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
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <Template>
        <Tag>Transcode</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <Container>
            <Format>mp4</Format>
        </Container>
        <Video>
            <Codec>H.264</Codec>
            <Profile>high</Profile>
            <Bitrate>1000</Bitrate>
            <Crf></Crf>
            <Width>1280</Width>
            <Height></Height>
            <Fps>30</Fps>
            <Gop></Gop>
            <Preset>medium</Preset>
            <ScanMode></ScanMode>
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
            <AdjDarMethod>scale</AdjDarMethod>
            <IsCheckReso>false</IsCheckReso>
            <ResoAdjMethod>1</ResoAdjMethod>
        </TransConfig>
        <TimeInterval>
            <Start>0</Start>
            <Duration>60</Duration>
        </TimeInterval>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
