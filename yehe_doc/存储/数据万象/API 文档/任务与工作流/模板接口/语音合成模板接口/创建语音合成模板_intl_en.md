## Feature Description

This API (`CreateMediaTemplate`) is used to create a text-to-speech template.

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

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
    <Tag>Tts</Tag>
    <Name>TemplateName</Name>
    <Mode>Sync</Mode>
    <Codec>pcm</Codec>
    <VoiceType>ruxue</VoiceType>
    <Volume>2</Volume>
    <Speed>200</Speed>
</Request>

```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |


`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ----------------------------------------------------- | --------- | ---- | ---- |
| Tag                | Request | Template type: Tts                                          | String    | Yes   | Tts |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| Mode               | Request | Processing mode, which is `Asyc` by default. | String   | No    | Asyc (async synthesis); Sync (sync synthesis).</br>When `Asyc` is selected, the codec can only be `pcm`. |
| Codec              | Request | Audio format, which is wav (sync)/pcm (async) by default. | String | No | wav, mp3, pcm |
| VoiceType          | Request | Voice, which is `ruxue` by default. | String | No | ruxue, aixiaonan |
| Volume             | Request | Volume, which is 0 by default. | String | No | [-10,10] |
| Speed              | Request | Speech rate, which is 100 by default. | String | No | [50,200] |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>Tts</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <TtsTpl>
            <Mode>Sync</Mode>
            <Codec>pcm</Codec>
            <VoiceType>ruxue</VoiceType>
            <Volume>2</Volume>
            <Speed>200</Speed>
        </TtsTpl>
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
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.Template | Template ID                        | String    |
| Name               | Response.Template | Template name                       | String    |
| BucketId           | Response.Template | Template bucket                 | String    |
| Category           | Response.Template | Template category: Custom or Official | String    |
| Tag                | Response.Template | Template type: Tts                                                | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| Tts                | Response.Template | Template parameters                                                | Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>Tts</Tag>
    <Name>TemplateName</Name>
    <Mode>Sync</Mode>
    <Codec>pcm</Codec>
    <VoiceType>ruxue</VoiceType>
    <Volume>2</Volume>
    <Speed>200</Speed>
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
        <Tag>Tts</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <TtsTpl>
            <Mode>Sync</Mode>
            <Codec>pcm</Codec>
            <VoiceType>ruxue</VoiceType>
            <Volume>2</Volume>
            <Speed>200</Speed>
        </TtsTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
