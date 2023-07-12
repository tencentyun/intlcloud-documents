## Feature Description

This API is used to create a video-to-animated image conversion template.

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
    <Tag>Animation</Tag>
    <Name>TemplateName</Name>
    <Container>
       <Format>gif</Format>
    </Container>
    <Video>
       <Codec>gif</Codec>
       <Width>1280</Width>
       <Height></Height>
       <Fps>15</Fps>
       <AnimateOnlyKeepKeyFrame>true</AnimateOnlyKeepKeyFrame>
    </Video>
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

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ------------------------------------------ | --------- | -------- |
| Tag                | Request | Template tag: Animation                                    | String    | Yes   |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       |
| Container          | Request | Container format                                               | Container | Yes   |
| Video              | Request | Video information                                               | Container | No   |
| TimeInterval       | Request | Time interval                                               | Container | No   |

<span id="Container"></span>
`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | ------ | -------- |
| Format                | Request.Container | Container format. Valid values: `gif`, `hgif` (higher-definition GIF), `webp` | String    | Yes   |

<span id="Video"></span>
`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------------------- | ------------- | ------------------------------------------------------------ | ------ | -------- | ----------------- | ------------------------------------------------------------ |
| Codec                      | Request.Video | Codec format            | String | Yes   |  None  | gif, webp                                          |
| Width                           | Request.Video | Width | String    | No   |  Original video width | <ul  style="margin: 0;"><li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Width` is set, `Height` is calculated based on the original video aspect ratio. </li></ul> |
| Height                          | Request.Video | Height | String    | No  | Original video height  | <ul  style="margin: 0;"><li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Height` is set, `Width` is calculated based on the original video aspect ratio.</li></ul> |
| Fps                        | Request.Video | Frame rate                  | String | No   | Original video frame rate | <ul  style="margin: 0;"><li>Value range: (0, 60]</li><li>Unit: fps</li><li>This parameter is optional. If it is not set, the video is played at the speed as per the original timestamp. This parameter specifies the frame rate for animated image playback.</li></ul> |
| AnimateOnly<br/>KeepKeyFrame    | Request.Video | Keeps only key frames for animated images. If `AnimateOnlyKeepKeyFrame` is set to `true`, `AnimateTimeIntervalOfFrame` and `AnimateFramesPerSecond` don't need to be set. If `AnimateOnlyKeepKeyFrame` is set to `false`, either `AnimateTimeIntervalOfFrame` or `AnimateFramesPerSecond` must be set.     | String | No   |      false        | <ul  style="margin: 0;"><li>Valid values: `true`, `false`.</li><li>This parameter specifies whether to keep only key frames for animated images </li> <li>Priority: AnimateFramesPerSecond > AnimateOnlyKeepKeyFrame > AnimateTimeIntervalOfFrame</li></ul> |
| AnimateTime<br/>IntervalOfFrame | Request.Video | Frame sampling interval for animated images      | String | No   |      None        | <ul  style="margin: 0;"><li>Value range: (0, video duration]</li><li>Frame sampling interval for animated images</li><li>The value of this parameter must be less than the value of `TimeInterval.Duration` if `TimeInterval.Duration` is set.</li></ul> |
| AnimateFrames<br/>PerSecond     | Request.Video | Number of frames sampled per second for animated images | String | No   |     None         | <ul  style="margin: 0;"><li>Value range: (0, video frame rate)</li><li>Frame sampling frequency for animated images</li><li>Priority: AnimateFramesPerSecond > AnimateOnlyKeepKeyFrame > AnimateTimeIntervalOfFrame</li></ul> |
| Quality                    | Request.Video | Relative quality          | String | No   |     None         | <ul  style="margin: 0;"><li>Value range: [1, 100)</li><li>This parameter will take effect for WEBP images and is not available for GIF images.</li></ul> |

<span id="TimeInterval"></span>
`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | -------------------- | -------- | ------ | -------- | -------- | ------------------------------------------------------------ |
| Start                | Request.TimeInterval | Start time | String    | No   | 0 | <ul  style="margin: 0;"><li>Value range: [0, video duration] </li> <li>Unit: Second </li> <li>The `float` format is supported, accurate to the millisecond.</li></ul> |
| Duration             | Request.TimeInterval | Duration | String    | No   | Video duration | <ul  style="margin: 0;"><li>Value range: [0, video duration] </li><li>Unit: Second </li> <li>The `float` format is supported, accurate to the millisecond.</li></ul> |


## Response

#### Response headers

This response contains common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Name>TemplateName</Name>
        <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
        <Tag>Animation</Tag>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <TransTpl>
            <Container>
                <Format>gif</Format>
            </Container>
            <Video>
                <Codec>gif</Codec>
                <Width>1280</Width>
                <Height></Height>
                <Fps>15</Fps>
                <AnimateOnlyKeepKeyFrame>true</AnimateOnlyKeepKeyFrame>
            </Video>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </TransTpl>
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
| :----------------- | :------- | :----------------------------- | :-------- |
| TemplateId         | Response | Template ID                                                      | String    |
| Name               | Response | Template name                                                     | String    |
| BucketId           | Response | Template bucket                                                | String    |
| Category           | Response | Template category: `Custom` or `Official`.                                | String    |
| Tag                | Response | Template tag                      | String    |
| UpdateTime         | Response | Update time                                                     | String    |
| CreateTime         | Response | Creation time                                                     | String    |
| TransTpl           | Response | Template parameters                 | Container |


`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | --------------------------- | ------------------------------------------------------------ | ------ |
| Format                | Response.TransTpl.Container | Container format: `gif`, `hgif` (higher-definition GIF), `webp`. | String    |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------------------- | ---------------------------- | ---------------------- | ------ |
| Codec                           | Response.<br/>TransTpl.Video | Codec             | String |
| Width                           | Response.<br/>TransTpl.Video | Width                    | String |
| Height                          | Response.<br/>TransTpl.Video | Height                    | String |
| Fps                             | Response.<br/>TransTpl.Video | Frame rate                  | String |
| AnimateOnly<br/>KeepKeyFrame    | Response.<br/>TransTpl.Video | Keeps only keyframes for animated images       | String |
| AnimateTime<br/>IntervalOfFrame | Response.<br/>TransTpl.Video | Frame sampling interval for animated images       | String |
| AnimateFrames<br/>PerSecond     | Response.<br/>TransTpl.Video | Number of frames sampled per second for animated images | String |
| Quality                         | Response.<br/>TransTpl.Video | Relative quality           | String |


`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------------ | -------- | ------ |
| Start              | Response.TransTpl.TimeInterval | Start time | String |
| Duration           | Response.TransTpl.TimeInterval | Duration | String |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>Animation</Tag>
    <Name>TemplateName</Name>
    <Container>
       <Format>gif</Format>
    </Container>
    <Video>
       <Codec>gif</Codec>
       <Width>1280</Width>
       <Height></Height>
       <Fps>15</Fps>
       <AnimateOnlyKeepKeyFrame>true</AnimateOnlyKeepKeyFrame>
    </Video>
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYz****=

<Response>
    <Template>
        <Name>TemplateName</Name>
        <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
        <Tag>Animation</Tag>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <TransTpl>
            <Container>
                <Format>gif</Format>
            </Container>
            <Video>
                <Codec>gif</Codec>
                <Width>1280</Width>
                <Height></Height>
                <Fps>15</Fps>
                <AnimateOnlyKeepKeyFrame>true</AnimateOnlyKeepKeyFrame>
            </Video>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```