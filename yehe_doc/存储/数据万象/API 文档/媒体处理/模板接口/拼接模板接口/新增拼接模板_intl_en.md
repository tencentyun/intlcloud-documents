## Feature Description
This API (`CreateMediaTemplate`) is used to create a concatenation template.

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
>

#### Request headers

#### Common request headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Non-common request headers
This API does not use any non-common request header.

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
   </ConcatTemplate>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |


`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Task type: Concat                                   | String    | Yes   |
| Name               | Request | Template name. The value can contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (*).                     | String    | Yes   |
| ConcatTemplate     | Request | Concatenation template                                                | Container | Yes   |


`ConcatTemplate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| ConcatFragment      | Request.ConcatTemplate | Concatenation node    | Container    | Yes   | None  | None |
| Audio               | Request.ConcatTemplate | Audio parameters    | Container    | No   | Original media value  | If the target file does not require audio information, set `Audio.Remove` to `true`. |
| Video               | Request.ConcatTemplate | Video parameters    | Container    | No   | Original media value  | If the target file does not require video information, set `Video.Remove` to `true`. |
| Container           | Request.ConcatTemplate | Container format     | Container    | Yes   | None  | None |


`ConcatFragment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Url                 | Request.ConcatTemplate.<br/>ConcatFragment | Concatenation object address   | String    | Yes   | None   | Same as the address of the bucket object file. |
| Mode                | Request.ConcatTemplate.<br/>ConcatFragment | Node type      | String    | Yes   | None   | <li>Start </br><li>End |


`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Codec              | Request.ConcatTemplate.<br/>Audio | Codec format     | String | Yes   | Original code of the file    | Valid values: `aac`, `mp3`                                                |
| Samplerate         | Request.ConcatTemplate.<br/>Audio | Sample rate         | String | No   | Original sample rate of the file  | <li>Unit: Hz<br/><li>Valid values: `11025`, `22050`, `32000`, `44100`, `48000`, `96000`<br/><li>Different container formats support different MP3 sample rates, as shown in the table below.|
| Bitrate            | Request.ConcatTemplate.<br/>Audio | Audio bitrate   | String | No   | Original audio bitrate of the file   | <li>Unit: Kbps<br/><li>Value range: [8, 1000]                       |
| Channels           | Request.ConcatTemplate.<br/>Audio | Number of sound channels         | String | No   | Original number of sound channels of the file      | <li>If `Codec` is `aac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.<br/><li>If `Codec` is `mp3`, the value can be `1` or `2`. |

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
| Codec                      | Request.ConcatTemplate.<br/>Video | Codec format             | String | Yes   |   H.264 | H.264                                          |
| Width                      | Request.ConcatTemplate.<br/>Video | Width                    | String | No   | Original video width | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Width` is set, `Height` is calculated according to the original video proportion. |
| Height                     | Request.ConcatTemplate.<br/>Video | Height                    | String | No   | Original video height | <li>Value range: [128, 4096]<br/><li>Unit: px<br/><li>If only `Height` is set, `Width` is calculated according to the original video proportion. |
| Fps                        | Request.ConcatTemplate.<br/>Video | Frame rate                  | String | No   | Original video frame rate | <li>Value range: (0, 60]<br><li>Unit: fps |
| Bitrate                    | Request.ConcatTemplate.<br/>Video | Bitrate of the video output file      | String | No   |  Original video bitrate           | <li>Value range: [10, 50000]<br/><li>Unit: Kbps    </li>                 |
| Remove                     | Request.ConcatTemplate.<br/>Video | Whether to delete the video stream         | String | No   | false        | Valid values: `true`, `false`

## Response

#### Response headers

#### Common response headers
This response contains [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Non-common response headers
This API does not use any non-common response header.

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
        </ConcatTemplate>
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
| :----------------- | :------- | :----------------------------- | :-------- |
| TemplateId         | Response | Template ID                                                      | String    |
| TotalCount         | Response | Total number of templates                                               | Int       |
| PageNumber         | Response | Current page number. Same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of records per page. Same as `pageSize` in the request.                             | Int       |
| ConcatTemplate     | Response | Concatenation information. Same as `ConcatTemplate` in the request body.  | Container |



#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

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
        </ConcatTemplate>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
