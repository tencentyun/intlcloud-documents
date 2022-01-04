## Feature Description
This API (`DescribeMediaTemplates`) is used to search for animated image templates.

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
| tag           | None        | Task type: Animation       | String    |Yes|
| category      | None   | Template category: Custom (default) or Official | String  |No|
| ids           | None        | Template ID. If you enter multiple IDs, separate them with commas (,).  | String     |No|
| name          | None        | Template name prefix              | String     |No|
| pageNumber    | None        | Page number                   | Integer     |No|
| pageSize      | None        | Records per page                 | Integer     |No|

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
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
| Tag                | Response.TemplateList | Task type: Animation                                           | String    |
| UpdateTime         | Response.TemplateList | Update time                                                     | String    |
| CreateTime         | Response.TemplateList | Creation time                                                     | String    |
| TransTpl           | Response.TemplateList | Template parameters                                                | Container |


`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Format                | TransTpl.Container | Container format: gif, hgif, webp (hgif indicates higher-definition gif.) | String    | Yes   |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | TransTpl.Video | Codec format            | String | Yes   |  None  | gif, webp                                          |
| Width                      | TransTpl.Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]</li><li>Unit: px<br/><li>If only `Width` is set, `Height` is calculated according to the original video proportion. |
| Height                     | TransTpl.Video | Height                    | String | No   | Original video height | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Height` is set, `Width` is calculated according to the original video proportion. |
| Fps                        | TransTpl.Video | Frame rate                  | String | No   | Original video frame rate | <li>Value range: (0, 60]<br/><li>Unit: fps<br/><li>If the frame rate is greater than 60, set this parameter to `60`.<br/>This parameter is optional. If it is not set, the video is played at the speed as per the original timestamp. This parameter specifies the frame rate for animated image playback. |
| AnimateOnly<br/>KeepKeyFrame    | TransTpl.Video | Keep only key frames for animated images      | String | No   |      false        | <li>true, false<br/><li>Parameter specifying whether to keep only key frames for animated images                     |
| AnimateTime<br/>IntervalOfFrame | TransTpl.Video | Frame sampling interval for animated images      | String | No   |      None        | <li>(0, Video duration]<br/><li>Frame sampling interval for animated images<br/><li>The value of this parameter must be less than the value of `TimeInterval.Duration` if `TimeInterval.Duration` is set. |
| AnimateFrames<br/>PerSecond     | TransTpl.Video | Number of frames sampled per second for animated images | String | No   |     None         | <li>(0, Video frame rate)<br/><li>Frame sampling frequency for animated images<br/><li>Priority: AnimateFramesPerSecond > AnimateOnlyKeepKeyFrame > AnimateTimeIntervalOfFrame |
| Quality                    | TransTpl.Video | Relative quality          | String | No   |     None         | <li>[1, 100)<br/><li>This parameter is valid for WEBP images and is not available for GIF images. </li>|


`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | TransTpl.TimeInterval | Start time | String    | No   | 0 | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds. |
| Duration             | TransTpl.TimeInterval | Duration | String    | No   | Video duration | <li>[0, Video duration] <br/><li>Unit: second <br/><li>Supports the float format, accurate to milliseconds.</li> |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

**Example 1: query by template ID**

#### Request

```shell
GET /template?ids=A,B,C HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzh****=</RequestId>
    <TemplateList>
        <Name>TemplateName</Name>
        <TemplateId>A</TemplateId>
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
GET /template?page_size=10&page_number=1 HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzh****=</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
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
    </TemplateList>
</Response>
```
