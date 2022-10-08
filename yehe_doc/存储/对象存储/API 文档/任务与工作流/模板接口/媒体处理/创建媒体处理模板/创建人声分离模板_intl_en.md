## Feature Description

This API is used to create a voice/sound separation template.

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
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>VoiceSeparate</Tag>
    <Name>TemplateName</Name>
    <AudioMode>IsAudio</AudioMode>
    <AudioConfig>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
    </AudioConfig>
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
| Tag                | Request | Template tag: VoiceSeparate                                | String    | Yes   | None |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| AudioMode          | Request | Audio output mode                                               | String    | Yes   | IsAudio: Outputs voice<br/>IsBackground: Outputs background sound<br/>AudioAndBackground: Outputs voice and background sound |
| AudioConfig        | Request | Audio configuration                                         | Container | Yes   |  None |

<span id="AudioConfig"></span>
`AudioConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | ------------ | ------ | -------- | ------ | ------------------------------------------------------------ |
| Codec              | Request.Audio | Codec format     | String | No   | aac    | Valid values: `aac`, `mp3`, `flac`, `amr`.                                                |
| Samplerate         | Request.Audio | Sample rate         | String | No   | 44100  | 1. Unit: Hz<br/>2. Valid values: `8000`, `11025`, `22050`, `32000`, `44100`, `48000`, `96000`.<br/>3. If `Codec` is `aac` or `flac`, the value cannot be `8000`.<br/>4. If `Codec` is `mp3`, the value cannot be `8000` or `96000`.<br/>5. If `Codec` is `amr`, the value can only be `8000`. |
| Bitrate            | Request.Audio | Original audio bitrate   | String | No   | None     | 1. Unit: Kbps<br/>2. Value range: [8, 1000]|
| Channels           | Request.Audio | Number of sound channels         | String | No   | None     | 1. If `Codec` is `aac` or `flac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`. <br/>2. If `Codec` is `mp3`, the value can only be `1` or `2`. <br/>3. If `Codec` is `amr`, the value can only be `1`. |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>VoiceSeparate</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <VoiceSeparate>
            <AudioMode>IsAudio</AudioMode>
            <AudioConfig>
                <Codec>mp3</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>12</Bitrate>
                <Channels>2</Channels>
            </AudioConfig>
        </VoiceSeparate>
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
| Tag                | Response.Template | Template tag: VoiceSeparate                                       | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| VoiceSeparate      | Response.Template | Template parameters                                                | Container |


`VoiceSeparate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------ | :------------------------------- | :-------- |
| AudioMode          | Response.Template.VoiceSeparate | Same as `Request.AudioMode` in the request body.          | String |
| AudioConfig        | Response.Template.VoiceSeparate | Same as `Request.AudioConfig` in the request body.        | Container |


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
    <Tag>VoiceSeparate</Tag>
    <Name>TemplateName</Name>
    <AudioMode>IsAudio</AudioMode>
    <AudioConfig>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
    </AudioConfig>
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
        <Tag>VoiceSeparate</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <VoiceSeparate>
            <AudioMode>IsAudio</AudioMode>
            <AudioConfig>
                <Codec>mp3</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>12</Bitrate>
                <Channels>2</Channels>
            </AudioConfig>
        </VoiceSeparate>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
