## Feature Description

This API is used to create a video montage template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateSnapshotTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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
    <Tag>VideoMontage</Tag>
    <Name>TemplateName</Name>
    <Duration>10.5</Duration>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Fps>30</Fps>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
        <Remove>false</Remove>
    </Audio>
    <AudioMix>
        <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
        <MixMode>Once</MixMode>
        <Replace>true</Replace>
    </AudioMix>
</Request>

```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------------------------------------------- | --------- | -------- | ------------------------------------------------------------ |
| Tag                | Request | Template tag: VideoMontage                                | String    | Yes   | None |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| Duration           | Request | Video montage duration                                                 | String    | No   | 1. The default value is the automatically analyzed duration.</br>2. Unit: Second</br>3. Supports the float format, accurate to the millisecond. |
| Container          | Request | Container format                                    | Container | Yes       | None                             |
| Video              | Request | Video information                                                 | Container | Yes   | None   |
| Audio              | Request | Audio information                                                 | Container | No   | None   |
| AudioMix           | Request | Audio mix parameter as described in <a href="https://intl.cloud.tencent.com/document/product/1045/49945" target="_blank">Structure</a>.                                    | Container array | No   | Valid only if `Audio.Remove` is `false` |

<span id="Container"></span>
`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | -------------------------------- | ------ | -------- |
| Format             | Request.Container | Container format. Valid values: `mp4`, `flv`, `hls`, `ts`, `mkv`. | String | Yes       |

Audio/Video formats supported by different container formats are as follows:

| Container      | Audio Codecs | Video Codecs |
| -------------- | ------------ | ------------ |
| mp4/ts/hls/mkv | AAC, MP3     | H.264, H.265 |
| flv            | AAC, MP3     | H.264        |

<span id="Video"></span>
`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | ------------------ | ------ | -------- | ------------ | ------------------------------------------------------------ |
| Codec                      | Request.Video | Codec format             | String | No   |   H.264 | 1. H.264<br/> 2.H.265  |
| Width              | Request.Video | Width                 | String | No       | Original video width | 1. Value range: [128, 4096]<br/>2.Unit: px<br/>3.If only `Width` is set, `Height` is calculated based on the original video aspect ratio.<br/>4.This parameter must be an even number. |
| Height             | Request.Video | Height                 | String | No   | Original video height | 1. Value range: [128, 4096]<br/>2.Unit: px<br/>3. If only `Height` is set, `Width` is calculated based on the original video aspect ratio.<br/>4. This parameter must be an even number. |
| Fps                        | Request.Video | Frame rate                  | String | No   | None           | 1. Value range: (0, 60]<br>2. Unit: fps |
| Bitrate            | Request.Video | Bitrate of the video output file | String | No       | None           | 1. Value range: [10, 50000]<br/>2. Unit: Kbps                  |
| Crf                | Request.Video | Bitrate, which is a quality control factor  | String | No       | None           | 1. Value range: (0, 51]<br/>2. If `Crf` is set, the setting of `Bitrate` becomes invalid.<br/>3. If `Bitrate` is empty, `25` is used for this parameter by default. |
| Rotate              | Request.Video | Rotation angle           | String | No   | None        | 1. Value range: [0, 360)<br/>2. Unit: Degree |

<span id="Audio"></span>
`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | -------------- | ------ | -------- | ------ | ------------------------------------------------------------ |
| Codec              | Request.Audio | Codec format     | String | No   | aac    | Valid values: `aac`, `mp3`. |
| Samplerate         | Request.Audio | Sample rate         | String | No   | 44100  | 1. Unit: Hz<br/>2. Valid values: `11025`, `22050`, `32000`, `44100`, `48000`, `96000`.<br/>3. Different container formats support different MP3 sample rates, as shown in the table below.|
| Bitrate            | Request.Audio | Original audio bitrate   | String | No   | None     | 1. Unit: Kbps<br/>2. Value range: [8, 1000]|
| Channels           | Request.Audio | Number of sound channels         | String | No   |  None      | 1. If `Codec` is `aac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.<br/>2. If `Codec` is `mp3`, the value can be `1` or `2`. |
| Remove             | Request.Audio | Whether to delete the audio stream | String | No   | false    | Valid values: `true`, `false`.                                             |

>? Y indicates supported, and N indicates unsupported.

| Container Format/Audio Sample Rate | 11025 | 22050 | 32000 | 44100 | 48000 | 96000 |
| ------------------- | ----- | ----- | ----- | ----- | ----- | ----- |
| flv                 | N     | Y     | N     | Y     | N     | N     |
| mp4                 | N     | Y     | Y     | Y     | Y     | N     |
| hls/ts/mkv          | Y     | Y     | Y     | Y     | Y     | N     |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>VideoMontage</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <VideoMontage>
            <Duration>10.5</Duration>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Fps>30</Fps>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
                <Remove>false</Remove>
            </Audio>
            <AudioMix>
                <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
                <MixMode>Once</MixMode>
                <Replace>true</Replace>
            </AudioMix>
        </VideoMontage>
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
| Tag                | Response.Template | Template tag: VideoMontage                                       | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| VideoMontage      | Response.Template | Template parameters                                                | Container |

<span id="VideoMontage"></span>
`VideoMontage` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description |
| :----------------- | :--------------------------------- | :-------------------------------- |
| Duration           | Response.TemplateList.VideoMontage | Same as the `Request.Duration` in the request body.     |
| TimeInterval       | Response.TemplateList.VideoMontage | Same as the `Request.TimeInterval` in the request body. |
| Container          | Response.TemplateList.VideoMontage | Same as the `Request.Container` in the request body.    |
| Video              | Response.TemplateList.VideoMontage | Same as the `Request.Video` in the request body.        |
| Audio              | Response.TemplateList.VideoMontage | Same as the `Request.Audio` in the request body.        |
| AudioMix           | Response.TemplateList.VideoMontage | Same as the `Request.AudioMix` in the request body.        |



#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).


## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>VideoMontage</Tag>
    <Name>TemplateName</Name>
    <Duration>10.5</Duration>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Fps>30</Fps>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
        <Remove>false</Remove>
    </Audio>
    <AudioMix>
        <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
        <MixMode>Once</MixMode>
        <Replace>true</Replace>
    </AudioMix>
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
        <Tag>VideoMontage</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <VideoMontage>
            <Duration>10.5</Duration>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Fps>30</Fps>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
                <Remove>false</Remove>
            </Audio>
            <AudioMix>
                <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
                <MixMode>Once</MixMode>
                <Replace>true</Replace>
            </AudioMix>
        </VideoMontage>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
