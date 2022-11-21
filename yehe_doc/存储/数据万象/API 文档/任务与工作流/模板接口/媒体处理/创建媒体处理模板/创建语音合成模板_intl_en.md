## Feature Description

This API is used to create a text-to-speech template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateTranscodeTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | -------------------------------------------- | ------ | -------- | ------------------------------------------------------------ |
| Tag                | Request | Template tag: Tts                                          | String    | Yes   | Tts |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| Mode               | Request | Processing mode, which is `Asyc` by default. | String   | No    | `Asyc` (async synthesis); `Sync` (sync synthesis).</br>When `Asyc` is selected, the codec can only be `pcm`. |
| Codec              | Request | Audio format, which is `wav` (sync) or `pcm` (async) by default. | String | No | `wav`, `mp3`, `pcm` |
| VoiceType          | Request | Voice, which is `ruxue` by default. | String | No | See the table below |
| Volume             | Request | Volume, which is `0` by default. | String | No | [-10,10] |
| Speed              | Request | Speech rate, which is `100` by default. | String | No | [50,200] |

Supported voices

| Name | Voice Parameter Value | Async Synthesis | Sync Synthesis |
|---------|---------|---------|---------|
| Ruxue   | ruxue       | Supported | Supported  |
| Aixiaonan | aixiaonan   | Not supported  | Supported |
| Aixiaoxing | aixiaoxing  | Supported | Supported |
| Aixiaocheng | aixiaocheng | Supported | Supported |
| Aixiaoxue | aixiaoxue   | Supported | Supported |
| Aixiaolu | aixiaolu    | Supported | Supported |
| Aixiaodong | aixiaodong  | Supported | Supported |
| Aixiaoliao | aixiaoliao  | Not supported | Supported |
| Aixiaoqian | aixiaoqian  | Supported | Supported |
| Aixiaoyang | aixiaoyang  | Supported | Supported |
| Alice | alice        | Supported | Supported |

Voice description

| Name | Voice Parameter Value | Type | Use Case | Supported Languages | Voice Quality |
|---------|---------|---------|---------|---------|---------|
| Ruxue | ruxue | Standard female voice | General | Chinese, Chinese-English mix | Standard |
| Aixiaonan | aixiaonan | Sweet female voice | General, social | Chinese, Chinese-English mix | Premium |
| Aixiaoxing | aixiaoxing | Vigorous male voice | General, commentary | Chinese, Chinese-English mix | Premium |
| Aixiaocheng | aixiaocheng | Standard male voice | General | Chinese, Chinese-English mix | Standard |
| Aixiaoxue | aixiaoxue   | Standard female voice | General, customer service | Chinese, Chinese-English mix | Standard |
| Aixiaolu | aixiaolu    | Reading female voice | General, audiobook | Chinese, Chinese-English mix | Standard |
| Aixiaodong | aixiaodong  | News male voice | General, news broadcasting | Chinese, Chinese-English mix | Standard |
| Aixiaoliao | aixiaoliao  | Sentimental female voice | General, social | Chinese, Chinese-English mix | Premium |
| Aixiaoqian | aixiaoqian  | Vigorous female voice | General, social | Chinese, Chinese-English mix | Premium |
| Aixiaoyang | aixiaoyang  | Broadcasting male voice | General, news broadcasting | Chinese, Chinese-English mix | Standard |
| Alice | alice        | English female voice | General | English | Standard |

Multi-sentiment voice description

| Name | Voice Parameter Value | Sentiment Category |
|---------|---------|---------|
| Aixiaoxing | aixiaoxing | Neutral, excited |
| Aixiaocheng | aixiaocheng | Neutral, broadcasting |
| Aixiaoxue | aixiaoxue   | Neutral, broadcasting, customer service |
| Aixiaolu | aixiaolu    | Neutral, story telling, customer service |


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
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
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
| Response           | None     | Result storage container | Container |

<span id="Response"></span>
`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.Template | Template ID                        | String    |
| Name               | Response.Template | Template name                       | String    |
| BucketId           | Response.Template | Template bucket                 | String    |
| Category           | Response.Template | Template category: `Custom` or `Official` | String    |
| Tag                | Response.Template | Template tag: Tts                                                | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| TtsTpl    | Response.Template     | Template parameters                                                | Container |

`TtsTpl` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | 
| :----------------- | :----------------------------- | :------------------------------- |
| Mode               | Response.Template.TtsTpl | Same as `Request.Mode` in the request body.  |
| Codec              | Response.Template.TtsTpl | Same as `Request.Codec` in the request body. |
| VoiceType          | Response.Template.TtsTpl | Same as `Request.VoiceType` in the request body. |
| Volume             | Response.Template.TtsTpl | Same as `Request.Volume` in the request body. |
| Speed              | Response.Template.TtsTpl | Same as `Request.Speed` in the request body. |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).


## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
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
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <Template>
        <Tag>Tts</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
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
