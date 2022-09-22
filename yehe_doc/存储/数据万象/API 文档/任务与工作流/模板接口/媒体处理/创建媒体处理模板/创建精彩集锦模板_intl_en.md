## Feature Description
This API (`CreateMediaTemplate`) is used to create a video montage template.

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

>? Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
    <Tag>VideoMontage</Tag>
    <Name>TemplateName</Name>
    <Duration></Duration>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Height></Height>
        <Fps>30</Fps>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
        <Remove>false</Remove>
    </Audio>
</Request>

```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None | Request container | Container | Yes   |


`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- | ---- |
| Tag                | Request | Task type: VideoMontage                                    | String    | Yes   | None |
| Name               | Request | Template name. The value can contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| Duration           | Request | Video montage duration                                                 | String    | No   | 1. The default value is the automatic analysis duration.</br>2. Unit: second</br>3. Supports the float format, accurate to milliseconds.|
| Container          | Request | Container format                                                 | Container | Yes   | None   |
| Video              | Request | Video information                                                 | Container | Yes   | None   |
| Audio              | Request | Audio information                                                 | Container | No   | None   |


`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| -----------------| ------- | ----------------------------------------------------    | --------- | ---- |
| Format           | Request.Container | Container format: mp4, flv, hls, ts, mkv             | String    | Yes   |

Audio/Video formats supported by different container formats are as follows:

| Container                  | Audio Codecs  | Video Codecs          |
| -------------------------- | ------------- | --------------------- | 
| MP4/TS/HLS/MKV                    | AAC, MP3      | H.264, H.265          |
| FLV                        | AAC, MP3      | H.264                 |


`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Request.Video | Codec format            | String | No   | H.264        |  1. H.264<br/> 2.H.265  |
| Width              | Request.Video | Width                 | String | No       | Original video width | 1. Value range: [128, 4096]<br/>2. Unit: px<br/>3. If only `Width` is set, `Height` is calculated according to the original video proportion.<br/>4. The value must be an even number. |
| Height             | Request.Video | Height                 | String | No       | Original video height | 1. Value range: [128, 4096]<br/>2. Unit: px<br/>3. If only `Height` is set, `Width` is calculated according to the original video proportion.<br/>4. The value must be an even number. |
| Fps                        | Request.Video | Frame rate                  | String | No   | None           | 1. Value range: (0, 60]<br>2. Unit: fps |
| Bitrate                    | Request.Video | Bitrate of the video output file    | String | No   |  None          | 1. Value range: [10, 50000]<br/>2. Unit: Kbps |
| Crf                | Request.Video | Bit rate, which is a quality control factor  | String | No       | None           | 1. Value range: (0, 51]<br/>2. If `Crf` is set, the setting of `Bitrate` becomes invalid. <br/>3. If `Bitrate` is empty, `25` is used for this parameter by default. |

`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | -------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| Codec              | Request.Audio | Codec format     | String | No   | aac    | Valid values: aac, mp3                                                |
| Samplerate         | Request.Audio | Sample rate         | String | No   | 44100  | 1. Unit: Hz<br/>2. Valid values: 11025, 22050, 32000, 44100, 48000, 96000<br/>3. Different container formats support different MP3 sample rates, as shown in the table below.|
| Bitrate            | Request.Audio | Original audio bitrate   | String | No   | None     | 1. Unit: Kbps<br/>2. Value range: [8, 1000]|
| Channels           | Request.Audio | Number of sound channels         | String | No   | None     | 1. If `Codec` is `aac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`. <br/>2. If `Codec` is `mp3`, the value can be `1` or `2`. |
| Remove             | Request.Audio | Whether to delete the audio stream | String | No   |   false    | Valid values: true, false                                             |

>? Y indicates supported, and N indicates unsupported.
>

| Container Format/Audio Sample Rate | 11025  | 22050|  32000 | 44100|  48000|   96000 |
| ------------------ | ------- | ------- | ------- | ------- |------------| ------------- |
| FLV             | Y       | Y| N| Y| N| N|
| MP4                | N       | Y| Y| Y| Y| N|
| HLS/TS/MKV         | Y       | Y| Y| Y| Y| N|


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>VideoMontage</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <VideoMontage>
            <Duration></Duration>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
                <Remove>false</Remove>
            </Audio>
        </VideoMontage>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None | Response container | Container |


`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.Template     | Template ID                                                      | String    |
| Name               | Response.Template     | Template name                                                     | String    |
| BucketId           | Response.Template     | Template bucket                                                | String    |
| Category           | Response.Template     | Template category: Custom or Official                                | String    |
| Tag                | Response.Template | Task type: VideoMontage                                          | String    |
| UpdateTime         | Response.Template     | Update time                                                     | String    |
| CreateTime         | Response.Template     | Creation time                                                     | String    |
| VideoMontage           | Response.Template | Template parameters                                                | Container |


`VideoMontage` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | 
| :----------------- | :----------------------------- | :------------------------------- |
| Duration           | Response.TemplateList.VideoMontage | Same as `Request.Duration` in the request body.     | 
| TimeInterval       | Response.TemplateList.VideoMontage | Same as `Request.TimeInterval` in the request body. |
| Container          | Response.TemplateList.VideoMontage | Same as `Request.Container` in the request body.    |
| Video              | Response.TemplateList.VideoMontage | Same as `Request.Video` in the request body.        |
| Audio              | Response.TemplateList.VideoMontage | Same as `Request.Audio` in the request body.        |


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
    <Tag>VideoMontage</Tag>
    <Name>TemplateName</Name>
    <Duration></Duration>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Height></Height>
        <Fps>30</Fps>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
        <Remove>false</Remove>
    </Audio>
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
        <Tag>VideoMontage</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <VideoMontage>
            <Duration></Duration>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
                <Remove>false</Remove>
            </Audio>
        </VideoMontage>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
