## Feature Description

This API (`UpdateMediaTemplate`) is used to update a transcoding template.

## Request

#### Sample request

```shell
PUT /template/<TemplateId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

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
| :----------------- | :----- | :---------------------------------------- | :-------- | ---- |
| Request            | None     | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |----|
| Tag                | Request | Job type: Transcode                         | String    | Yes       | None                             |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (*).                    | String    | Yes   | None |
| Container          | Request | Container format                                    | Container | Yes       | None                             |
| Video              | Request | Video information                                    | Container | No       | If `Video` is not passed in, the video information will be deleted. |
| TimeInterval       | Request | Time interval                                    | Container | No       | None                             |
| Audio              | Request | Audio information                                    | Container | No       | If `Audio` is not passed in, the audio information will be deleted. |
| TransConfig        | Request | Transcoding configuration                                    | Container | No       | None                             |

`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ---------------------------------------------------- | --------- | ---- |
| Format             | Request.Container | Container format. Valid values: mp4, flv, hls, ts, mp3, aac, WebM, dash, mov, avi | String | Yes       |
| ClipConfig         | Request.Container | Segment configuration. This node is valid only when `format` is `hls` or `dash`.    | Container    | No  |

`ClipConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| -------------------| ------- | ------------------------------------| --------- | ---- |
| Duration     | Request.Container.ClipConfig | Segment duration. Default value: 5s   | String    | No   |

Audio/Video formats supported by different container formats are as follows:

| Container | Audio Codecs | Video Codecs |
| --------- | ------------ | ------------ |
| mp4/hls/mkv | aac, mp3    | H.264, H.265 |
| ts/flv    | aac, mp3      | H.264        |
| AAC       | AAC          | Not supported       |
| MP3       | MP3          | Not supported       |
| FLAC      | FLAC         | Not supported       |
| AMR       | AMR          | Not supported       |
| WebM      | Vorbis, Opus | VP8, VP9     |
| dash      | aac          | H.264     |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec              | Request.Video | Codec format         | String | No       | H.264. If `format` is `WebM`, the default value is `VP8`.        | 1. H.264<br/>2. H.265<br/>3. VP8 <br/>4. VP9   |
| Width              | Request.Video | Width                 | String | No       | Original video width | 1. Value range: [128, 4096]<br/>2.Unit: px<br/>3.If only `Width` is set, `Height` is calculated according to the original video aspect ratio.<br/>4.This parameter must be an even number. |
| Height             | Request.Video | Height                 | String | No   | Original video height | 1. Value range: [128, 4096]<br/>2.Unit: px<br/>3. If only `Height` is set, `Width` is calculated according to the original video aspect ratio.<br/>4. This parameter must be an even number. |
| Fps                        | Request.Video | Frame rate                  | String | No   | None           | 1. Value range: (0, 60]<br>2. Unit: fps |
| Remove             | Request.Video | Whether to delete the video stream     | String | No       | false        |  Valid values: true, false                                               |
| Profile            | Request.Video | Encoding level           | String | No       | high         | 1. Valid values: baseline, main, high, auto<br/>2. If `Pixfmt` is `auto`, this parameter can only be `auto` and will be changed to `auto` if set to other values.<br/>3. baseline: Suitable for mobile devices.<br/>4. main: Suitable for standard resolution devices.<br/>5. high: Suitable for high resolution devices.<br/>6. Only H.264 supports this parameter. |
| Bitrate            | Request.Video | Bitrate of the video output file | String | No       | None           | 1. Value range: [10, 50000]<br/>2. Unit: Kbps                  |
| Crf                | Request.Video | Bitrate, which is a quality control factor  | String | No       | None           | 1. Value range: (0, 51]<br/>2. If `Crf` is set, the setting of `Bitrate` becomes invalid.<br/>3. If `Bitrate` is empty, `25` is used for this parameter by default. |
| Gop                | Request.Video | Maximum number of frames between two keyframes   | String | No       | None           | Value range: [1, 100000]                                       |
| Preset             | Request.Video | Video algorithm preset     | String | No       | medium. If `Codec` is `VP8`, the value is `good`.       | 1. H.264 supports: veryfast, fast, medium, slow, slower<br/>2. VP8 supports: good, realtime<br/>3. H.265 and VP9 don't support this parameter. |
| Bufsize            | Request.Video | Buffer size         | String | No       | None           | 1. Value range: [1000, 128000]<br/>2.  Unit: KB<br/>3. If `Codec` is `VP8` or `VP9`, this parameter is not supported.              |
| Maxrate            | Request.Video | Peak video bitrate       | String | No       | None           | 1. Value range: [10, 50000]<br/>2. Unit: Kbps<br/>3. If `Codec` is `VP8` or `VP9`, this parameter is not supported.                |
| Pixfmt             | Request.Video | Video color format       | String | No       | None           | 1. Valid values for H.264: yuv420p, yuv422p, yuv444p, yuvj420p, yuvj422p, yuvj444p, auto<br/>2. Valid values for H.265: yuv420p, yuv420p10le, auto<br/>3. If `Codec` is `VP8` or `VP9`, this parameter is not supported. |
| LongShortMode              | Request.Video | Whether to use long short mode          | String | No   | false        | 1. Valid values: true, false<br/>2. If `Codec` is `VP8` or `VP9`, this parameter is not supported. |
| Rotate              | Request.Video | Rotation angle           | String | No   | None        | 1. Value range: [0, 360)<br/>2. Unit: degree |

`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Request.TimeInterval | Start time | String    | No   | 0 | <ul  style="margin: 0;"><li>[0, video duration] </li><li>Unit: second </li><li>Supports the float format, accurate to the millisecond.</li></ul> |
| Duration             | Request.TimeInterval | Duration | String    | No   | Video duration | <ul  style="margin: 0;"><li>[0, video duration] </li><li>Unit: second </li><li>Supports the float format, accurate to the millisecond.</li></ul> |

`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | -------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| Codec              | Request.Audio | Codec format   | String | No       | `aac`. If `format` is `WebM`, the default value is `Vorbis`.    | Valid values: aac, mp3, flac, amr, Vorbis, opus                                     |
| Samplerate         | Request.Audio | Sample rate       | String | No       | `44100`. If `Codec` is `opus`, the default value is `48000`.  | <ul  style="margin: 0;"><li>Unit: Hz</li><li>Valid values: 8000, 11025, 12000, 16000, 22050, 24000, 32000, 44100, 48000, 88200, 96000</li><li>Different container formats support different MP3 sample rates, as shown in the table below.</li><li>If `Codec` is `amr`, the value can only be `8000`.</li><li>If `Codec` is `opus`, the value can be `8000`, `16000`, `24000`, or `48000`.</li></ul> |
| Bitrate            | Request.Audio | Original audio bitrate | String | No       | None     | <ul  style="margin: 0;"><li>Unit: Kbps</li><li>Value range: [8, 1000] </li></ul>          |
| Channels           | Request.Audio | Number of sound channels       | String | No       | None     | <ul  style="margin: 0;"><li>If `Codec` is `aac` or `flac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.</li><li>If `Codec` is `mp3` or `opus`, the value can only be `1` or `2`.</li><li>If `Codec` is `Vorbis`, the value can only be `2`.</li><li>If `Codec` is `amr`, the value can only be `1`.</li><li>If `Codec` is `dash`, the value cannot be `8`.</li></ul> |
| Remove             | Request.Audio | Whether to delete the source audio stream | String | No   |   false    | Valid values: true, false                                            |
| KeepTwoTracks      | Request.Audio | Keep double audio track | String | No   | false    | Valid values: true, false. If `Video.Codec` is `H.265`, this parameter is invalid.       |
| SwitchTrack        | Request.Audio | Switch the track | String | No   | false    | Valid values: true, false. If `Video.Codec` is `H.265`, this parameter is invalid.                                       |
| SampleFormat       | Request.Audio | Sampling bit width  | String | No   | None      | <ul  style="margin: 0;"><li>If `Codec` is `aac`, the value can only be `fltp`.</li><li>If `Codec` is `mp3`, the value can be `fltp`, `s16p`, or `s32p`.</li><li>If `Codec` is `flac`, the value can only be `s16` or `s32`.</li><li>If `Codec` is `amr`, the value can only be `s16`.</li><li>If `Video.Codec` is `H.265`, this parameter is invalid.</li></ul>|


>? Y indicates supported, and N indicates unsupported.
>


`Audio.Codec` supports the sample rates as shown below:

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

If `Audio.Codec` is `mp3`, `Container.Format` supports the sample rates as shown below:

| Container Format/Audio Sample Rate | 8000 | 11025 | 12000 | 16000 | 22050 | 24000 | 32000 | 44100 | 48000 | 88200 | 96000 |
| ------------------- | ---- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| flv	              | N    | N     | N     | N     | Y     | N     | N     | Y     | N     | N     | N     |
| mp4                 | N    | N     | N     | Y     | Y     | Y     | Y     | Y     | Y     | N     | N     |
| hls/ts/mp3/mkv      | N    | Y     | Y     | Y     | Y     | Y     | Y     | Y     | Y     | N     | N     |


`TransConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| --------------------- | ------------------- | ---------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| AdjDarMethod          | Request.TransConfig                        | Resolution adjustment method               | String    | No       | none   | <ul  style="margin: 0;"><li>Valid values: scale, crop, pad, none</li><li>If the aspect ratio of the output video is different from that of the original video, the resolution is adjusted according to this parameter.</li></ul>  |
| IsCheckReso           | Request.TransConfig                        | Whether to check the resolution               | String    | No       | false  | <ul  style="margin: 0;"><li>Valid values: true, false </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul>      |
| ResoAdjMethod         | Request.TransConfig                        | Resolution adjustment method               | String    | No       | 0      | <ul  style="margin: 0;"><li>Valid values: 0, 1. `0` indicates to use the original video resolution. `1` indicates to return the transcoding failure message.</li><li>This parameter is valid only when `IsCheckReso` is `true`.</li></ul> |
| IsCheckVideoBitrate   | Request.TransConfig                        | Whether to check the video bitrate             | String    | No       | false  | <ul  style="margin: 0;"><li>Valid values: true, false </li><li>If the value is `false`, transcoding is performed based on settings. </li><li>If the video codec is H.265, this parameter is invalid.</li></ul> |
| VideoBitrateAdjMethod | Request.TransConfig                        | Video bitrate adjustment method             | String    | No       | 0      | <ul  style="margin: 0;"><li>Valid values: 0, 1. `0` indicates to use the original video bitrate. `1` indicates to return the transcoding failure message.</li><li>This parameter is valid only when `IsCheckVideoBitrate` is `true`.</li><li>If the video codec is H.265, this parameter is invalid.</li></ul>  |
| IsCheckAudioBitrate   | Request.TransConfig                        | Whether to check the audio bitrate | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: true, false </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul> |
| AudioBitrateAdjMethod | Request.TransConfig                        | Audio bitrate adjustment method | String | No   | 0      | <ul  style="margin: 0;"><li>Valid values: 0, 1. `0` indicates to use the original audio bitrate. `1` indicates to return the transcoding failure message.</li><li>This parameter is valid only when `IsCheckAudioBitrate` is `true`.</li></ul>|
| DeleteMetadata        | Request.TransConfig                         | Whether to delete metadata from the file | String    | No       | false  | <ul  style="margin: 0;"><li>Valid values: true, false </li><li>If the value is `false`, the source file information is retained.</li></ul> |
| IsHdr2Sdr             | Request.TransConfig                        | Whether to enable HDR-to-SDR conversion             | String    | No       | false  | Valid values: true, false                                                   |
| HlsEncrypt            | Request.TransConfig                        | HLS encryption configuration                  | Container | No       | None     | None                                                           |

The `AdjDarMethod` parameter is illustrated as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/e2eb1d7346df8f51756fdab7bdce2ca0.png)


`HlsEncrypt` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| --------------------- | ------------------- | ---------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| IsHlsEncrypt       | Request.TransConfig.HlsEncrypt | Whether to enable HLS encryption | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: true, false</li><li>Encryption is supported only when `Video.Codec` is `H264` or `H265` and `Container.Format` is `hls`.</li></ul> |
| UriKey             | Request.TransConfig.HlsEncrypt | HLS encryption key    | String | No   | None     | This parameter is valid only when `IsHlsEncrypt` is `true`.                       |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

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

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------- | :-------- |
| Response           | None     | Response container, which is the same as `Response` in `CreateMediaTemplate`. | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response | Template ID                                                      | String    |
| Name               | Response | Template name                                                     | String    |
| Tag                | Response | Template type: Transcode                                           | String    |
| UpdateTime         | Response | Update time                                                     | String    |
| TimeInterval       | Response | Same as `Request.TimeInterval` in the request body. | Container |
| Container          | Response | Same as `Request.Container` in the request body.    | Container |
| Video              | Response | Same as `Request.Video` in the request body.         | Container |
| Audio              | Response | Same as `Request.Audio` in the request body.        | Container |
| TransConfig        | Response | Same as `Request.TransConfig` in the request body.  | Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Use Cases

#### Request

```shell
PUT /template/<TemplateId> HTTP/1.1
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

