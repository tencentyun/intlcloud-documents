## Feature Description
This API (`UpdateMediaTemplate`) is used to update an animated image template.

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
    <Tag>Animation</Tag>
    <Name>TemplateName</Name>
    <TemplateId></TemplateId>
    <Container>
        <Format>gif</Format>
    </Container>
    <Video>
        <Codec>gif</Codec>
        <Width>1280</Width>
        <Height></Height>
        <Fps>15</Fps>
        <AnimateOnlyKeepKeyFrame>false</AnimateOnlyKeepKeyFrame>
    </Video>
    <TimeInterval>
        <Start>0</Start>
        <Duration>60</Duration>
    </TimeInterval>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :---------------------------------------- | :-------- | ---- |
| Request            | None | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Task type: Animation                                    | String    | Yes   |
| Name               | Request | Template name. The value can contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (*).                    | String    | Yes   |
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
| Width                      | Request.Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Width` is set, `Height` is calculated according to the original video proportion. |
| Height                     | Request.Video | Height                    | String | No   | Original video height | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Height` is set, `Width` is calculated according to the original video proportion. |
| Fps                        | Request.Video | Frame rate                  | String | No   | Original video frame rate | <li>Value range: (0, 60]<br/><li>Unit: fps<br/><li>If the frame rate is greater than 60, set this parameter to `60`.<br/>This parameter is optional. If it is not set, the video is played at the speed as per the original timestamp. This parameter specifies the frame rate for animated image playback. |
| AnimateOnly<br/>KeepKeyFrame    | Request.Video | Keep only key frames for animated images      | String | No   |      false        | <li>true, false<br/><li>Parameter specifying whether to keep only key frames for animated images                     |
| AnimateTime<br/>IntervalOfFrame | Request.Video | Frame sampling interval for animated images      | String | No   |      None        | <li>(0, Video duration]<br/><li>Frame sampling interval for animated images<br/><li>The value of this parameter must be less than the value of `TimeInterval.Duration` if `TimeInterval.Duration` is set. |
| AnimateFrames<br/>PerSecond     | Request.Video | Number of frames sampled per second for animated images | String | No   |     None         | <li>(0, Video frame rate)<br/><li>Frame sampling frequency for animated images<br/><li>Priority: AnimateFramesPerSecond > AnimateOnlyKeepKeyFrame > AnimateTimeIntervalOfFrame |
| Quality                    | Request.Video | Relative quality          | String | No   |     None         | <li> [1, 100)<br/><li>This parameter is valid for WEBP images and is not available for GIF images. |


`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Request.TimeInterval | Start time | String    | No   | 0 | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds. |
| Duration             | Request.TimeInterval | Duration | String    | No   | Video duration | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds. |



## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell

<Response>
    <Template>
        <Tag>Animation</Tag>
        <Name>TemplateName</Name>
        <TemplateId></TemplateId>
        <TransTpl>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>gif</Codec>
                <Width>1280</Width>
                <Height></Height>
                <Fps>15</Fps>
                <AnimateOnlyKeepKeyFrame>false</AnimateOnlyKeepKeyFrame>
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
| :----------------- | :----- | :----------------------------------------- | :-------- |
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
| Codec                      | Response.<br/>TransTpl.Video | Codec format            | String | Yes   |  None  | gif, webp                                          |
| Width                      | Response.<br/>TransTpl.Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Width` is set, `Height` is calculated according to the original video proportion. |
| Height                     | Response.<br/>TransTpl.Video | Height                    | String | No   | Original video height | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Height` is set, `Width` is calculated according to the original video proportion. |
| Fps                        | Response.<br/>TransTpl.Video | Frame rate                  | String | No   | Original video frame rate | <li>Value range: (0, 60]<br/><li>Unit: fps<br/><li>If the frame rate is greater than 60, set this parameter to `60`.<br/>This parameter is optional. If it is not set, the video is played at the speed as per the original timestamp. This parameter specifies the frame rate for animated image playback. |
| AnimateOnly<br/>KeepKeyFrame    | Response.<br/>TransTpl.Video | Keep only key frames for animated images      | String | No   |      false        | <li>true, false<br/><li>Parameter specifying whether to keep only key frames for animated images                     |
| AnimateTime<br/>IntervalOfFrame | Response.<br/>TransTpl.Video | Frame sampling interval for animated images      | String | No   |      None        | <li>(0, Video duration]<br/><li>Frame sampling interval for animated images<br/><li>The value of this parameter must be less than the value of `TimeInterval.Duration` if `TimeInterval.Duration` is set. |
| AnimateFrames<br/>PerSecond     | Response.<br/>TransTpl.Video | Number of frames sampled per second for animated images | String | No   |     None         | <li>(0, Video frame rate)<br/><li>Frame sampling frequency for animated images<br/><li>Priority: AnimateFramesPerSecond > AnimateOnlyKeepKeyFrame  > AnimateTimeIntervalOfFrame |
| Quality                    | Response.TransTpl.Video | Relative quality          | String | No   |     None         | <li>[1, 100)<br/><li>This parameter is valid for WEBP images and is not available for GIF images. |


`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Response.TransTpl.TimeInterval | Start time | String    | No   | 0 | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds. |
| Duration             | Response.TransTpl.TimeInterval | Duration | String    | No   | Video duration | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds. |



#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

#### Request

```shell
PUT /template/<TemplateId> HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml



<Request>
    <Tag>Animation</Tag>
    <Name>TemplateName</Name>
    <TemplateId></TemplateId>
    <Container>
        <Format>gif</Format>
    </Container>
    <Video>
        <Codec>gif</Codec>
        <Width>1280</Width>
        <Height></Height>
        <Fps>15</Fps>
        <AnimateOnlyKeepKeyFrame>false</AnimateOnlyKeepKeyFrame>
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
    <Tag>Animation</Tag>
    <Name>TemplateName</Name>
    <TemplateId></TemplateId>
    <TransTpl>
      <Container>
         <Format>mp4</Format>
      </Container>
      <Video>
        <Codec>gif</Codec>
        <Width>1280</Width>
        <Height></Height>
        <Fps>15</Fps>
        <AnimateOnlyKeepKeyFrame>false</AnimateOnlyKeepKeyFrame>
      </Video>
      <TimeInterval>
         <Start>0</Start>
         <Duration>60</Duration>
      </TimeInterval>
   </TransTpl>
   <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
   <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
</Response>
```
