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
| :----------------- | :----- | :---------------------------------------- | :-------- | ---- |
| Request            | None     | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |----|
| Tag                | Request | Task type: Transcode                                    | String    | Yes   | None |
| Name               | Request | Template name. The value can contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (*).                    | String    | Yes   | None |
| Container          | Request | Container format                                               | Container | Yes   | None |
| Video              | Request | Video information                                               | Container | No   | If `Video` is not passed in, the video information will be deleted. |
| TimeInterval       | Request | Time interval                                               | Container | No   | None |
| Audio              | Request | Audio information                                               | Container | No   | If `Audio` is not passed in, the audio information will be deleted. |
| TransConfig        | Request | Transcoding configuration                                               | Container | No   | None |

`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ---------------------------------------------------- | --------- | ---- |
| Format                | Request.Container | Container format: mp4, flv, hls, ts               | String    | Yes   |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Request.Video | Codec format            | String | No   |   Original video codec | H.264                                          |
| Width                      | Request.Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]<br/> <li>Unit: px<br/> <li>If only `Width` is set, `Height` is calculated according to the original video proportion. |
| Height                     | Request.Video | Height                    | String | No   | Original video height |  <li>Value range: [128, 4096]<br/> <li>Unit: px<br/> <li>If only `Height` is set, `Width` is calculated according to the original video proportion. |
| Fps                        | Request.Video | Frame rate                  | String | No   | Original video frame rate |  <li>Value range: (0, 60]<br> <li>Unit: fps<br> <li>If the frame rate is greater than 60, set this parameter to `60`.<br/>This parameter is optional. If it is not set, the video is played at the speed as per the original timestamp. This parameter specifies the frame rate for animated image playback. |
| Remove                     | Request.Video | Whether to delete the video stream        | String | No   | false        | true, false                                               |
| Profile                    | Request.Video | Encoding format              | String | No   | high         |  <li>Valid values: baseline, main, high<br/><li>baseline: suitable for mobile devices<br/><li>main: suitable for standard resolution devices<br/><li>high: suitable for high resolution devices<br/><li>Only H.264 supports this parameter. |
| Bitrate                    | Request.Video | Bitrate of the video output file    | String | No   |  Original video bitrate           |  <li>Value range: [10, 50000]<br/> <li>Unit: Kbps                     |
| Crf                        | Request.Video | Bit rate, which is a quality control factor     | String | No   | Null           |  <li>Value range: [0, 51]<br/> <li>If `Crf` is set, the setting of `Bitrate` becomes invalid. <br/> <li>`Crf` is not set by default.  |
| Gop                        | Request.Video | Maximum number of frames between two key frames      | String | No   |  Null            | <li>Value range: [0, 100000]  <br/> <li>`Gop` is not set by default.                                        |
| Preset                     | Request.Video | Video algorithm preset        | String | No   | medium       |  <li>Only H.264 supports this parameter.<br/> <li>Valid values: veryfast, fast, medium, slow, slower |
| Bufsize                    | Request.Video | Buffer size            | String | No   | 0            |  <li>Value range: [1000, 128000]<br/> <li>Unit: Kb<br/> <li>The default value is `0`, indicating that buffer is not used. |
| Maxrate                    | Request.Video | Peak video bitrate          | String | No   | 0            |  <li>Value range: [10, 50000]<br/> <li>Unit: Kbps<br/> <li>The default value is `0`, indicating that this parameter is not used. |
| HlsTsTime                  | Request.Video | HLS segment time          | String | No   | 5            | <li>(0, Video duration] <br/><li>Unit: second |
| Pixfmt                     | Request.Video | Video color format          | String | No   | yuv420p          | Valid values: yuv420p, yuv422p, yuv444p, yuvj420p, yuvj422p, yuvj444p |
| LongShortMode              | Request.Video | Long and short sides adaptive          | String | No   | false        | true, false

`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Request.TimeInterval | Start time | String    | No   | 0 |  <li>[0, Video duration] <br/> <li>Unit: second <br/> <li>Supports the float format, accurate to milliseconds. |
| Duration             | Request.TimeInterval | Duration | String    | No   | Video duration |  <li>[0, Video duration] <br/> <li>Unit: second <br/> <li>Supports the float format, accurate to milliseconds. |

`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | -------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| Codec              | Request.Audio | Codec format     | String | No   | aac    | Valid values: aac, mp3                                                |
| Samplerate         | Request.Audio | Sample rate         | String | No   | 44100  |  <li>Unit: Hz<br/> <li>44100, 32000, 44100, 48000, 96000<br/> <li>If the container format is FLV and the audio codec format is MP3, the sample rate cannot be 32000, 48000, or 96000. If the audio codec format is MP3, the sample rate cannot be 96000. |
| Bitrate            | Request.Audio | Original audio bitrate   | String | No   | 128    |  <li>Unit: Kbps<br/> <li>Value range: [8, 1000]                       |
| Channels           | Request.Audio | Number of sound channels         | String | No   |  None      |  <li>If `Codec` is `aac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.<br/><li>If `Codec` is `mp3`, the value can be `1` or `2`. |
| Remove             | Request.Audio | Whether to delete the audio stream | String | No   |   None    | Valid values: true, false                                             |

`TransConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| --------------------- | ------------------- | ---------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| AdjDarMethod          | Request.TransConfig | Resolution adjustment mode   | String | No   | none   |  <li>Valid values: scale, crop, pad, none<br/> <li>If the aspect ratio of the output video is different from that of the original video, the resolution is adjusted according to this parameter. |
| IsCheckReso           | Request.TransConfig | Whether to check the resolution   | String | No   | false  |  <li>true, false <br/> <li>If the value is `false`, transcoding is performed based on settings. |
| ResoAdjMethod         | Request.TransConfig | Resolution adjustment mode   | String | No   | 0      |  <li>Valid values: `0`, `1`. `0` indicates to use the original video resolution. `1` indicates to return the transcoding failure message.<br/> <li>This parameter is valid only when `IsCheckReso` is `true`. |
| IsCheckVideoBitrate   | Request.TransConfig | Whether to check the video bitrate | String | No   | false  |  <li>true, false <br/> <li>If the value is `false`, transcoding is performed based on settings. |
| VideoBitrateAdjMethod | Request.TransConfig | Video bitrate adjustment mode | String | No   | 0      |  <li>Valid values: `0`, `1`. `0` indicates to use the original video bitrate. `1` indicates to return the transcoding failure message.<br/> <li>This parameter is valid only when `IsCheckVideoBitrate` is `true`. |
| IsCheckAudioBitrate   | Request.TransConfig | Whether to check the audio bitrate | String | No   | false  |  <li>true, false <br/> <li>If the value is `false`, transcoding is performed based on settings.<br/> |
| AudioBitrateAdjMethod | Request.TransConfig | Audio bitrate adjustment mode | String | No   | 0      |  <li>Valid values: `0`, `1`; `0` indicates to use the original audio bitrate. `1` indicates to return the transcoding failure message.<br/> <li>This parameter is valid only when `IsCheckAudioBitrate` is `true`. |

The `AdjDarMethod` parameter is illustrated as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/0bc73f058dcfc8ba34572fd1bcadb997.png)

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
| :----------------- | :----- | :----------------------------------------- | :-------- |
| Response           | None     | Response container. Same as `Response` in `CreateMediaTemplate`.  | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response | Template ID                                                      | String    |
| Name               | Response | Template name                                                     | String    |
| Tag                | Response | Task type: Transcode                                          | String    |
| UpdateTime         | Response | Update time                                                     | String    |
| TimeInterval       | Response | Same as `Request.TimeInterval` in the request body. | Container |
| Container          | Response | Same as `Request.Container` in the request body.    | Container |
| Video              | Response | Same as `Request.Video` in the request body.        | Container |
| Audio              | Response | Same as `Request.Audio` in the request body.        | Container |
| TransConfig        | Response | Same as `Request.TransConfig` in the request body.  | Container |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

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
