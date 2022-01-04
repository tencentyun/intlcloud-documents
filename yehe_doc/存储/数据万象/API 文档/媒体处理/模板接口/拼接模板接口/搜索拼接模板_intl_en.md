## Feature Description
This API (`DescribeMediaTemplates`) is used to search for concatenation templates.

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

#### Common request headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Non-common request headers
This API does not use any non-common request header.

#### Request body
The request body of this request is empty.

#### Request parameters
The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---           |:--       |:--                    |   :--     |   :--    |
| tag           | None        | Task type: Concat     | String    |Yes|
| ids           | None        | Template ID. If you enter multiple IDs, separate them with commas (,).  | String     |No|
| name          | None        | Template name prefix              | String     |No|
| pageNumber    | None        | Page number                   | Integer     |No|
| pageSize      | None        | Records per page                 | Integer     |No|


## Response

#### Response headers

#### Common response headers
This response contains [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Non-common response headers
This API does not use any non-common response header.

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
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
        </ConcatTemplate>
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
| Category           | Response.TemplateList | Template category: Custom                                             | String    |
| Tag                | Response.TemplateList | Task type: Concat                                          | String    |
| UpdateTime         | Response.TemplateList | Update time                                                     | String    |
| CreateTime         | Response.TemplateList | Creation time                                                     | String    |
| ConcatTemplate     | Response.TemplateList | Watermark information                 | Container |


`ConcatTemplate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| ConcatFragment      | Response.TemplateList.<br/>ConcatTemplate | Concatenation node    | Container    | Yes   | None  | None |
| Audio               | Response.TemplateList.<br/>ConcatTemplate | Reference position    | String    | Yes   | None  | None |
| Video               | Response.TemplateList.<br/>ConcatTemplate | Video parameters    | Container    | Yes   | None  | None |
| Container           | Response.TemplateList.<br/>ConcatTemplate | Container format    | Container    | Yes   | None  | None |

`ConcatFragment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Url                 | Response.TemplateList.<br/>ConcatTemplate.ConcatFragment | Concatenation object address   | String    | Yes   | None   | Same as the address of the bucket object file. |
| Mode                | Response.TemplateList.<br/>ConcatTemplate.ConcatFragment | Node type      | String    | Yes   | None   |<li>Start </br><li>End |


`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Codec              | Response.TemplateList.<br/>ConcatTemplate.Audio | Codec format     | String | No   | aac    | Valid values: aac, mp3                                                |
| Samplerate         | Response.TemplateList.<br/>ConcatTemplate.Audio | Sample rate         | String | No   | 44100  |<li>Unit: Hz<br/><li>Valid values: 11025, 22050, 32000, 44100, 48000, 96000<br/><li>Different container formats support different MP3 sample rates, as shown in the table below.|
| Bitrate            | Response.TemplateList.<br/>ConcatTemplate.Audio | Original audio bitrate   | String | No   | None    | <li>Unit: Kbps<br/><li>Value range: [8, 1000]                       |
| Channels           | Response.TemplateList.<br/>ConcatTemplate.Audio | Number of sound channels         | String | No   | None      | <li>If `Codec` is `aac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.<br/><li>If `Codec` is `mp3`, the value can be `1` or `2`. |

Y indicates supported, and N indicates unsupported.

| Container Format/Audio Sample Rate | 11025  | 22050|  32000 | 44100|  48000|   96000 |
| ------------------ | ------- | ------- | ------- | ------- |------------| ------------- |
| mp3     | Y       | Y| Y| Y| Y| N|

`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ---------------------------------------------------- | --------- | ---- |
| Format                | Request.ConcatTemplate.<br/>Container | Container format: mp4, flv, hls, ts, mp3, aac   | String    | Yes   |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Response.TemplateList.<br/>ConcatTemplate.Video | Codec format             | String | No   |   H.264 | H.264                                          |
| Width                      | Response.TemplateList.<br/>ConcatTemplate.Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Width` is set, `Height` is calculated according to the original video proportion. |
| Height                     | Response.TemplateList.<br/>ConcatTemplate.Video | Height                    | String | No   | Original video height | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Height` is set, `Width` is calculated according to the original video proportion. |
| Fps                        | Response.TemplateList.<br/>ConcatTemplate.Video | Frame rate                  | String | No   | Original video frame rate | <li>Value range: (0, 60]<br><li>Unit: fps |
| Bitrate                    | Response.TemplateList.<br/>ConcatTemplate.Video | Bitrate of the video output file      | String | No   |  Original video bitrate           | <li>Value range: [10, 50000]<br/><li>Unit: Kbps   </li>                  |
| Remove                     | Response.TemplateList.<br/>ConcatTemplate.Video | Whether to delete the video stream         | String | No   | false        | Valid values: true, false


#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

**Example 1: query by template ID**
#### Request

```shell
GET /template?ids=A,B,C HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
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
        </ConcatTemplate>
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
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
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
        </ConcatTemplate>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
</Response>
```
