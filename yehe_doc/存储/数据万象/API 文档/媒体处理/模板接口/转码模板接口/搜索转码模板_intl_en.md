## Feature Description
This API (`DescribeMediaTemplates`) is used to search for transcoding templates.

## Request

#### Sample request

```shell
GET /template HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

```

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
The request body of this request is empty.

#### Request parameters
The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---           |:--       |:--                    |   :--     |   :--    |
| tag           | None        | Task type: Transcode       | String    |Yes|
| category      | None   | Template category: Custom (default) or Official | String    |Yes|
| ids           | None        | Template ID. If you enter multiple IDs, separate them with commas (,).  | String     |No|
| name          | None        | Template name prefix              | String     |No|
| pageNumber    | None        | Page number                   | Integer     |No|
| pageSize      | None        | Records per page                 | Integer     |No|


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Transcode</Tag>
        <TransTpl>
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
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------- | :-------- |
| RequestId          | Response | Unique ID of the request                   | String    |
| TotalCount         | Response | Total number of templates                       | Int       |
| PageNumber         | Response | Current page number. Same as `pageNumber` in the request. | Int       |
| PageSize           | Response | Number of records per page. Same as `pageSize` in the request.   | Int       |
| TemplateList       | Response | Template array                       | Container |

`TemplateList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.TemplateList | Template ID                                                      | String    |
| Name               | Response.TemplateList | Template name                                                     | String    |
| BucketId           | Response.TemplateList | Template bucket                                                | String    |
| Category           | Response.TemplateList | Template category: Custom or Official                                | String    |
| Tag                | Response.TemplateList | Task type: Transcode                                          | String    |
| UpdateTime         | Response.TemplateList | Update time                                                     | String    |
| CreateTime         | Response.TemplateList | Creation time                                                     | String    |
| TransTpl           | Response.TemplateList | Template parameters                                                | Container |

`TransTpl` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :------- | :-------- |
| TimeInterval       | Response.TemplateList.TransTpl | Time interval | Container |
| Container          | Response.TemplateList.TransTpl | Container format | Container |
| Video              | Response.TemplateList.TransTpl | Video information | Container |
| Audio              | Response.TemplateList.TransTpl | Audio information | Container |
| TransConfig        | Response.TemplateList.TransTpl | Transcoding configuration | Container |

`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ---------------------------------------------------- | --------- | ---- |
| Format                | Request.Container | Container format: mp4, flv, hls, ts               | String    | Yes   |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Response.TemplateList.<br/>TransTpl.Video | Codec format            | String | No   |   Original video codec | H.264                                          |
| Width                      | Response.TemplateList.<br/>TransTpl.Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li> If only `Width` is set, `Height` is calculated according to the original video proportion. |
| Height                     | Response.TemplateList.<br/>TransTpl.Video | Height                    | String | No   | Original video height | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li> If only `Height` is set, `Width` is calculated according to the original video proportion. |
| Fps                        | Response.TemplateList.<br/>TransTpl.Video | Frame rate                  | String | No   | Original video frame rate | <li>Value range: (0, 60]<br><li>Unit: fps<br><li>If the frame rate is greater than 60, set this parameter to `60`.<br/>This parameter is optional. If it is not set, the video is played at the speed as per the original timestamp. This parameter specifies the frame rate for animated image playback. |
| Remove                     | Response.TemplateList.<br/>TransTpl.Video | Whether to delete the video stream        | String | No   | false        | true, false                                               |
| Profile                    | Response.TemplateList.<br/>TransTpl.Video | Encoding format              | String | No   | high         | <li>Valid values: baseline, main, high<br/><li>baseline: suitable for mobile devices<br/><li>main: suitable for standard resolution devices<br/><li>high: suitable for high resolution devices<br/><li>Only H.264 supports this parameter. |
| Bitrate                    | Response.TemplateList.<br/>TransTpl.Video | Bitrate of the video output file    | String | No   |  Original video bitrate          | <li>Value range: [10, 50000]<br/><li>Unit: Kbps                     |
| Crf                        | Response.TemplateList.<br/>TransTpl.Video | Bit rate, which is a quality control factor     | String | No   | Null           | <li>Value range: [0, 51]<br/><li>If `Crf` is set, the setting of `Bitrate` becomes invalid. <br/><li>`Crf` is not set by default. |
| Gop                        | Response.TemplateList.<br/>TransTpl.Video | Maximum number of frames between two key frames      | String | No   |  Null            | Value range: <li>[0, 100000] <br/><li>`Gop` is not set by default.                                       |
| Preset                     | Response.TemplateList.<br/>TransTpl.Video | Video algorithm preset        | String | No   | medium       | <li>Only H.264 supports this parameter.<br/><li>Valid values: veryfast, fast, medium, slow, slower |
| Bufsize                    | Response.TemplateList.<br/>TransTpl.Video | Buffer size            | String | No   | 0            | <li>Value range: [1000, 128000]<br/><li>Unit: Kb<br/><li>The default value is `0`, indicating that buffer is not used. |
| Maxrate                    | Response.TemplateList.<br/>TransTpl.Video | Peak video bitrate          | String | No   | 0            | <li>Value range: [10, 50000]<br/><li>Unit: Kbps<br/><li>The default value is `0`, indicating that this parameter is not used. |
| HlsTsTime                  | Response.TemplateList.<br/>TransTpl.Video | HLS segment time          | String | No   | 5            | <li>Value range: (0, Video duration] <br/> <li>Unit: second |
| Pixfmt                     | Response.TemplateList.<br/>TransTpl.Video | Video color format          | String | No   |     yuv420p       | Valid values: yuv420p, yuv422p, yuv444p, yuvj420p, yuvj422p, yuvj444p |
| LongShortMode              | Response.TemplateList.<br/>TransTpl.Video | Long and short sides adaptive          | String | No   | false        | true, false

`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Response.TemplateList.<br/>TransTpl.TimeInterval | Start time | String    | No   | 0 | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds. |
| Duration             | Response.TemplateList.<br/>TransTpl.TimeInterval | Duration | String    | No   | Video duration | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds. |

`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | -------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| Codec              | Response.TemplateList.<br/>TransTpl.Audio | Codec format     | String | No   | aac    | Valid values: aac, mp3                                                |
| Samplerate         | Response.TemplateList.<br/>TransTpl.Audio | Sample rate         | String | No   | 44100  | <li>Unit: Hz<br/><li>44100, 32000, 44100, 48000, 96000<br/> <li>If the container format is FLV and the audio codec format is MP3, the sample rate cannot be 32000, 48000, or 96000. If the audio codec format is MP3, the sample rate cannot be 96000. |
| Bitrate            | Response.TemplateList.<br/>TransTpl.Audio | Original audio bitrate   | String | No   | 128    | <li>Unit: Kbps<br/><li>Value range: [8, 1000]                       |
| Channels           | Response.TemplateList.<br/>TransTpl.Audio | Number of sound channels         | String | No   |  None      | <li>If `Codec` is `aac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.<br/><li>If `Codec` is `mp3`, the value can be `1` or `2`. |
| Remove             | Response.TemplateList.<br/>TransTpl.Audio | Whether to delete the audio stream | String | No   |   None    | Valid values: true, false                                             |

`TransConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| --------------------- | ------------------- | ---------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| AdjDarMethod          | Response.TemplateList.<br/>TransTpl.TransConfig | Resolution adjustment mode   | String | No   | none   | <li>Valid values: scale, crop, pad, none<br/><li>If the aspect ratio of the output video is different from that of the original video, the resolution is adjusted according to this parameter. |
| IsCheckReso           | Response.TemplateList.<br/>TransTpl.TransConfig | Whether to check the resolution   | String | No   | false  | <li>true, false <br/><li>If the value is `false`, transcoding is performed based on settings. |
| ResoAdjMethod         | Response.TemplateList.<br/>TransTpl.TransConfig | Resolution adjustment mode   | String | No   | 0      | <li>Valid values: `0`, `1`. `0` indicates to use the original video resolution. `1` indicates to return the transcoding failure message.<br/><li>This parameter is valid only when `IsCheckReso` is `true`. |
| IsCheckVideoBitrate   | Response.TemplateList.<br/>TransTpl.TransConfig | Whether to check the video bitrate | String | No   | false  | <li>true, false <br/><li>If the value is `false`, transcoding is performed based on settings. |
| VideoBitrateAdjMethod | Response.TemplateList.<br/>TransTpl.TransConfig | Video bitrate adjustment mode | String | No   | 0      | <li>Valid values: `0`, `1`. `0` indicates to use the original video bitrate. `1` indicates to return the transcoding failure message.<br/><li>This parameter is valid only when `IsCheckVideoBitrate` is `true`. |
| IsCheckAudioBitrate   | Response.TemplateList.<br/>TransTpl.TransConfig | Whether to check the audio bitrate | String | No   | false  | <li>true, false <br/><li>If the value is `false`, transcoding is performed based on settings.<br/> |
| AudioBitrateAdjMethod | Response.TemplateList.<br/>TransTpl.TransConfig | Audio bitrate adjustment mode | String | No   | 0      | <li>Valid values: `0`, `1`. `0` indicates to use the original audio bitrate. `1` indicates to return the transcoding failure message.<br/><li>This parameter is valid only when `IsCheckAudioBitrate` is `true`. |

The `AdjDarMethod` parameter is illustrated as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/0bc73f058dcfc8ba34572fd1bcadb997.png)


#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43609).

## Examples
**Example 1: query by template ID**
#### Request

```shell
GET /template?ids=A,B,C HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
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
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Transcode</Tag>
        <TransTpl>
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
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
    <NonExistTIDs>
        <TemplateId>B</TemplateId>
        <TemplateId>C</TemplateId>
    </NonExistTIDs>
</Response>
```

**Example 2: query by paginated list**

#### Request

```shell
GET /template?pageSize=10&pageNumber=1 HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
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
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Transcode</Tag>
        <TransTpl>
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
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
</Response>
```
