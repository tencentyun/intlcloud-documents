## Feature Description

This API (`CreateMediaTemplate`) is used to create a splicing template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateConcatTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 

#### Request headers

#### Common request headers

This API uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Non-common request headers

This request operation does not use any non-common request headers.

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>Concat</Tag>
    <Name>TemplateName</Name>
    <ConcatTemplate>
        <ConcatFragment>
            <Mode>Start</Mode>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
        </ConcatFragment>
        <ConcatFragment>
            <Mode>End</Mode>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/end.mp4</Url>
        </ConcatFragment>
        <Audio>
            <Codec>mp3</Codec>
            <Samplerate></Samplerate>
            <Bitrate></Bitrate>
            <Channels></Channels>
        </Audio>
        <Video>
            <Codec>H.264</Codec>
            <Bitrate>1000</Bitrate>
            <Width>1280</Width>
            <Height></Height>
            <Fps>30</Fps>
        </Video>
        <Container>
            <Format>mp4</Format>
        </Container>
        <AudioMix>
            <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
            <MixMode>Once</MixMode>
            <Replace>true</Replace>
            <EffectConfig>
                <EnableStartFadein>true</EnableStartFadein>
                <StartFadeinTime>3</StartFadeinTime>
                <EnableEndFadeout>false</EnableEndFadeout>
                <EndFadeoutTime>0</EndFadeoutTime>
                <EnableBgmFade>true</EnableBgmFade>
                <BgmFadeTime>1.7</BgmFadeTime>
            </EffectConfig>
        </AudioMix>
    </ConcatTemplate>
</Request>
```

The nodes are described as follows:

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | --------------------------------------- | --------- | ---- |
| Tag                | Request | Template type: Concat                                   | String    | Yes   |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (*).                    | String    | Yes   |
| ConcatTemplate     | Request | Splicing template                                                | Container | Yes   |


`ConcatTemplate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ---------------------- | -------- | --------- | ---- | ---------- | ------------------------------------------------------------ |
| ConcatFragment      | Request.ConcatTemplate | Splicing node    | Container array   | Yes   | None  | None |
| Audio               | Request.ConcatTemplate | Audio parameter    | Container    | No   | Original media value  | If the target file does not require audio information, set `Audio.Remove` to `true`. |
| Video               | Request.ConcatTemplate | Video parameter    | Container    | No   | Original media value  | If the target file does not require video information, set `Video.Remove` to `true`. |
| Container           | Request.ConcatTemplate | Container format     | Container    | Yes   | None  | None |
| AudioMix           | Request.ConcatTemplate | Audio mix parameter    | Container | No   | This parameter takes effect only if `Audio.Remove` is `false`. | None |
| DirectConcat       | Request.ConcatTemplate | Whether to splice without transcoding | String    | No   | false         | true/ false |


`ConcatFragment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------------------------------------ | ------------ | ------ | ---- | ------ | ---------------------------------- |
| Url                | Request.ConcatTemplate.<br/>ConcatFragment | Splicing object address   | String    | Yes   | None   | Same as the address of the bucket object file. |
| Mode                | Request.ConcatTemplate.<br/>ConcatFragment | Node type      | String    | Yes   | None   | <li>Start </br><li>End |


`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | --------------------------------- | ---------- | ------ | ---- | -------------- | ------------------------------------------------------------ |
| Codec              | Request.ConcatTemplate.<br/>Audio | Codec format     | String | Yes   | Original codec of the file    | Valid values: aac, mp3                                                |
| Samplerate         | Request.ConcatTemplate.<br/>Audio | Sample rate         | String | No   | Original sample rate of the file  | <li>Unit: Hz<br/><li>Valid values: 11025, 22050, 32000, 44100, 48000, 96000<br/><li>Different container formats support different MP3 sample rates, as shown in the table below.|
| Bitrate            | Request.ConcatTemplate.<br/>Audio | Audio bitrate   | String | No   | Original audio bitrate of the file   | <li>Unit: Kbps<br/><li>Value range: [8, 1000]                       |
| Channels           | Request.ConcatTemplate.<br/>Audio | Number of sound channels         | String | No   | Original number of sound channels of the file      | <li>If `Codec` is `aac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.<br/><li>If `Codec` is `mp3`, the value can be `1` or `2`. |

Y indicates supported, and N indicates unsupported.

| Container Format/Audio Sample Rate | 11025 | 22050 | 32000 | 44100 | 48000 | 96000 |
| ------------------- | ----- | ----- | ----- | ----- | ----- | ----- |
| mp3                 | Y     | Y     | Y     | Y     | Y     | N     |

`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------------------- | ------------------------------------- | ------ | ---- |
| Format                | Request.ConcatTemplate.<br/>Container | Container format: mp4, flv, hls, ts, mp3, aac   | String    | Yes   |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | --------------------------------- | ------------------ | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Request.ConcatTemplate.<br/>Video | Codec format             | String | Yes   |   H.264 | H.264                                          |
| Width              | Request.ConcatTemplate.<br/>Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Width` is set, `Height` is calculated according to the original video aspect ratio. |
| Height             | Request.ConcatTemplate.<br/>Video | Height                    | String | No   | Original video height | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Height` is set, `Width` is calculated according to the original video aspect ratio. |
| Fps                | Request.ConcatTemplate.<br/>Video | Frame rate                  | String | No   | Original video frame rate | <li>Value range: (0, 60]<br><li>Unit: fps |
| Bitrate            | Request.ConcatTemplate.<br/>Video | Bitrate of the video output file      | String | No   |  Original video bitrate           | <li>Value range: [10, 50000]<br/><li>Unit: Kbps    </li>          |
| Crf                | Request.ConcatTemplate.<br/>Video | Bitrate, which is a quality control factor  | String | No       | Original video bitrate           | <li>Value range: (0, 51]</li><li> If `Crf` is set, the setting of `Bitrate` becomes invalid. </li><li> If `Bitrate` is empty, `25` is used for this parameter by default.</li>          |
| Remove             | Request.ConcatTemplate.<br/>Video | Whether to delete the video stream     | String | No       | false        |  Valid values: true, false                                               |
| Rotate              | Request.Video | Rotation angle           | String | No   | None        | 1. Value range: [0, 360)<br/>2. Unit: degree |

`AudioMix` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ----------------- | ------------------------------ | ------------ | ------ | ---- | ------ | ---------------------------- |
| AudioSource       | Request.ConcatTemplate.AudioMix | Address of the audio track file to be mixed | String | Yes | None | It must be stored in the same bucket as the input media file. |
| MixMode           | Request.ConcatTemplate.AudioMix | Audio mix mode  | String | No   | Repeat| <li>Repeat: Repeats the background sound <br/><li>Once: Plays back the background sound once |
| Replace           | Request.ConcatTemplate.AudioMix | Whether to replace the original audio of the input media file with the mixed audio track | String | No | false | true/false |
| EffectConfig      | Request.ConcatTemplate.AudioMix | Audio mix transition configuration  | Container | No   | false  | None |

`EffectConfig ` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ----------------- | ------------------------------ | ------------ | ------ | ---- | ------ | ---------------------------- |
| EnableStartFadein | Request.ConcatTemplate.AudioMix.EffectConfig | Enables fade-in  | String | No   | false       | true/false |
| StartFadeinTime   | Request.ConcatTemplate.AudioMix.EffectConfig | Fade-in duration  | String | No   | None    | A floating point number above 0 |
| EnableEndFadeout  | Request.ConcatTemplate.AudioMix.EffectConfig | Enables fade-out  | String | No   | false       | true/false |
| EndFadeoutTime    | Request.ConcatTemplate.AudioMix.EffectConfig | Fade-out duration  | String | No   | None    | A floating point number above 0 |
| EnableBgmFade     | Request.ConcatTemplate.AudioMix.EffectConfig | Enables fade-in for background music transition  | String | No   | false       | true/false |
| BgmFadeTime       | Request.ConcatTemplate.AudioMix.EffectConfig | Fade-in duration for background music transition  | String | No   | None    | A floating point number above 0 |

## Response

#### Response headers

#### Common response headers

This response contains common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Non-common response headers

This response does not use any non-common response header.

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Tag>Concat</Tag>
        <Name>TemplateName</Name>
        <ConcatTemplate>
            <ConcatFragment>
                <Mode>Start</Mode>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
            </ConcatFragment>
            <ConcatFragment>
                <Mode>End</Mode>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/end.mp4</Url>
            </ConcatFragment>
            <Audio>
                <Codec>mp3</Codec>
                <Samplerate></Samplerate>
                <Bitrate></Bitrate>
                <Channels></Channels>
            </Audio>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
            </Video>
            <Container>
                <Format>mp4</Format>
            </Container>
            <AudioMix>
                <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
                <MixMode>Once</MixMode>
                <Replace>true</Replace>
                <EffectConfig>
                    <EnableStartFadein>true</EnableStartFadein>
                    <StartFadeinTime>3</StartFadeinTime>
                    <EnableEndFadeout>false</EnableEndFadeout>
                    <EndFadeoutTime>0</EndFadeoutTime>
                    <EnableBgmFade>true</EnableBgmFade>
                    <BgmFadeTime>1.7</BgmFadeTime>
                </EffectConfig>
            </AudioMix>
        </ConcatTemplate>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None     | Response container | Container |


`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------- | :-------- |
| TemplateId         | Response.Template | Template ID                        | String    |
| Name               | Response.Template | Template name                       | String    |
| BucketId           | Response.Template | Template bucket                 | String    |
| Category           | Response.Template | Template category: Custom or Official | String    |
| Tag                | Response.Template | Template type: Concat                                             | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| ConcatTemplate     | Response.Template | Same as `Request.ConcatTemplate` in the request body.                           | Container |



#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml



<Request>
   <Tag>Concat</Tag>
   <Name>TemplateName</Name>
   <ConcatTemplate>
        <ConcatFragment>
            <Mode>Start</Mode>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
        </ConcatFragment>
        <ConcatFragment>
            <Mode>End</Mode>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/end.mp4</Url>
        </ConcatFragment>
        <Audio>
            <Codec>mp3</Codec>
            <Samplerate></Samplerate>
            <Bitrate></Bitrate>
            <Channels></Channels>
        </Audio>
        <Video>
            <Codec>H.264</Codec>
            <Bitrate>1000</Bitrate>
            <Width>1280</Width>
            <Height></Height>
            <Fps>30</Fps>
        </Video>
        <Container>
            <Format>mp4</Format>
        </Container>
        <AudioMix>
            <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
            <MixMode>Once</MixMode>
            <Replace>true</Replace>
            <EffectConfig>
                <EnableStartFadein>true</EnableStartFadein>
                <StartFadeinTime>3</StartFadeinTime>
                <EnableEndFadeout>false</EnableEndFadeout>
                <EndFadeoutTime>0</EndFadeoutTime>
                <EnableBgmFade>true</EnableBgmFade>
                <BgmFadeTime>1.7</BgmFadeTime>
            </EffectConfig>
        </AudioMix>
   </ConcatTemplate>
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Tag>Concat</Tag>
        <Name>TemplateName</Name>
        <ConcatTemplate>
            <ConcatFragment>
                <Mode>Start</Mode>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
            </ConcatFragment>
            <ConcatFragment>
                <Mode>End</Mode>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/end.mp4</Url>
            </ConcatFragment>
            <Audio>
                <Codec>mp3</Codec>
                <Samplerate></Samplerate>
                <Bitrate></Bitrate>
                <Channels></Channels>
            </Audio>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
            </Video>
            <Container>
                <Format>mp4</Format>
            </Container>
            <AudioMix>
                <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
                <MixMode>Once</MixMode>
                <Replace>true</Replace>
                <EffectConfig>
                    <EnableStartFadein>true</EnableStartFadein>
                    <StartFadeinTime>3</StartFadeinTime>
                    <EnableEndFadeout>false</EnableEndFadeout>
                    <EndFadeoutTime>0</EndFadeoutTime>
                    <EnableBgmFade>true</EnableBgmFade>
                    <BgmFadeTime>1.7</BgmFadeTime>
                </EffectConfig>
            </AudioMix>
        </ConcatTemplate>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
