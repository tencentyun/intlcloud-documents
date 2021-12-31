## Feature Description
This API (`CreateMediaTemplate`) is used to create an animated image template.

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
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None | Request container | Container | Yes   |


`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Task type: Animation                                    | String    | Yes   |
| Name               | Request | Template name. The value can contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (\*).                    | String    | Yes   |
| Container          | Request | Container format                                               | Container | Yes   |
| Video              | Request | Video information                                               | Container | No   |
| TimeInterval       | Request | Time interval                                               | Container | No   |


`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Format                | Request.Container | Container format: gif, hgif, webp (hgif indicates higher-definition gif.) | String    | Yes   |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Request.Video | Codec format            | String | Yes   |  None  | gif, webp                                          |
| Width                      | Request.Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Width` is set, `Height` is calculated according to the original video proportion.</li> |
| Height                     | Request.Video | Height                    | String | No   | Original video height | <li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Height` is set, `Width` is calculated according to the original video proportion.</li> |
| Fps                        | Request.Video | Frame rate                  | String | No   | Original video frame rate | <li>Value range: (0, 60]</li><li>Unit: fps</li><li>This parameter is optional. If it is not set, the video is played at the speed as per the original timestamp. This parameter specifies the frame rate for animated image playback.</li> |
| AnimateOnly<br/>KeepKeyFrame    | Request.Video | Keep only key frames for animated images. If `AnimateOnlyKeepKeyFrame` is `true`, `AnimateTimeIntervalOfFrame` and `AnimateFramesPerSecond` do not need to be set. If `AnimateOnlyKeepKeyFrame` is false`, either `AnimateTimeIntervalOfFrame` or `AnimateFramesPerSecond` must be set.     | String | No   |      false        | <li>true, false</li><li>Parameter specifying whether to keep only key frames for animated images </li> <li>Priority: AnimateFramesPerSecond > AnimateOnlyKeepKeyFrame > AnimateTimeIntervalOfFrame</li>               |
| AnimateTime<br/>IntervalOfFrame | Request.Video | Frame sampling interval for animated images      | String | No   |      None        | <li>(0, Video duration]</li><li>Frame sampling interval for animated images</li><li>The value of this parameter must be less than the value of `TimeInterval.Duration` if `TimeInterval.Duration` is set.</li> |
| AnimateFrames<br/>PerSecond     | Request.Video | Number of frames sampled per second for animated images | String | No   |     None         | <li>(0, Video frame rate)</li><li>Frame sampling frequency for animated images</li><li>Priority: AnimateFramesPerSecond > AnimateOnlyKeepKeyFrame > AnimateTimeIntervalOfFrame</li> |
| Quality                    | Request.Video | Relative quality          | String | No   |     None         | <li>[1, 100)</li><li>This parameter is valid for WEBP images and is not available for GIF images.</li> |


`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Request.TimeInterval | Start time | String    | No   | 0 |<li> [0, Video duration] </li> <li>Unit: second </li> <li>Supports the float format, accurate to milliseconds.</li> |
| Duration             | Request.TimeInterval | Duration | String    | No   | Video duration | <li> [0, Video duration] </li><li>Unit: second </li> <li>Supports the float format, accurate to milliseconds.</li> |


## Response

#### Response headers

This response contains [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Name>TemplateName</Name>
        <TemplateId></TemplateId>
        <Tag>Animation</Tag>
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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response | Template ID                                                      | String    |
| Name               | Response | Template name                                                     | String    |
| BucketId           | Response | Template bucket                                                | String    |
| Category           | Response | Template category: Custom or Official                                | String    |
| Tag                | Response | Task type: Animation                                           | String    |
| UpdateTime         | Response | Update time                                                     | String    |
| CreateTime         | Response | Creation time                                                     | String    |
| TransTpl           | Response | Template parameters                                                | Container |


`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Format                | Response.TransTpl.Container | Container format: gif, hgif, webp (hgif indicates higher-definition gif.) | String    | Yes   |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Response.<br/>TransTpl.Video | Codec format            | String | Yes   |  None  |  gif, webp                                          |
| Width                      | Response.<br/>TransTpl.Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Width` is set, `Height` is calculated according to the original video proportion.</li> |
| Height                     | Response.<br/>TransTpl.Video | Height                    | String | No   | Original video height | <li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Height` is set, `Width` is calculated according to the original video proportion. </li>|
| Fps                        | Response.<br/>TransTpl.Video | Frame rate                  | String | No   | Original video frame rate | <li>Value range: (0, 60]</li><li>Unit: fps</li><li>If the frame rate is greater than 60, set this parameter to `60`.<br/>This parameter is optional. If it is not set, the video is played at the speed as per the original timestamp. This parameter specifies the frame rate for animated image playback.</li> |
| AnimateOnly<br/>KeepKeyFrame    | Response.<br/>TransTpl.Video | Keep only key frames for animated images      | String | No   |      false        | <li>true, false<br/><li>Parameter specifying whether to keep only key frames for animated images                     |
| AnimateTime<br/>IntervalOfFrame | Response.<br/>TransTpl.Video | Frame sampling interval for animated images      | String | No   |      None        | <li>(0, Video duration]</li><li>Frame sampling interval for animated images</li><li> The value of this parameter must be less than the value of `TimeInterval.Duration` if `TimeInterval.Duration` is set. </li>|
| AnimateFrames<br/>PerSecond     | Response.<br/>TransTpl.Video | Number of frames sampled per second for animated images | String | No   |     None         | <li>(0, Video frame rate)</li><li>Frame sampling frequency for animated images</li><li> Priority: AnimateFramesPerSecond > AnimateOnlyKeepKeyFrame > AnimateTimeIntervalOfFrame </li>|
| Quality                    | Response.<br/>TransTpl.Video | Relative quality          | String | No   |     None         | <li>[1, 100)</li><li>This parameter is valid for WEBP images and is not available for GIF images.</li> |


`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Response.TransTpl.TimeInterval | Start time | String    | No   | 0 | <li> [0, Video duration]</li> <li>Unit: second</li><li>Supports the float format, accurate to milliseconds.</li> |
| Duration             | Response.TransTpl.TimeInterval | Duration | String    | No   | Video duration | <li>[0, Video duration] </li><li>Unit: second </li><li>Supports the float format, accurate to milliseconds.</li> |


#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

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
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYz****=



<Response>
    <Template>
        <Name>TemplateName</Name>
        <TemplateId></TemplateId>
        <Tag>Animation</Tag>
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
