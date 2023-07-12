## Feature Description

This API is used to create a professional transcoding template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateTranscodeProTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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
    <Tag>TranscodePro</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mxf</Format>
    </Container>
    <Video>
        <Codec>xavc</Codec>
        <Profile>XAVC-HD_422_10bit</Profile>
        <Width>1920</Width>
        <Height>1080</Height>
        <Interlaced>true</Interlaced>
        <Fps>30000/1001</Fps>
        <Bitrate>50000</Bitrate>
    </Video>
    <Audio>
        <Codec>pcm_s24le</Codec>
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
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- | ---- |
| Tag                | Request | Template tag: TranscodePro                                | String    | Yes   | None |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| Container          | Request | Container format                                    | Container | Yes       | None                             |
| Video              | Request | Video information                                                 | Container | Yes   | None   |
| TimeInterval       | Request | Time interval                                    | Container | No       | None                             |
| Audio              | Request | Audio information                                    | Container | No       | If `Audio` is not passed in, the audio information will be deleted. |
| TransConfig        | Request | Transcoding configuration                                    | Container | No       | None                             |

<span id="Container"></span>
`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ---------------------------------------------------- | --------- | ---- |
| Format             | Request.Container | Container format. Valid values: `mxf`, `mov`, `mkv`. | String | Yes       |

Audio/Video formats supported by different container formats are as follows:

| Container                  | Audio Codecs  | Video Codecs          |
| -------------------------- | ------------- | --------------------- |
| mxf                        | pcm_s24le     | xavc                  |
| mov, mkv                   | aac, mp3      | apple_prores          |

<span id="Video"></span>
`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ---------------- | ------------- | -------------------- | ------ | ---- | ------------ |------ |
| Codec                      | Request.Video | Codec format            | String | Yes   |  None  | xavc, apple_prores                                           |
| Profile          | Request.Video | Video algorithm profile        | String | Yes   | None       | See the following table for valid values.  |
| Width            | Request.Video | Width                   | String | Yes   | None       | See the following table for valid values.  |
| Height           | Request.Video | Height                   | String | Yes   | None       | See the following table for valid values.  |
| Interlaced       | Request.Video | Field mode               | String | Yes   | None       | See the following table for valid values.  |
| Fps            | Request.Video | Frame rate                   | String | Yes   | None       | See the following table for valid values.  |
| Bitrate          | Request.Video | Bitrate of the video output file    | String | No   | None       | See the following table for valid values.  |
| Rotate              | Request.Video | Rotation angle           | String | No   | None        | 1. Value range: [0, 360)<br/>2. Unit: Degree |

<br>
Video Parameter Constraint Table:<br>
Note: '-' indicates empty. The valid values of bitrate correspond to the valid values of frame rate numerically.

If `Video.Codec` is `xavc`:

| Profile                          | Width  | Height | Interlaced| Fps | Bitrate (Kbps)    |
| -------------------------------- | ------ | ------ | --------- | --- | ---------- |
| XAVC-HD_intra_420_10bit_class50  | 1440   | 1080   | true | 1. 25<br>2. 30000/1001 |-|
| XAVC-HD_intra_420_10bit_class50  | 1440   | 1080   | false| 1. 25<br>2. 24000/1001<br>3. 30000/1001|-|
| XAVC-HD_intra_422_10bit_class100 | 1280   | 720    | false| 1. 50<br>2. 60000/1001 |-|
| XAVC-HD_intra_422_10bit_class100 | 1920   | 1080   | true | 1. 25<br>2. 30000/1001 |-|
| XAVC-HD_intra_422_10bit_class100 | 1920   | 1080   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |-|
| XAVC-HD_intra_422_10bit_class200 | 1920   | 1080   | true | 1. 25<br>2. 30000/1001 |-|
| XAVC-HD_intra_422_10bit_class200 | 1920   | 1080   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |-|
| XAVC-4K_intra_422_10bit_class100 | 2048   | 1080   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |-|
| XAVC-4K_intra_422_10bit_class300 | 3840   | 2160   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |-|
| XAVC-4K_intra_422_10bit_class300 | 4096   | 2160   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |-|
| XAVC-4K_intra_422_10bit_class480 | 3840   | 2160   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |-|
| XAVC-4K_intra_422_10bit_class480 | 4096   | 2160   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |-|
| XAVC-4K_intra_422_10bit          | 2048   | 1080   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |                                                            1. 93000<br>2. 185000<br>3. 89000<br>4. 111000<br>5. 222000  |
| XAVC-4K_intra_422_10bit          | 3840   | 2160   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |                                                            1. 250000 or 400000<br>2. 500000 or 800000<br>3. 240000 or 384000<br>4. 300000 or 480000<br>5. 600000 or 960000  |
| XAVC-4K_intra_422_10bit          | 4096   | 2160   | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 |                                                            1. 250000 or 400000<br>2. 500000 or 800000<br>3. 240000 or 384000<br>4. 300000 or 480000<br>5. 600000 or 960000  |
| XAVC-HD_422_10bit                | 1280   | 720   | false| 1. 50<br>2. 60000/1001 | 1. 50000<br>2. 50000|
| XAVC-HD_422_10bit                | 1920   | 1080  | true | 1. 25<br>2. 30000/1001 | 1. 25000, 35000, or 50000<br>2. 25000, 35000, or 50000 |
| XAVC-HD_422_10bit                | 1920   | 1080  | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | 1. 25000, 35000, or 50000<br>2. 35000 or 50000<br>3. 25000, 35000, or 50000<br>4. 25000, 35000, or 50000<br>5. 35000 or 50000 |
| XAVC-4K_422_10bit                | 3840   | 2160  | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | 1. 100000, 140000, or 200000<br>2. 140000 or 200000<br>3. 100000, 140000, or 200000<br>4. 100000, 140000, or 200000<br>5. 140000 or 200000 |
| XAVC-4K_420_8bit                 | 3840   | 2160  | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | 1. 188000<br>2. 300000<br>3. 188000<br>4. 188000<br>5. 300000|

If `Video.Codec` is `apple_prores`:

| Profile |
| ------ |
|1.ProRes_422_Proxy</br>2.ProRes_422_LT</br>3.ProRes_422</br>4.ProRes_422_HQ</br>5.ProRes_4444</br>6.ProRes_4444_XQ</br>7.ProRes_4444_alpha</br>8.ProRes_4444_XQ_alpha    |

| Width  | Height | Interlaced| Fps |Bitrate (Kbps)    |
| ------ | ------ | --------- | --- | --- |
| 720    | 486    | false| 1. 24000/1001<br>2. 30000/1001 | Value range: [2000,3000000]|
| 720    | 486    | true | 1. 60000/1001 | Value range: [2000,3000000]|
| 720    | 576    | false| 1. 25 | Value range: [2000,3000000]|
| 720    | 576    | true | 1. 50 | Value range: [2000,3000000]|
| 960    | 720    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|
| 1280    | 720    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|
| 1280    | 1080    | false| 1. 24000/1001<br>2. 30000/1001 | Value range: [2000,3000000]|
| 1280    | 1080    | true | 1. 60000/1001 | Value range: [2000,3000000]|
| 1440   | 1080   | false| 1. 24000/1001<br>2. 25<br>3. 30000/1001 | Value range: [2000,3000000]|
| 1440   | 1080   | true | 1. 50<br>2. 60000/1001 | Value range: [2000,3000000]|
| 1920    | 1080    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|
| 1920   | 1080   | true | 1. 50<br>2. 60000/1001 | Value range: [2000,3000000]|
| 2048    | 1080    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|
| 2048    | 1556    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|
| 3840    | 2160    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|
| 4096    | 2160    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|
| 5120    | 2700    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|
| 6144    | 3240    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|
| 8192    | 4320    | false| 1. 25<br>2. 50<br>3. 24000/1001<br>4. 30000/1001<br>5. 60000/1001 | Value range: [2000,3000000]|

<span id="TimeInterval"></span>
`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Request.TimeInterval | Start time | String    | No   | 0 | <ul  style="margin: 0;"><li>Value range: [0, video duration] </li><li>Unit: Second </li><li>The `float` format is supported, accurate to the millisecond.</li></ul> |
| Duration             | Request.TimeInterval | Duration | String    | No   | Original video duration | <ul  style="margin: 0;"><li>Value range: [0, video duration] </li><li>Unit: Second </li><li>The `float` format is supported, accurate to the millisecond.</li></ul> |

<span id="Audio"></span>
`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | ----------- | ------ | ---- | ------ | ----------------------------- |
| Codec              | Request.Audio | Codec format   | String | Yes   | None    | pcm_s24le, aac, mp3|
| Remove             | Request.Audio | Whether to delete the source audio stream | String | No   |   false    | Valid values: `true`, `false`.                                             |

<span id="TransConfig"></span>
`TransConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| --------------------- | ------------------- | ---------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| AdjDarMethod          | Request.TransConfig                        | Resolution adjustment method               | String    | No       | none   | <ul  style="margin: 0;"><li>Valid values: `scale`, `crop`, `pad`, `none`.</li><li>If the aspect ratio of the output video is different from that of the original video, the resolution is adjusted according to this parameter.</li></ul>  |
| IsCheckReso           | Request.TransConfig                        | Whether to check the resolution               | String    | No       | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul>      |
| ResoAdjMethod         | Request.TransConfig                        | Resolution adjustment method               | String    | No       | 0      | <ul  style="margin: 0;"><li>Valid values: `0`, `1`. `0` indicates to use the original video resolution, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckReso` is `true`.</li></ul> |
| IsCheckVideoBitrate   | Request.TransConfig | Whether to check the video bitrate | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul> |
| VideoBitrateAdjMethod | Request.TransConfig                        | Video bitrate adjustment method             | String    | No       | 0      | <ul  style="margin: 0;"><li>Valid values: `0`, `1`. When the output video has a higher bitrate than the input video, `0` indicates to use the original video bitrate, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckVideoBitrate` is `true`.</li></ul> |
| IsCheckAudioBitrate   | Request.TransConfig                        | Whether to check the audio bitrate | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul> |
| AudioBitrateAdjMethod | Request.TransConfig                        | Audio bitrate adjustment method | String | No   | 0      | <ul  style="margin: 0;"><li>Valid values: `0`, `1`. When the output audio has a higher bitrate than the input audio, `0` indicates to use the original audio bitrate, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckAudioBitrate` is `true`.</li></ul> |
| IsCheckVideoFps       | Request.TransConfig | Whether to check the video frame rate | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul> |
| VideoFpsAdjMethod     | Request.TransConfig | Video frame rate adjustment method             | String    | No       | 0      | <ul  style="margin: 0;"><li>Valid values: `0`, `1`. When the output video has a higher frame rate than the input video, `0` indicates to use the original video frame rate, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckVideoFps` is `true`.</li></ul> |
| DeleteMetadata        | Request.TransConfig                         | Whether to delete metadata from the file | String    | No       | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`. </li><li>If the value is `false`, the source file information is retained.</li></ul>|
| IsHdr2Sdr             | Request.TransConfig                        | Whether to enable HDR-to-SDR conversion             | String    | No       | false  | true/false                                                   |

The `AdjDarMethod` parameter is illustrated as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/e2eb1d7346df8f51756fdab7bdce2ca0.png)

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>TranscodePro</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <TransProTpl>
            <Container>
                <Format>mxf</Format>
            </Container>
            <Video>
                <Codec>xavc</Codec>
                <Profile>XAVC-HD_422_10bit</Profile>
                <Width>1920</Width>
                <Height>1080</Height>
                <Interlaced>true</Interlaced>
                <Fps>30000/1001</Fps>
                <Bitrate>50000</Bitrate>
            </Video>
            <Audio>
                <Codec>pcm_s24le</Codec>
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
        </TransProTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None     | Response container | Container |

<span id="Response"></span>
`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.Template     | Template ID                                                      | String    |
| Name               | Response.Template     | Template name                                                     | String    |
| BucketId           | Response.Template     | Template bucket                                                | String    |
| Category           | Response.Template     | Template category: Custom or Official                                | String    |
| Tag                | Response.Template | Template tag: TranscodePro                                       | String    |
| UpdateTime         | Response.Template     | Update time                                                     | String    |
| CreateTime         | Response.Template     | Creation time                                                     | String    |
| TransProTpl      | Response.Template | Template parameters                                                | Container |


`TransProTpl` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :-------------------------------------- | :-------- |
| TimeInterval       | Response.Template.TransProTpl | Same as `Request.TimeInterval` in the request body. | Container |
| Container          | Response.Template.TransProTpl | Same as `Request.Container` in the request body.    | Container |
| Video              | Response.Template.TransProTpl | Same as `Request.Video` in the request body.        | Container |
| Audio              | Response.Template.TransProTpl | Same as `Request.Audio` in the request body.        | Container |
| TransConfig        | Response.Template.TransProTpl | Same as `Request.TransConfig` in the request body.  | Container |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).


## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signatrue=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>TranscodePro</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mxf</Format>
    </Container>
    <Video>
        <Codec>xavc</Codec>
        <Profile>XAVC-HD_422_10bit</Profile>
        <Width>1920</Width>
        <Height>1080</Height>
        <Interlaced>true</Interlaced>
        <Fps>30000/1001</Fps>
        <Bitrate>50000</Bitrate>
    </Video>
    <Audio>
        <Codec>pcm_s24le</Codec>
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
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <Template>
        <Tag>TranscodePro</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <TransProTpl>
            <Container>
                <Format>mxf</Format>
            </Container>
            <Video>
                <Codec>xavc</Codec>
                <Profile>XAVC-HD_422_10bit</Profile>
                <Width>1920</Width>
                <Height>1080</Height>
                <Interlaced>true</Interlaced>
                <Fps>30000/1001</Fps>
                <Bitrate>50000</Bitrate>
            </Video>
            <Audio>
                <Codec>pcm_s24le</Codec>
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
        </TransProTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
